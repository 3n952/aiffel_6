# AIFFEL Campus Online Code Peer Review

- 코더 : 김산
- 리뷰어 : 이동희


# PRT(Peer Review)
- [x]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**

> 문제에서 요구하는 최종 결과물이 첨부되었는지 확인
> 문제를 해결하는 완성된 코드란 프로젝트 루브릭 3개 중 2개, 
> 퀘스트 문제 요구조건 등을 지칭

1. 기본모델 구성과 학습 진행 완료
2. classification map 얻은 뒤 시각화 완료
3. cam과 grad-cam 비교 완료
    
- [x]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**

> 해당 코드 블럭에 doc string/annotation이 달려 있는지 확인
> 해당 코드가 무슨 기능을 하는지, 왜 그렇게 짜여진건지, 작동 메커니즘이 뭔지 기술.
> 주석을 보고 코드 이해가 잘 되었는지 확인
```python

def generate_grad_cam(model, activation_layer, item):
    item = copy.deepcopy(item)
    width = item['image'].shape[1]
    height = item['image'].shape[0]
    img_tensor, class_idx = normalize_and_resize_img(item)
    
    # Grad cam에서도 cam과 같이 특정 레이어의 output을 필요로 하므로 모델의 input과 output을 새롭게 정의합니다.
    # 이때 원하는 레이어가 다를 수 있으니 해당 레이어의 이름으로 찾은 후 output으로 추가합니다.
    grad_model = tf.keras.models.Model([model.inputs], [model.get_layer(activation_layer).output, model.output])
    
    # Gradient를 얻기 위해 tape를 사용합니다.
    with tf.GradientTape() as tape:
        conv_output, pred = grad_model(tf.expand_dims(img_tensor, 0))
    
        loss = pred[:, class_idx] # 원하는 class(여기서는 정답으로 활용) 예측값을 얻습니다.
        output = conv_output[0] # 원하는 layer의 output을 얻습니다.
        grad_val = tape.gradient(loss, conv_output)[0] # 예측값에 따른 Layer의 gradient를 얻습니다.

    weights = np.mean(grad_val, axis=(0, 1)) # gradient의 GAP으로 weight를 구합니다.
    grad_cam_image = np.zeros(dtype=np.float32, shape=conv_output.shape[0:2])
    for k, w in enumerate(weights):
        # output의 k번째 채널과 k번째 weight를 곱하고 누적해서 class activation map을 얻습니다.
        grad_cam_image += w * output[:, :, k]
        
    grad_cam_image = tf.math.maximum(0, grad_cam_image)
    grad_cam_image /= np.max(grad_cam_image)
    grad_cam_image = grad_cam_image.numpy()
    grad_cam_image = cv2.resize(grad_cam_image, (width, height))
    return grad_cam_image
```

     
- [x]  **3. 에러가 난 부분을 디버깅하여 문제를 “해결한 기록을 남겼거나” 
”새로운 시도 또는 추가 실험을 수행”해봤나요?**

> 문제 원인 및 해결 과정을 잘 기록하였는지 확인
> 문제에서 요구하는 조건에 더해 추가적으로 수행한 나만의 시도, 
> 실험이 기록되어 있는지 확인

> -> 엉망진창이다. activation dense layer에서 학습이 잘 안됐나..? (해결!)
> 원인은 학습이 잘 진행되지 않았기 떄문이였다.
`preds = keras.layers.Dense(num_classes, activation='softmax')(x)`
softmax를 추가하고 모델을 다시 학습시켜서 cam과 grad-cam을 구한 점.
        
- [x]  **4. 회고를 잘 작성했나요?**

> 주어진 문제를 해결하는 완성된 코드 내지 프로젝트 결과물에 대해
> 배운점과 아쉬운점, 느낀점 등이 기록되어 있는지 확인
> 전체 코드 실행 플로우를 그래프로 그려서 이해를 돕고 있는지 확인

>모델의 분류기 부분이 제대로 학습이 되어야 CAM / grad-CAM이 feature map의 어떤 부분을 activation하는 것인지 파악할 수 있다는 것을
시각적으로 파악할 수 있었다.
>cam / grad-cam의 분류기 성능을 높히는 것 이외에 bounding box외각선 그리는 함수의 thresh hold를 어떻게 바꿔야 더 효과적으로 바뀔지
파악하는 것이 필요하다. 이를 위해서는 각 output의 image histogram으로 시각화 해보는 게 필요할 것 같다.
        
- [x]  **5. 코드가 간결하고 효율적인가요?**

> 파이썬 스타일 가이드 (PEP8) 를 준수하였는지 확인
> 하드코딩을 하지않고 함수화, 모듈화가 가능한 부분은 함수를 만들거나 클래스로 짰는지
> 코드 중복을 최소화하고 범용적으로 사용할 수 있도록 함수화했는지

```python
def rect_to_minmax(rect, image):
    bbox = [
        rect[:,1].min()/float(image.shape[0]),  #bounding box의 y_min
        rect[:,0].min()/float(image.shape[1]),  #bounding box의 x_min
        rect[:,1].max()/float(image.shape[0]), #bounding box의 y_max
        rect[:,0].max()/float(image.shape[1]) #bounding box의 x_max
    ]
    return bbox
```


# 참고 링크 및 코드 개선
```
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
```

# AIFFEL Campus Online Code Peer Review

- 코더 : 김 산.
- 리뷰어 : 이동희


# PRT(Peer Review)
- [x]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**

> 문제에서 요구하는 최종 결과물이 첨부되었는지 확인
> 문제를 해결하는 완성된 코드란 프로젝트 루브릭 3개 중 2개, 
> 퀘스트 문제 요구조건 등을 지칭
> 해당 조건을 만족하는 코드를 캡쳐해 근거로 첨부

> 1. multiface detection을 위한 widerface 데이터셋의 전처리가 적절히 진행되었다. -> O
> 2. SSD 모델이 안정적으로 학습되어 multiface detection이 가능해졌다. -> O
> 3. 이미지 속 다수의 얼굴에 스티커가 적용되었다. -> O
    
- [x]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**

> 해당 코드 블럭에 doc string/annotation이 달려 있는지 확인
> 해당 코드가 무슨 기능을 하는지, 왜 그렇게 짜여진건지, 작동 메커니즘이 뭔지 기술.
> 주석을 보고 코드 이해가 잘 되었는지 확인
> 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.

> _transform_data : augmemtation과 label을 encoding 하여 기존의 dataset을 변환하는 메소드
> _parse_tfrecord : TFRecord 에 _transform_data를 적용하는 함수 클로저 생성
> load_tfrecord_dataset : tf.data.TFRecordDataset.map()에 _parse_tfrecord을 적용하는 실제 데이터셋 변환 메인 메소드
> load_dataset : load_tfrecord_dataset을 통해 train, validation 데이터셋을 생성하는 최종 메소드
        
- [x]  **3. 에러가 난 부분을 디버깅하여 문제를 “해결한 기록을 남겼거나” 
”새로운 시도 또는 추가 실험을 수행”해봤나요?**

> 문제 원인 및 해결 과정을 잘 기록하였는지 확인
> 문제에서 요구하는 조건에 더해 추가적으로 수행한 나만의 시도, 
> 실험이 기록되어 있는지 확인
> 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.

> 추가 실험
> 에포크 40일 때 성능이 제일 좋다고 판단 -> 기준 40
> 사람을 잘 인식하지 못하는 것 같다. 여러 노이즈가 섞인 이미지를 넣어 확인해보자

학습과정 시각화
```python
# training loop

loss_list = []
loc_loss = []
class_loss = []

EPOCHS = 50

for epoch in range(0, EPOCHS):
    for step, (inputs, labels) in enumerate(train_dataset.take(steps_per_epoch)):
        load_t0 = time.time()
        total_loss, losses = train_step(inputs, labels)
        load_t1 = time.time()
        batch_time = load_t1 - load_t0
        
        # flush = true 이면, ouput clear된다. 즉 에포크마다 한 줄 씩 나오는게 아니라 계속 초기화 되면서 출력
        print(f"\rEpoch: {epoch + 1}/{EPOCHS} | Batch {step + 1}/{steps_per_epoch} | Loss: {total_loss:.6f} | loc loss:{losses['loc']:.6f} | class loss:{losses['class']:.6f} ",end = '',flush=True)
        
    loss_list.append(total_loss)
    loc_loss.append(losses['loc'])
    class_loss.append(losses['class'])
    filepath = os.path.join(os.getenv('HOME')+'/aiffel/aiffel_6/GD07/weights', f'weights_epoch_{(epoch + 1):03d}.h5')
    model.save_weights(filepath)
```

![image](https://github.com/3n952/aiffel_6/assets/29495950/c9cf02b1-7269-4697-b4c7-2888da436cc0)


- [x]  **4. 회고를 잘 작성했나요?**

> 주어진 문제를 해결하는 완성된 코드 내지 프로젝트 결과물에 대해
> 배운점과 아쉬운점, 느낀점 등이 기록되어 있는지 확인
> 전체 코드 실행 플로우를 그래프로 그려서 이해를 돕고 있는지 확인
> 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.

> face를 잘 detect하지 못하는 경우에 대해 생각해본 것을 구현하여 실험 결과에 포함시키고 싶었는데
시간이 부족하여 넣지 못한 것이 아쉽다.
> 산타 모자를 적용할 때, 매우 부자연스럽다. ex) 깨지는 화질, 고정된 모자의 각도 및 크기 등등..
이를 해결할 수 있는 방안이 필요하다.
> 가까운 사람에게 큰 모자 멀리 있는 사람에게 작은 모자
> 얼굴의 각도에 따른 모자의 각도 조정

        
- [x]  **5. 코드가 간결하고 효율적인가요?**

> 파이썬 스타일 가이드 (PEP8) 를 준수하였는지 확인
> 하드코딩을 하지않고 함수화, 모듈화가 가능한 부분은 함수를 만들거나 클래스로 짰는지
> 코드 중복을 최소화하고 범용적으로 사용할 수 있도록 함수화했는지
> 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.


# 참고 링크 및 코드 개선
```
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
```

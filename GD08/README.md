# AIFFEL Campus Online Code Peer Review

- 코더 : 김 산.
- 리뷰어 : 이 동희.


# PRT(Peer Review)
- [x]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**

> 문제에서 요구하는 최종 결과물이 첨부되었는지 확인
> 문제를 해결하는 완성된 코드란 프로젝트 루브릭 3개 중 2개, 
> 퀘스트 문제 요구조건 등을 지칭
> 해당 조건을 만족하는 코드를 캡쳐해 근거로 첨부

> 1. TFRecord를 활용한 데이터셋 구성과 전처리를 통해 프로젝트 베이스라인 구성을 확인하였다 -> O
> 2. simplebaseline 모델을 정상적으로 구현하였다. -> O
> 3. Hourglass모델과 simplebaseline 모델을 비교분석한 결과를 체계적으로 정리하였다. ->  O
    
- [x]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**

> 해당 코드 블럭에 doc string/annotation이 달려 있는지 확인
> 해당 코드가 무슨 기능을 하는지, 왜 그렇게 짜여진건지, 작동 메커니즘이 뭔지 기술.
> 주석을 보고 코드 이해가 잘 되었는지 확인
> 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.
        
- [x]  **3. 에러가 난 부분을 디버깅하여 문제를 “해결한 기록을 남겼거나” 
”새로운 시도 또는 추가 실험을 수행”해봤나요?**

> 문제 원인 및 해결 과정을 잘 기록하였는지 확인
> 문제에서 요구하는 조건에 더해 추가적으로 수행한 나만의 시도, 
> 실험이 기록되어 있는지 확인
> 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.

> 위의 오류를 해결하지 못하여 simplebaseline에 대하여 keras.model.fit을 사용하기로 했다 ..
```py
# data input
strategy = tf.distribute.MirroredStrategy()
global_batch_size = strategy.num_replicas_in_sync * batch_size

train_dataset = create_dataset(train_tfrecords, global_batch_size, num_heatmap, is_train=True)
val_dataset = create_dataset(val_tfrecords, global_batch_size, num_heatmap, is_train=False)

# model checkpoint
model_checkpoint = os.getenv('HOME') + '/aiffel/aiffel_6/GD08/weights'+ '/simple_model-epoch-{epoch:02d}-loss-{val_loss:.4f}.h5'

model_cb = tf.keras.callbacks.ModelCheckpoint(filepath = model_checkpoint,
                                             save_weights_only = True,
                                             save_best_only = True,
                                             monitor = 'val_loss',
                                             )

# compile
simple_loss = tf.keras.losses.MeanSquaredError(reduction = tf.keras.losses.Reduction.NONE)
simple_optimizer = tf.keras.optimizers.Adam(learning_rate = learning_rate)

simplebase_model.compile(optimizer = simple_optimizer, loss = simple_loss)

# training
simple_history = simplebase_model.fit(train_dataset,
                                     epochs = epochs,
                                     batch_size = batch_size,
                                     validation_data = val_dataset,
                                     callbacks = [model_cb])
```
        
- [x]  **4. 회고를 잘 작성했나요?**

> 주어진 문제를 해결하는 완성된 코드 내지 프로젝트 결과물에 대해
> 배운점과 아쉬운점, 느낀점 등이 기록되어 있는지 확인
> 전체 코드 실행 플로우를 그래프로 그려서 이해를 돕고 있는지 확인
> 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.

> 회고하기
> 1. simplebaseline model을 학습할 때, 기존에 정의한 trainer, train을 사용하여 학습하면 문제가 생긴다. 이 부분을 해결하기 위해 simplebaseline과 stackedhourglass 모델 두 경우에 대해 다른 compute_loss를 계산했다. 하지만, simplebaseline 모델을 정의할 때, resnet 모델을 앞 단에서 먼저 함수 밖에서 선언했는데, 이게 문제라고 한다. 실제로 해보고 돌아가는 지는 시간관계상 못해보았지만, 코드는 다 수정해놓았다.
> 2. 같은 loss를 사용했는데 크게 차이가 나는 이유는 batch_size 차이에서 오는 건가? 라는 의문이 들었다. loss가 적고 크게 나오는데에 batch_size가 미치는 영향에 대해 생각해 볼 필요가 있다.
> 3. loss가 크게 다름에도 불구하고 실제로 inference를 해보면 비슷한 성능을 내는 것을 확인할 수 있었다.
> 4. 모델의 크기에 큰 차이가 있음에도 실제 결과의 큰 차이가 없는 것이 흥미로웠다.


- [x]  **5. 코드가 간결하고 효율적인가요?**

> 파이썬 스타일 가이드 (PEP8) 를 준수하였는지 확인
> 하드코딩을 하지않고 함수화, 모듈화가 가능한 부분은 함수를 만들거나 클래스로 짰는지
> 코드 중복을 최소화하고 범용적으로 사용할 수 있도록 함수화했는지
> 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.

```py
def Simplebaseline(input_shape=(256, 256, 3)):
    # resnet backbone
    resnet = tf.keras.applications.resnet.ResNet50(include_top=False, weights='imagenet')
                                                   
    inputs = tf.keras.Input(shape=input_shape)
    x = resnet(inputs)
    x = upconv(x)
    out = final_layer(x)
    model = tf.keras.Model(inputs, out, name='simple_baseline')
    
    return model
```

# 참고 링크 및 코드 개선
```
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
```

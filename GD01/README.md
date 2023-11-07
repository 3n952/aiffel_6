# AIFFEL Campus Online Code Peer Review
- 코더 : 김산
- 리뷰어 : 이동희


# PRT(Peer Review)
- [x]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**
    - 문제에서 요구하는 최종 결과물이 첨부되었는지 확인
    - 문제를 해결하는 완성된 코드란 프로젝트 루브릭 3개 중 2개, 
    퀘스트 문제 요구조건 등을 지칭
        - 해당 조건을 만족하는 코드를 캡쳐해 근거로 첨부
> 1. ResNet-34, ResNet-50 모델 구현이 정상적으로 진행되었는가?	O
> 2. 구현한 ResNet 모델을 활용하여 Image Classification 모델 훈련이 가능한가? O 
> 3. Ablation Study 결과가 바른 포맷으로 제출되었는가?	O
    
- []  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**
    - 해당 코드 블럭에 doc string/annotation이 달려 있는지 확인
    - 해당 코드가 무슨 기능을 하는지, 왜 그렇게 짜여진건지, 작동 메커니즘이 뭔지 기술.
    - 주석을 보고 코드 이해가 잘 되었는지 확인
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.

주석은 거의 없습니다.

        
- [x]  **3. 에러가 난 부분을 디버깅하여 문제를 “해결한 기록을 남겼거나” 
”새로운 시도 또는 추가 실험을 수행”해봤나요?**
    - 문제 원인 및 해결 과정을 잘 기록하였는지 확인
    - 문제에서 요구하는 조건에 더해 추가적으로 수행한 나만의 시도, 
    실험이 기록되어 있는지 확인
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.
        
- [x]  **4. 회고를 잘 작성했나요?**
    - 주어진 문제를 해결하는 완성된 코드 내지 프로젝트 결과물에 대해
    배운점과 아쉬운점, 느낀점 등이 기록되어 있는지 확인
    - 전체 코드 실행 플로우를 그래프로 그려서 이해를 돕고 있는지 확인
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.
> 회고
> 1. url로 tfds로 데이터를 load하는 방법과 로컬에 데이터를 다운받아 image_dataset_from_directory를 사용하는 것에 차이가 있다. -> 첫번쨰 방법은 코랩에서 되지만 lms 커널 상에서 안된다..
> 2. 각 모델이 몇 epoch에서 과대적합이 발생하는 지 파악하고, 그 때의 모델을 모니터링하는 것이 필요할 것 같다. 따라서 epoch를 늘려서 학습시켜 봐야한다.
> 3. validation accuracy의 값이 튀는 경향이 있어보이는데, 에포크를 늘리면 어느정도 해결될 것 같다.
> 4. validation accuracy 기준으로 성능이 좋은 모델은 resnet34 > resnet50 > plain50 > plain34 순 이다.

- [x]  **5. 코드가 간결하고 효율적인가요?**
    - 파이썬 스타일 가이드 (PEP8) 를 준수하였는지 확인
    - 하드코딩을 하지않고 함수화, 모듈화가 가능한 부분은 함수를 만들거나 클래스로 짰는지
    - 코드 중복을 최소화하고 범용적으로 사용할 수 있도록 함수화했는지
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.

conv_block부분을 activation 유뮤로 함수화시킨점이 정말 좋습니다.
```python
# resnet conv block
def conv_block(layer, channel, kernel_size, strides = 1, padding='same', activation='relu'):
    x = keras.layers.Conv2D(filters=channel,
                            kernel_size=kernel_size,
                            kernel_initializer='he_normal',
                            padding=padding,
                            strides=strides)(layer)
    x = keras.layers.BatchNormalization()(x)
    if activation:
        x = keras.layers.Activation(activation)(x)
    
    return x
```


# 참고 링크 및 코드 개선
```
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
ResNet-50 전체 구조 시각화
https://ethereon.github.io/netscope/#/gist/db945b393d40bfa26006
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
```

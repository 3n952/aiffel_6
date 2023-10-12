# AIFFEL Campus Online Code Peer Review
- 코더 : 김산
- 리뷰어 : 임정훈.


# PRT(Peer Review)
- [ ]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**
    - 문제에서 요구하는 최종 결과물이 첨부되었는지 확인
    - 문제를 해결하는 완성된 코드란 프로젝트 루브릭 3개 중 2개, 
    퀘스트 문제 요구조건 등을 지칭
        - 해당 조건을 만족하는 코드를 캡쳐해 근거로 첨부
        
> 1. 한국어 전처리를 통해 학습 데이터셋을 구축하였다.	공백과 특수문자 처리, 토크나이징, 병렬데이터 구축의 과정이 적절히 진행되었다. - 0
> 2. 트랜스포머 모델을 구현하여 한국어 챗봇 모델 학습을 정상적으로 진행하였다.	구현한 트랜스포머 모델이 한국어 병렬 데이터 학습 시 안정적으로 수렴하였다. - 0
> 3. 한국어 입력문장에 대해 한국어로 답변하는 함수를 구현하였다.	한국어 입력문장에 맥락에 맞는 한국어로 답변을 리턴하였다. - 0
    
- [ ]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**
    - 해당 코드 블럭에 doc string/annotation이 달려 있는지 확인 - 0
    - 해당 코드가 무슨 기능을 하는지, 왜 그렇게 짜여진건지, 작동 메커니즘이 뭔지 기술. - 0
    - 주석을 보고 코드 이해가 잘 되었는지 확인  - 0
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.
        
> 네 모두 잘 작성되어 있습니다
```
    python
    # 사용할 샘플의 최대 개수
    MAX_SAMPLES = 50000

    # 정규표현식을 사용하여 구두점을 제거
    def preprocess_sentence(sentence):
        # 단어와 구두점(punctuation) 사이의 거리를 만듭니다.
        # 예를 들어서 "I am a student." => "I am a student ."와 같이
        # student와 온점 사이에 거리를 만듭니다.
        sentence = re.sub(r"([?.!,])", r" \1 ", sentence)
        sentence = re.sub(r'[" "]+', " ", sentence)

        # (a-z, A-Z, ㄱ-ㅎ, ㅏ-ㅣ,가-힣,0-9, ".", "?", "!", ",")를 제외한 모든 문자를 공백인 ' '로 대체합니다.
        sentence = re.sub(r"[^a-zA-Zㄱ-ㅣ가-힣0-9?.!,]+", " ", sentence) 
        sentence = sentence.strip()
        return sentence
```
        
- [ ]  **3. 에러가 난 부분을 디버깅하여 문제를 “해결한 기록을 남겼거나” 
”새로운 시도 또는 추가 실험을 수행”해봤나요?**
    - 문제 원인 및 해결 과정을 잘 기록하였는지 확인 - 0
    - 문제에서 요구하는 조건에 더해 추가적으로 수행한 나만의 시도, 
    실험이 기록되어 있는지 확인 - 0
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.
        
>네 모두 잘 수행하였습니다.
```
python
#한국어 불용어 사전 출처: https://ahnsun98.tistory.com/35
#txt 파일에 한 줄에 불용어가 하나씩 작성 되어있다. 따라서 이것을 한 칸씩 띄어 다시 작성한다.
#불용어 제거 시도

stopword_path = "/aiffel/aiffel/workspace/transformer_cb/data/stopword.txt"
stopword_file = open(stopword_path)
stopwords = []
for line in stopword_file: 
    stopwords.append(line.replace(" ",""))

for i in range(len(stopwords)):
    stopwords[i].replace("\n","")
    
stopword_file.close()

stopwords

# 불용어를 제거할 필요가 없다고 판단.
# 바로 구두점을 제거를 실행
    
```
- [ ]  **4. 회고를 잘 작성했나요?**
    - 주어진 문제를 해결하는 완성된 코드 내지 프로젝트 결과물에 대해
    배운점과 아쉬운점, 느낀점 등이 기록되어 있는지 확인 - 0
    - 전체 코드 실행 플로우를 그래프로 그려서 이해를 돕고 있는지 확인 - 0
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.
 > 네 모두 잘 작성하였습니다.
```
1. 트랜스포머의 각 구조의 역할과 기능에 대해 좀 더 자세히 공부할 시간이 필요하다.(ing)
2. 한국어 불용어를 제거하려는 시도를 했는데 이것이 효과적일지 의문이 들어서 하지 않았지만, 실제 실험을 통해 확인해보는 것도 좋을 것 같다.
3. 데이터 셋에 일상적인 대화가 많으므로 수학적 연산, 표현과 관련된 대화에서는 부자연스러운 대답을 하는 것 같다. 
```
- [ ]  **5. 코드가 간결하고 효율적인가요?**
    - 파이썬 스타일 가이드 (PEP8) 를 준수하였는지 확인 - 0
    - 하드코딩을 하지않고 함수화, 모듈화가 가능한 부분은 함수를 만들거나 클래스로 짰는지 - 0
    - 코드 중복을 최소화하고 범용적으로 사용할 수 있도록 함수화했는지 - 0
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.

```
python
# 포지셔널 인코딩 레이어
class PositionalEncoding(tf.keras.layers.Layer):
    def __init__(self, position, d_model):
        super(PositionalEncoding, self).__init__()
        self.pos_encoding = self.positional_encoding(position, d_model)
    
    def get_angles(self, position, i, d_model):
        angles = 1 / tf.pow(10000, (2 * (i // 2)) / tf.cast(d_model, tf.float32))
        return position * angles
    
    def positional_encoding(self, position, d_model):
        # 각도 배열 생성
        angle_rads = self.get_angles(
        position=tf.range(position, dtype=tf.float32)[:, tf.newaxis],
        i=tf.range(d_model, dtype=tf.float32)[tf.newaxis, :],
        d_model=d_model)

        # 배열의 짝수 인덱스에는 sin 함수 적용
        sines = tf.math.sin(angle_rads[:, 0::2])
        # 배열의 홀수 인덱스에는 cosine 함수 적용
        cosines = tf.math.cos(angle_rads[:, 1::2])

        # sin과 cosine이 교차되도록 재배열
        pos_encoding = tf.stack([sines, cosines], axis=0)
        pos_encoding = tf.transpose(pos_encoding,[1, 2, 0]) 
        pos_encoding = tf.reshape(pos_encoding, [position, d_model])

        pos_encoding = pos_encoding[tf.newaxis, ...]
        return tf.cast(pos_encoding, tf.float32)
    
    def call(self, inputs):
        return inputs + self.pos_encoding[:, :tf.shape(inputs)[1], :]

```

# 참고 링크 및 코드 개선
```
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
```

```
python
tf.keras.utils.plot_model(model, show_shapes=True)
```
> 생성한 모델을 시각적으로 그려볼 수 있어서 좋습니다f.keras.utils.plot_model(model, show_shapes=True)
> pickle라이브러리로 저장해 놓으면 재사용할 때 용이할 것 같습니다. 모델도 마찬가지로 저장하면 좋을 것 같습니다.
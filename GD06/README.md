# AIFFEL Campus Online Code Peer Review

- 코더 : 김산
- 리뷰어 : 김태민


# PRT(Peer Review)
- [x]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**

루브릭
- [x] 1. Text recognition을 위해 특화된 데이터셋 구성이 체계적으로 진행되었다.<br/>

      - 텍스트 이미지 리사이징, ctc loss 측정을 위한 라벨 인코딩, 배치처리 등이 적절히 수행되었다.
      
- [x] 2. CRNN 기반의 recognition 모델의 학습이 정상적으로 진행되었다.<br/>

      - 학습결과 loss가 안정적으로 감소하고 대부분의 문자인식 추론 결과가 정확하다.
      
![image](https://github.com/3n952/aiffel_6/assets/29370771/f9ec8653-f31e-41de-b688-fbee92e7c3c9)
![image](https://github.com/3n952/aiffel_6/assets/29370771/1dc058b6-9e2d-4d83-a6f4-8ed9917610da)


- [x] 3. keras-ocr detector와 CRNN recognizer를 엮어 원본 이미지 입력으로부터 text가 출력되는 OCR이 End-to-End로 구성되었다.<BR/>

      - 샘플 이미지를 원본으로 받아 OCR 수행 결과를 리턴하는 1개의 함수가 만들어졌다.

![image](https://github.com/3n952/aiffel_6/assets/29370771/e5bd0c29-35e8-471f-8263-a5431a8088d3)
![image](https://github.com/3n952/aiffel_6/assets/29370771/dc28c074-b13b-4760-9098-7ce0f4f6f213)




- [x]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**<br/>

        - 잘 작성했습니다.
![image](https://github.com/3n952/aiffel_6/assets/29370771/bc621d6d-96a2-4162-b61e-383fcab9fea2)

        
- [ ]  **3. 에러가 난 부분을 디버깅하여 문제를 “해결한 기록을 남겼거나” 
”새로운 시도 또는 추가 실험을 수행”해봤나요?**<br/>

        - 해결한 기록과 새로운 시도한 기록이 없습니다.
        
- [x]  **4. 회고를 잘 작성했나요?**<br/>

      - 잘 작성했습니다.
![image](https://github.com/3n952/aiffel_6/assets/29370771/7cb9fe2a-7ab0-4001-b21f-4ce6b92ebea8)

        
- [x]  **5. 코드가 간결하고 효율적인가요?**<br/>

        - 잘 작성했습니다.
![image](https://github.com/3n952/aiffel_6/assets/29370771/c722d538-e73f-4585-8c55-10ceece664bf)



# 참고 링크 및 코드 개선
```
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
```

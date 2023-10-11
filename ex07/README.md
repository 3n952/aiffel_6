# AIFFEL Campus Online Code Peer Review
- 코더 : 김산
- 리뷰어 : 김서연


# PRT(Peer Review)
- [ ]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**
    - <img width="912" alt="스크린샷 2023-10-11 오후 12 40 44" src="https://github.com/Seoyeon1129/aiffel_6/assets/112914475/2ee8b54d-ec68-4133-8678-acb36cace8ea">
    - 결과물이 잘 출력되었는데 생성 이미지가 원본과 너무 흡사하다?
    - <img width="701" alt="스크린샷 2023-10-11 오후 12 41 35" src="https://github.com/Seoyeon1129/aiffel_6/assets/112914475/ced47ee2-2666-4c81-84ab-b0dc809dcb1f">
    - 위 코드에서 fake_disc, real_disc 정의할 때 argument 순서가 서로 다른 것이 원인이지 않을까?


    
- [ ]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**
    - <img width="635" alt="스크린샷 2023-10-11 오후 12 13 14" src="https://github.com/3n952/aiffel_6/assets/112914475/d61dc231-40e2-47fa-9234-eb3be1c30d6a">
    - data augmentation에서 어떤 작업을 했는지 주석으로 남기면 좋을 것 같다.
- [ ]  **3. 에러가 난 부분을 디버깅하여 문제를 “해결한 기록을 남겼거나” ”새로운 시도 또는 추가 실험을 수행”해봤나요?**
    - 특별히 없음.
        
- [ ]  **4. 회고를 잘 작성했나요?**
    - <img width="602" alt="스크린샷 2023-10-11 오후 12 42 32" src="https://github.com/Seoyeon1129/aiffel_6/assets/112914475/ac212b90-aa3c-4ecb-a507-2815623d8fa1">
    - 아쉬운 점과 잘 이해되지 않는 점을 잘 작성했다.

        
- [ ]  **5. 코드가 간결하고 효율적인가요?**
    - <img width="435" alt="스크린샷 2023-10-11 오후 12 07 43" src="https://github.com/3n952/aiffel_6/assets/112914475/5c0f5eec-e12d-4a94-8142-73bbe68096aa">
    - constant padding을 넣어서 이미지에 여백이 생겼는데 이 부분이 학습에 영향을 끼치지는 않을까?
    - <img width="603" alt="스크린샷 2023-10-11 오후 12 11 06" src="https://github.com/3n952/aiffel_6/assets/112914475/fa648e30-1685-408f-8060-a9a6f5b40c40">
    - <img width="672" alt="스크린샷 2023-10-11 오후 12 11 17" src="https://github.com/3n952/aiffel_6/assets/112914475/0e610b9c-3152-433a-a840-165a9580ca46">
    - 사용되지 않는 Encoder, Decoder 클래스가 코드에 남아있다.



# 참고 링크 및 코드 개선
```
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
```

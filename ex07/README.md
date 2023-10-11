# AIFFEL Campus Online Code Peer Review
- 코더 : 김산
- 리뷰어 : 김서연


# PRT(Peer Review)
- [ ]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**
    - <img width="596" alt="스크린샷 2023-10-11 오후 12 03 05" src="https://github.com/3n952/aiffel_6/assets/112914475/68d7f7d7-7f18-4d61-9263-e8bb74b862be">
    - ```python
      #train function

        @tf.function
        def train_step(gt, seg):
            with tf.GradientTape() as gene_tape, tf.GradientTape() as disc_tape:
                # Generator 예측
                fake_colored = generator(gt, training=True) # 리뷰어 주석: 여기서 generator에 seg를 넣어야 한다
                # Discriminator 예측
                fake_disc = discriminator(gt, fake_colored, training=True)
                real_disc = discriminator(gt, seg, training=True)
                # Generator 손실 계산
                gene_loss, l1_loss = get_gene_loss(fake_colored, seg, fake_disc)
                gene_total_loss = gene_loss + (100 * l1_loss) ## L1 손실 반영 λ=100
                # Discrminator 손실 계산
                disc_loss = get_disc_loss(fake_disc, real_disc)
            
            gene_gradient = gene_tape.gradient(gene_total_loss, generator.trainable_variables)
            disc_gradient = disc_tape.gradient(disc_loss, discriminator.trainable_variables)
            
            gene_opt.apply_gradients(zip(gene_gradient, generator.trainable_variables))
            disc_opt.apply_gradients(zip(disc_gradient, discriminator.trainable_variables))
            return gene_loss, l1_loss, disc_loss
      ```
    - segmented image를 입력하여 fake image를 생성해야 하는데 ground truth 이미지를 입력으로 넣었다.ㅠㅠ

    
- [ ]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**
    - <img width="635" alt="스크린샷 2023-10-11 오후 12 13 14" src="https://github.com/3n952/aiffel_6/assets/112914475/d61dc231-40e2-47fa-9234-eb3be1c30d6a">
    - data augmentation에서 어떤 작업을 했는지 주석으로 남기면 좋을 것 같다.
- [ ]  **3. 에러가 난 부분을 디버깅하여 문제를 “해결한 기록을 남겼거나” 
”새로운 시도 또는 추가 실험을 수행”해봤나요?**
    - 특별히 없음.
        
- [ ]  **4. 회고를 잘 작성했나요?**
    - ㅇㅇ
        
- [ ]  **5. 코드가 간결하고 효율적인가요?**
    - <img width="435" alt="스크린샷 2023-10-11 오후 12 07 43" src="https://github.com/3n952/aiffel_6/assets/112914475/5c0f5eec-e12d-4a94-8142-73bbe68096aa">
    - constant padding을 넣어서 이미지에 여백이 생겼는데 이 부분이 학습에 영향을 끼치지는 않을까요?
    - <img width="603" alt="스크린샷 2023-10-11 오후 12 11 06" src="https://github.com/3n952/aiffel_6/assets/112914475/fa648e30-1685-408f-8060-a9a6f5b40c40">
    - <img width="672" alt="스크린샷 2023-10-11 오후 12 11 17" src="https://github.com/3n952/aiffel_6/assets/112914475/0e610b9c-3152-433a-a840-165a9580ca46">
    - 사용되지 않는 Encoder, Decoder 클래스가 코드에 남아있다.



# 참고 링크 및 코드 개선
```
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
```

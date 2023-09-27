# AIFFEL Campus Online Code Peer Review Templete
- 코더 : 김산
- 리뷰어 : 서민성


# PRT(Peer Review Template)
- [ ]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**
    - 문제에서 요구하는 최종 결과물이 첨부되었는지 확인
    - 문제를 해결하는 완성된 코드란 프로젝트 루브릭 3개 중 2개,
      - 데이터 전처리, 모델학습, 예측의 전체 과정을 거쳐 캐글 submission까지 전과정이 성공적으로 진행되었는가?
        - 네 전과정이 성공적으로 진행되었습니다 
      - 제출된 노트북이 캐글 커널로 사용될 수 있을 만큼 전처리, 학습, 최적화 진행 과정이 체계적으로 기술되었는가?
        - 네 전처리, 학습, 최적화 진행과정이 체계적으로 기술되어있습니다. 추가적으로 목차가 있었으면 좋겠다는 생각이 있습니다.
      - 다양한 피처 엔지니어링과 하이퍼 파라미터 튜닝 등의 최적화 기법을 통해 캐글 리더보드의 Private score 기준 110000 이하의 점수를 얻었는가?
        - 아니요, score확인 결과 최고 score는 116,130으로 기준에 통과하지는 못했습니다.
        
    퀘스트 문제 요구조건 등을 지칭
        - 해당 조건을 만족하는 코드를 캡쳐해 근거로 첨부
      ![스크린샷 2023-09-27 오후 12 15 55](https://github.com/minsung6333/san/assets/138687269/db30be77-1f86-4c26-9351-5a5758eba05a)
      ![스크린샷 2023-09-27 오후 12 16 26](https://github.com/minsung6333/san/assets/138687269/b044a463-aeb3-41b7-9e0d-c5402951d2f8)


- [ ]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**
    - 해당 코드 블럭에 doc string/annotation이 달려 있는지 확인
    - ![스크린샷 2023-09-27 오후 12 22 07](https://github.com/minsung6333/san/assets/138687269/3479bee5-7466-4cb0-8b84-34f0d3f3119c)
    - 코드 복붙이 안되어서 캡쳐로 대체합니다..ㅠ  

    - 해당 코드가 무슨 기능을 하는지, 왜 그렇게 짜여진건지, 작동 메커니즘이 뭔지 기술.
      - def my_GridSearch(model, train, y, param_grid, verbose=2, n_jobs=5): > my_gridsearch는 다음과 같은 매개변수를 받습니다.
      - grid_model = GridSearchCV(model, param_grid=param_grid, scoring='neg_mean_squared_error', cv=5, verbose=verbose, n_jobs=n_jobs):
        > GridSearchCV 객체를 생성
        > model: 사용할 머신러닝 모델을 전달
        > param_grid: 탐색할 하이퍼파라미터 그리드를 전달
        > scoring: 모델의 성능을 평가할 스코어링 메트릭
        > cv: 교차 검증(Cross-Validation)을 몇 개의 폴드(fold)로 수행할 것인지 지정
        > verbose: 그리드 서치 진행 과정을 출력할 상세도 수준을 지정
        > n_jobs: 병렬 작업을 수행할 CPU 코어 수
      - grid_model.fit(train, y) > 모델을 학습
      - params = grid_model.cv_results_['params'] > 결과값 저장
      - score = grid_model.cv_results_['mean_test_score'] > 결과값 저장
      - results = pd.DataFrame(params) > 데이터 프레임 생성
      - results['score'] = score > 새로운 칼럼 생성
      - results['RMSLE'] = np.sqrt(-1 * results['score']) > RMSLE 값 계산 
      - results = results.sort_values('RMSLE') > 결과값 정렬
      - return results > Results값 반환
        
    - 주석을 보고 코드 이해가 잘 되었는지 확인
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.
        - ![스크린샷 2023-09-27 오후 12 22 07](https://github.com/minsung6333/san/assets/138687269/3479bee5-7466-4cb0-8b84-34f0d3f3119c)
        
- [ ]  **3. 에러가 난 부분을 디버깅하여 문제를 “해결한 기록을 남겼거나” 
”새로운 시도 또는 추가 실험을 수행”해봤나요?**
    - 문제 원인 및 해결 과정을 잘 기록하였는지 확인
      - GridSearch 진행간 각각 모델에 대한 파라미터 적용에 대한 오류가 발생되었던 사실을 구두로 전달 받았고, 해당부분을 해결하는 과정에 대한 기록은 없다고 전달받았습니다.
      - 해당 부분에 대한 기록은 없습니다.
    - 문제에서 요구하는 조건에 더해 추가적으로 수행한 나만의 시도, 
    실험이 기록되어 있는지 확인
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.
        - GridSearch를 위한 다양한 파라미터 값 수정부분이 잘 작성되었고 이를 실험한 과정이 인상깊었습니다.
        ![스크린샷 2023-09-27 오후 12 34 26](https://github.com/minsung6333/san/assets/138687269/8ec81bc6-d708-4e4d-b6c7-6d9673a30ef3)
        ![스크린샷 2023-09-27 오후 12 35 37](https://github.com/minsung6333/san/assets/138687269/3935503b-0826-4c88-a48d-78cc90ac618b)

- [ ]  **4. 회고를 잘 작성했나요?**
    - 주어진 문제를 해결하는 완성된 코드 내지 프로젝트 결과물에 대해
    배운점과 아쉬운점, 느낀점 등이 기록되어 있는지 확인
    - 회고 작성이 잘 되어있었습니다.
    - 전체 코드 실행 플로우를 그래프로 그려서 이해를 돕고 있는지 확인
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.
        - 해당부분이 기입되어있지 않았습니다.
        
- [ ]  **5. 코드가 간결하고 효율적인가요?**
    - 파이썬 스타일 가이드 (PEP8) 를 준수하였는지 확인
      - 파이썬 스타일 가이드를 준수하여 작성되었습니다. 
    - 하드코딩을 하지않고 함수화, 모듈화가 가능한 부분은 함수를 만들거나 클래스로 짰는지
      -AveragingBlending 모듈을 만들어 블랜딩하는 하드코드를 작성하지 않았습니다. 
    - 코드 중복을 최소화하고 범용적으로 사용할 수 있도록 함수화했는지
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.
        - ![스크린샷 2023-09-27 오후 12 39 08](https://github.com/minsung6333/san/assets/138687269/d6ad9ba2-f1be-4a04-847a-d092af12e9d3)

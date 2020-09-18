#2020.09.18
## TIL
단순한 네트워크(MLP)에서 precision 혹은 accuracy가 안나온다면, activation을 변경해라(leaky_relu)
## problem
단순 Binary classification 의 단순 MLP인데 precision은 높고, accuracy가 0로 나와서 왜 그런지 고생
## 상황
1이 20%, 0이 80% 인 문제
## 해결 방법
### network 변경   ( 아래 숫자로 변경 필요)
기본 Input이 2개 이므로 attention으로 변경 ---> 실패 (Attention 확인 필요)

depth 변경(깊게도 얇게도) --> 실패

dropout layer 추가 --> 실패

batch normailztion --> 실패

### 하이퍼 파라미터 변경
lr 변경, 크게도(0.1) 작게도(0.0001) --> 실패

Optimizer 변경 (SGD --> Adam --< Nadm) --> 실패

배치 사이즈 변경 ( 128, 1280,12800) --> 실패

Dense layer 초기화 변경 (GlorotUniform --> GlorotNormal) 실패

activation 변경 (relu --> leaky_relu) :성공
--> 그러나 속도 느림, 그리고 검색해본 결과 tanh 도 괜찬핟고 함. 추후 변경할 예정
reference : stackoverflow에서 본거 같은데 왜 못찾겟지 ㅠㅠ 우선 잠

### 출처

![스크린샷 2024-06-29 오후 7 09 26](https://github.com/Kyeong6/google-ml/assets/100195725/66ee9675-1905-4c55-adee-435dfdac879a)

본 자료는 [Deeplearning.AI](http://Deeplearning.AI)에서 제공한 교육 자료입니다.
<br/></br>
### 1. 신경망이란 무엇인가?

![스크린샷 2024-06-29 오후 7 10 50](https://github.com/Kyeong6/google-ml/assets/100195725/f2b8e768-a2cd-43ad-bdee-8f34191f4fdb)

위 그래프를 보면 **선형회귀**임을 알 수 있고, x축은 집의 크기를 y축은 가격을 의미

x축의 size가 입력(input)으로 사용되어 이를 통해 y축의 가격(output)이 예측
<br/></br>

**어떻게 예측할 수 있는 것인가?**

Input에 뉴런함수가 적용되면 Output이 나오는 구조
<br/></br>

**중간에 존재하는 node는 무엇인가?**

뉴런을 의미하며, 뉴런을 레고블록이라고 생각해보자!

결국 레고블록을 많이 쌓으면 깊은 신경망

참고사항으로 위 파란색 선은 ReLU(활성화함수) 모양

![스크린샷 2024-06-29 오후 7 16 34](https://github.com/Kyeong6/google-ml/assets/100195725/35c21f45-aac0-478e-8af5-26210214def3)

위에서는 x가 하나만 존재하였지만, 해당 예시는 x가 다수 존재하는 경우이다. x가 많아진 만큼 중간에 존재하는 레고블록도 늘어났다. 

노드는 각각 활성화함수(ReLU)가 적용될 수 있으며, 최종적으로 price라는 예측값을 출력한다.

 

![스크린샷 2024-06-29 오후 7 21 20](https://github.com/Kyeong6/google-ml/assets/100195725/f18a8736-f83a-41af-8c41-9f0a4d00f0c6)

x는 모든 뉴런에 대해 연결되기때문에 밀도가 높은 것을 알 수 있다.

x의 입력값과 y라는 결과값을 Train set에 도입시켜 중간에 존재하는 즉, 뉴런이 스스로 family size, workability, school quality를 알아내는 것이다. 

또한 (x, y)에서 x와 y에 대한 충분한 훈련 예제가 주어지면 신경망은 x에서 y까지 정확하게 **매핑하는 함수**를 알아내는데 좋은 성능을 보인다. 
<br/></br>

**궁금한 점**

위의 자료에서는 size + #bedrooms가 첫 번째 뉴런에 접근해서 family size를 도출하는데 실제로는 모든 x가 모든 뉴런에 대해 접근한다. 그렇다면 size와 #bedrooms는 첫 번째 뉴런에 대해 가중치가 높지만, 나머지 zip code, wealth는 가중치가 낮거나 없다는 것인가라는 궁금증이 생겼다. 아무래도 추후 **forward propagation**, **back propagation**을 학습하며 궁금증이 해결될 것이라고 생각한다.

<br/></br>
### 2. 신경망을 사용한 지도학습

![스크린샷 2024-06-29 오후 7 28 09](https://github.com/Kyeong6/google-ml/assets/100195725/33fdb173-0cfd-4813-9551-ee1c841e65f5)

신경망을 통한 많은 가치 차출은 특정 문제에 대해 **무엇이 x이고, 무엇이 y가 되어야하는지 영리하게 선택**하는 것이 중요하다.

또한, 지도학습 구성요소를 시스템에 잘 맞추는 것도 중요하다. 예를 들어, sequential data(순차 데이터)는 RNN(순환 신경망) 기반으로 많이 사용된다.

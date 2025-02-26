### 출처

![Untitled2](https://github.com/Kyeong6/google-ml/assets/100195725/a818aef2-d268-4d20-80e9-e0e27273562e)

본 자료는 [Deeplearning.AI](http://Deeplearning.AI)에서 제공한 교육 자료입니다.

### 이진분류

![Untitled](https://github.com/Kyeong6/google-ml/assets/100195725/5437fb5d-5336-405d-b6ac-636e46900e11)
</br></br>

**해당 강의 목표**

m개의 훈련예제가 있다면, for-loop를 사용하는 게 일반적, 이번 강의를 토해 for-loop를 사용하지 않고 구현하는 법을 배운다.
</br></br>

**Binary Classification**

현재 고양이가 존재하는 이미지에서 1(cat) vs 0(non cat)으로 분류할 수 있다. 

이미지는 RGB라는 3차원으로 표현할 수 있는데, 이걸 벡터화한다면 위에서의 x처럼 표현할 수 있다. 

결국 입력 x는 모든 R,G,B 픽셀로 채운 값을 나열하여서 긴 특징 벡터를 얻을 때까지 계속 진행한다.

최종적으로 vector x의 전체 차원은 `64x64x3`으로 12,288이다. 

이를 `nx=12,288` 로 표현할 수 있다. (입력 특징 벡터의 차원을 나타내기 위해서 소문자 n을 사용)

결국 이진 분류에서의 목표는 특징벡터 x로 표현되는 이미지를 입력할 수 있는 `분류기` 를 배우는 것이다. 

이때 분류란 해당 레이블 y가 1인지 0인지 분류하는 것을 의미한다.(x → y)
</br></br>

**Notation**

![image](https://github.com/Kyeong6/google-ml/assets/100195725/dc56de96-7969-4552-8bb9-24946562e340)

간결한 표기법을 사용하면 행렬 X는 nx개의 특징벡터, m개의 train example이 존재하는 걸로 이해할 수 있다. Excel에서와 같이 행/열을 구조로 생각해보기.

- X.shape = (nx, m)
- Y.shape = (1, m)

![image](https://github.com/Kyeong6/google-ml/assets/100195725/ee16c4fe-0fdf-4427-b3fb-cb3e6b2308b3)
</br></br>

### 로지스틱 회귀

입력 X가 주어졌을 때 model algorithm을 통해 y hat(추정치)를 얻는다

그런데 여기서 $\hat{y}$은 로지스틱 회귀에 맞게 0~1사이에 값(추정치)을 얻어야 한다.   

 $\hat{y} = W^{T}x+b$  은 $\hat{y}$에 관한 식인데 이를 0~1사이로 설정하기 위해 
 </br></br>

 **Sigmoid Function**을 적용

- W, b : 매개변수(매개변수에 관한 상세 정보는 추후 학습)
- X : 입력

![스크린샷 2024-07-01 오후 3 19 09](https://github.com/Kyeong6/google-ml/assets/100195725/016f7b5f-5af4-4971-b09e-42858d08a8b1)

결론적으로 Sigmoid는 0~1사이의 함수이므로, 값이 들어왔을 때 0~1사이의 값을 반환합니다. 이를 통해, **이진 분류**를 할 수 있는 것이다!
</br></br>

**로지스틱 회귀 구현 목표**

매개변수 W, b를 학습하여 $\hat{y}$이 y가 1일 가능성에 대한 좋은 추정치가 되도록 하는 것!

![image](https://github.com/Kyeong6/google-ml/assets/100195725/a0364e26-564c-4efe-9b8e-603e5d7ac0b4)

일반적으로 제곱오차를 로지스틱회귀에서는 사용하지 않는다라는 설명에 대한 이유를 찾아보았다.
</br></br>

### 로지스틱 회귀 비용

**로지스틱 회귀에서 손실함수로 제곱오차 사용 x?**

시그모이드 함수에 비용함수를 평균 제곱오차로 하여 그래프를 그리면 다음과 같은 형태를 얻는다.

![스크린샷 2024-07-01 오후 4 10 31](https://github.com/Kyeong6/google-ml/assets/100195725/620c2f85-494e-40b5-9a17-d415733b5aec)

추후 학습 내용이지만, 경사 하강법을 사용하였을 때, 찾고자하는 최소값이 아닌 잘못된 최솟값을 얻을 수 있는 경우가 존재하기 때문이다. 이때 설명하는 개념이 **Local Minimum**과 **Global Minimum**이다.

해당 경우가 존재하기 때문에 시그모이드를 사용하는 로지스틱 회귀에서의 손실함수로써 적합하지 않다.
</br></br>

**y 값에 따른 y hat 변화**

식을 풀이해보면 알 수 있지만, 최종적으로 얻을 수 있는 결과는 다음과 같다.

- y = 0 → y hat : small
- y = 1 → y hat : large

![image](https://github.com/Kyeong6/google-ml/assets/100195725/6a182601-a38f-4fab-a57b-8415eba24f00)
</br></br>

**Loss function과 Cost function의 차이점**

기존에 공부하였을 때 손실함수(Loss function)과 비용함수(Cost function)에 관한 개념이 헷갈렸다. 

서로 같은 개념인가?라는 생각을 하였지만 이번 강의를 통해 전혀 다른 요소임을 알게 되었다. 
</br></br>

**Loss function(예측 정도 확인)**

단일 훈련 예제에 적용되는 함수로, 얼마나 잘 예측을 하였는 지에 대한 지표라고 할 수 있다.
</br></br>

**Cost function(매개변수 찾기)**

전체 학습 세트의 손실함수의 평균의 수식을 갖는다. 

매개변수의 비용(cost)이므로, 로지스틱 회귀 모델을 훈련할 때 매개변수 W, b를 찾는데 사용되는 함수이다. 

결국, 손실 함수의 결과를 통해 이에 따른 매개변수 W, b가 얼마나 잘 수행되는 지 측정

![image](https://github.com/Kyeong6/google-ml/assets/100195725/c37a039b-a404-4e8c-8a2f-36c1bacf121b)

### 그라데이션 하강

**Gradient descent, 왜 사용할까?**

손실 함수와 비용 함수를 통해서 알게된 점은 결국 손실 함수의 값을 가장 낮게하는 것이 목표이다. 이때 값을 가장 낮게 나오게 하는 파라미터(w,b)를 비용함수를 통해 얻어야 한다. 

비용함수로 어떻게 최소의 값을 나오게 하는 파라미터를 얻을 수 있을까? 이는 Gradient descent, 경사하강법을 통해 얻을 수 있다. 

경사하강법이라는 말 그대로 경사하강, 즉 점점 내려가면서 기울기를 확인하는 것이다.
</br></br>

**초기치 설정**

로지스틱 회귀 같은 경우 거의 모든 초기화(위치 설정) 방법을 사용해도 작동한다. 이는 2차원 평면으로 생각했을 때 로지스틱 회귀는 볼록함수이므로 어느 지점에 위치시켜도 최솟값을 갖는 점으로 이동하기 때문

![image](https://github.com/Kyeong6/google-ml/assets/100195725/10782e4e-a1f2-416e-ba2c-ecb19d5de699)
</br></br>

**경사하강법 수식**

$$
w:= w-{\alpha}\frac{dJ(w)}{dw}
$$

해당 수식을 이용해서 알고리즘이 수렴될 때까지 반복을 진행한다. 

여기서 ${\alpha}$는 **learning rate**를 의미하며 학습 속도, 즉 단계(step) 설정이다. 

해당 수식에서 ${dw}$로 나누었는데 이것을 사용함을 유의하자! 왜냐하면 현재 w를 미분하여 갱신(update)해나가기 때문이다. 

그림을 통해 확인해보면 w가 어디에 위치해있든 ${-}$(minus)를 통해 점점 최소점으로 이동해감을 파악할 수 있다.

- 최소점에서 왼쪽 위치 : 기울기 음수 → w (+) 방향 이동
- 최소점에서 오른쪽 위치 : 기울기 양수 → w (-) 방향 이동
</br></br>

**코드 상 표현**

$$
w:= w-{\alpha}{dw}
$$

여기서 ${dw}$는 도함수를 가지고 있는 변수
</br></br>

### 도함수(파생상품)

![image](https://github.com/Kyeong6/google-ml/assets/100195725/985c52f8-e152-4fc7-9119-eb74343a044a)
</br></br>

**도함수**

도함수의 정의에 대해 단순 공식이 아닌 원리에 대해 고민해보는 내용이였다. 

$$
Slope = {\frac{height}{width}} = {\frac{y의 변화량}{x의 변화량}}={\frac{df(a)}{da}}={\frac{d}{da}fa}
$$

도함수는 무한정으로 작은 값의 이동으로 정의할 수 있다. 
</br></br>

**딥러닝 같은 경우에는 어떻게 사용될까?**

**경사 하강법**에서 매개변수 w를 좌/우측으로 이동함에 따라 기울기가 변함을 알 수 있는데, 이를 통해 최종적으로 최소의 점을 파악 가능하다. 
</br></br>

### 더 많은 도함수 예제

![image](https://github.com/Kyeong6/google-ml/assets/100195725/243b461d-7207-4b48-ab4a-14aa23b5f3ca)

$f(x)$가 어떤 형태이든지 $x$가 이동하면 $f(x)$가 **얼마만큼** 이동(상승 및 하강)할 것으로 예상되느냐에서 파악할 수 있다. 이때의 **얼마만큼**이 곧, **기울기**라고 할 수 있다.
</br></br>

### 계산 그래프 및 계산그래프가 포함된 도함수

![image](https://github.com/Kyeong6/google-ml/assets/100195725/9ce5753e-03bf-4d79-b8c3-3e463ab16db6)
</br></br>

**Back propagation(역전파)**

위의 식을 일반화하여 생각해보면 다음과 같다. 

입력층에 들어온 입력값을 **순전파**하여 예측값을 도출하는 과정을 진행한다. 

이때 발생한 오차에 관해서 **역전파**를 통해 가중치를 업데이트한다. 

이번 강의에서는 역전파 과정에서 영향을 주는 것을  표현하기 위해서 위와 같은 예제를 통해 설명한다. 
</br></br>

**예제 설명**

${\frac{dJ}{da}}$는 다음과 같이 풀어서 파악할 수 있다. 

$$
{\frac{dJ}{da}} = {\frac{dJ}{dv}} {\frac{dv}{da}} = {da}
$$

위의 식은 미적분에 **연쇄법칙**이 적용된 예이다.

**역전파**를 구현할 때, 일반적으로 **최종출력변수**가 존재하는데 위의 경우에서는 J이다.

J는 v에 변화량에 영향을 받고, v는 a의 변화량에 영향을 받는다라고 생각할 수 있다. 

결국, 위의 식은 a가 변함에 따라 J가 얼마나 변하냐?라고 이해할 수 있는데, v가 매개체가 되어서 파악할 수 있다. 

![image](https://github.com/Kyeong6/google-ml/assets/100195725/a46a3ed6-9a15-4d69-9175-34b541896b25)
</br></br>

**결론**

위의 예제와 동일한 방식으로 b,c,u 또한 알 수 있다. 

정리해보자면 위의 예제를 통해 중간 변수들의 도함수를 파악(역전파 방식)할 수 있는데, 원리는 어떤 것이 영향을 끼쳐서 최종값이 나오는지를 토대로 파악할 수 있다. 
</br></br>

### 로지스틱 회귀 그라데이션 하강

![image](https://github.com/Kyeong6/google-ml/assets/100195725/89acc600-f9d1-4eb7-b472-888774e3c68d)

![image](https://github.com/Kyeong6/google-ml/assets/100195725/1aedb0a7-1ffd-4f54-afae-8292ac2f3db0)

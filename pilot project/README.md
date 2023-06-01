## 스터디 개요

###  Image-Text representation study (based on CLIP and prefix-tuning)

### 연구 동기
이미지 캡셔닝 모델 중 clipcap 모델을 기반으로 연구하게 된 동기

- 최근에 뛰어난 성능을 보이는 거대 모델이 화제가 되고 있는데, 데이터와 자원에 의존적이라는 한계점이 뚜렷한 상황
- 특히 이미지캡셔닝 task는 많은 모델이 지도학습을 기반으로 훈련을 시키기 때문에 labeled data가 많이 필요해서, data dependency가 큰 경향이 있다.
- 또한, 이미지캡셔닝의 성능을 위해서는 적절한 text generation 전략이 필요하다.

- Clipcap이 이에 착안하여 적은 데이터와 한정된 자원으로도 좋은 성능을 낼 수 있는 모델이라는 것을 알게됨

그래서, ClipCap을 이미지 캡셔닝 연구 모델로 삼아서 contribution을 찾아보고자 하여 연구를 진행하게 되었다.

### ClipCap Architecture

![image](https://github.com/dhye1/ETRI-research_intern/assets/96327142/809d9f46-9ab0-42cf-8d5c-7dcc826d4378)


### CLIP

![image](https://github.com/dhye1/ETRI-research_intern/assets/96327142/2308df1b-2d4b-4176-8d86-398dcf80a5c4)
![image](https://github.com/dhye1/ETRI-research_intern/assets/96327142/62ea046e-683d-4fb5-a2f9-954627cba3a5)

### Prefix-tuning
![image](https://github.com/dhye1/ETRI-research_intern/assets/96327142/25ef673e-297a-4380-963f-9fb7ed84358d)


### 연구 내용 : ‘Prefix 길이에 따른 이미지 캡셔닝 성능 분석’

- Clipcap모델이 prefix tuning을 시도한 이유
  - prefix를 생성하기 위한 mlp만 최적화시키고, clip과 gpt2는 추가 Fine-tuning을 하지 않고도 좋은 성능을 보였기 때문
- 논문에서는 prefix의 길이가 증가할 수록 많은 양의 정보가 담겨있다고 함
- But, 저자들이 참고했다고 한 prefix-tuning 논문의 실험결과를 보면, prefix길이가 증가한다고 무조건 좋은 성능을 내는 것은 아님
- 따라서 ClipCap 에서 prefix 길이를 조정하여 성능 비교하고, 결론을 도출 해보고자 함

![image](https://github.com/dhye1/ETRI-research_intern/assets/96327142/e8c2a841-6582-4447-9e28-91e564d58210)

### Experiments
기본 실험 세팅 및 데이터는 ClipCap 논문과 동일

- jupyter 가상환경에서 MSCOCO dataset으로 multi layer perceptron optimizing 
  - GPU 환경이 요구되어 연구실 내 서버 활용

- ClipCap에서 사용하는 패키지를 설치하고 CLIP과, GPT2 모델을 불러온다.
- prefix length = 1, 10, 20 으로 설정하여 학습 진행
- 각각의 prefix length에 대해, 학습 과정에서 저장된 prefix.pt를 불러와서 추론 진행 




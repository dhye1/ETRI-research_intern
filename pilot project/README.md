## 스터디 개요

##  Image-Text representation study (based on CLIP and prefix-tuning)
<br/>

### 연구 동기
이미지 캡셔닝 모델 중 clipcap 모델을 기반으로 연구하게 된 동기

- 최근에 뛰어난 성능을 보이는 거대 모델이 화제가 되고 있는데, 데이터와 자원에 의존적이라는 한계점이 뚜렷한 상황
- 특히 이미지캡셔닝 task는 많은 모델이 지도학습을 기반으로 훈련을 시키기 때문에 labeled data가 많이 필요해서, data dependency가 큰 경향이 있다.
- 또한, 이미지캡셔닝의 성능을 위해서는 적절한 text generation 전략이 필요하다.

- Clipcap이 이에 착안하여 적은 데이터와 한정된 자원으로도 좋은 성능을 낼 수 있는 모델이라는 것을 알게됨

그래서, ClipCap을 이미지 캡셔닝 연구 모델로 삼아서 contribution을 찾아보고자 하여 연구를 진행하게 되었다.

<br/>

### ClipCap Architecture

![image](https://github.com/dhye1/ETRI-research_intern/assets/96327142/5bac44a9-ed71-4a66-b005-f35e984ac946)

<br/>

### CLIP
![image](https://github.com/dhye1/ETRI-research_intern/assets/96327142/0e45018d-ae70-4f34-8607-bad08e537a3a)
![image](https://github.com/dhye1/ETRI-research_intern/assets/96327142/ff941f0d-8d74-409c-b6e8-f871d9ba60c5)

<br/>

### Prefix-tuning
![image](https://github.com/dhye1/ETRI-research_intern/assets/96327142/3ab75586-54b2-44e7-9b12-cecc84ccf046)

<br/>

### 연구 내용 : ‘Prefix 길이에 따른 이미지 캡셔닝 성능 분석’

- Clipcap모델이 prefix tuning을 시도한 이유
  - prefix를 생성하기 위한 mlp만 최적화시키고, clip과 gpt2는 추가 Fine-tuning을 하지 않고도 좋은 성능을 보였기 때문 <br/>
  
- 논문에서는 prefix의 길이가 증가할 수록 많은 양의 정보가 담겨있다고 함
- But, 저자들이 참고했다고 한 prefix-tuning 논문의 실험결과를 보면, prefix길이가 증가한다고 무조건 좋은 성능을 내는 것은 아님
- 따라서 ClipCap 에서 prefix 길이를 조정하여 성능 비교하고, 결론을 도출 해보고자 함

![image](https://github.com/dhye1/ETRI-research_intern/assets/96327142/d80221a4-c50a-4a12-a553-24a08a6f1853)


### Experiments
기본 실험 세팅 및 데이터는 ClipCap 논문과 동일

- jupyter 가상환경에서 MSCOCO dataset으로 multi layer perceptron optimizing 
  - GPU 환경이 요구되어 연구실 내 서버 활용
  
- ClipCap에서 사용하는 패키지를 설치하고 CLIP과, GPT2 모델을 불러온다.
- prefix length = 1, 10, 20 으로 설정하여 학습 진행
![image](https://github.com/dhye1/ETRI-research_intern/assets/96327142/7f02710a-cb44-44d2-9c5a-91311cc91228)

(해당 코드를 터미널 환경에서 실행하여 학습)
- 각각의 prefix length에 대해, 학습 과정에서 저장된 prefix.pt를 불러와서 추론 진행 
<br/>

### Results
![image](https://github.com/dhye1/ETRI-research_intern/assets/96327142/e72b5095-e32e-4bcc-aa2f-db1c00c2785f)

- prefix length 별 BLEU score 확인 결과, 길이가 증가할 수록 점수가 올라가는 경향성 보인다.
- BLEU score1과 4 기준 length=10 일 때 length=20 일 때 보다 미세하게 높음
<br/>

![image](https://github.com/dhye1/ETRI-research_intern/assets/96327142/a23e97e9-7dfd-4c42-8248-d758845ca15e)

- prefix 길이가 증가하면 캡셔닝 성능이 좋아지는 경향성이 있지만, 모든 경우에서 더 좋은 것은 아님
- 길이를 증가하는게 모델 성능을 개선할 수 있는 최적의 방법은 아니라는 것을 알 수 있음
<br/>

### 연구방향 구체화
- ClipCap에서 제시한 prefix-tuning 방법 외에도,  decoding 성능을 개선할 수 있는 방법에 대한 연구를 찾아보고자 함
- 적절한 decoding method에 대한 연구 (Text generation model & decoding methods)
- zero-shot 에 강한 representation을 활용한 연구 (CLIP)
- prompt-based learning 외에도 효율적인 학습을 위한 Parameter-Efficient Learning 방법




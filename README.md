## ETRI 인턴 연구일지 및 멀티모달 파일럿 프로젝트 (23.01~23.03)

etri 언어지능연구실에서 연구인턴을 하면서 배운 연구일지, 관련해서 수행한 파일럿 프로젝트 기록
### 수행 내용


- 이미지캡셔닝 관련 SOTA 모델 searching (01.16 ~ 01.27)
  - 다양한 decoding methods 관련 공부
  - 현재 low resource 환경에서의 제로샷 캡셔닝 연구도 활발히 진행되고 있음 [[관련 논문 정리]](https://velog.io/@hyeda/%EB%85%BC%EB%AC%B8-%EB%A6%AC%EB%B7%B0-Language-Models-Can-See-Plugging-Visual-Controls-in-Text-Generation#unsupervised-approaches-zerocap) <br/>
  
- 한국어 캡션 데이터 구축 (01.03 ~ 01.27) <br/>

- ClipCap 논문 리뷰 (01.23 ~ 01.27)
  - ClipCap 은 CLIP과 GPT2를 freeze하고, 두 모달을 연결시켜주는 MLP의 파라미터를 update 하는 과정에서 더 나은 prefix를 생성하는 방법으로 학습을 진행함 

  - What is prefix-tuning? 
    - ["prompt-based learning" 방법론 공부](https://velog.io/@hyeda/About-prompt-learning)

- ClipCap 추가 연구 진행 (02.01 ~)

### 연구 동기
  - 논문에서는 prefix-tuning을 기반으로 text decoding을 진행한다.
  - 저자들이 참고한 prefix-tuning 논문의 실험결과를 보았을 때, prefix길이가 증가한다고 무조건 좋은 성능을 내는 것은 아니라는 것을 알게 됨
  - 1)학습에 너무 많은 학습시간 소요, 2) overfitting 가능성
  - prefix 길이 별 performance 분석을 진행해보고자 함 
  
### 연구 내용
- [[pilot project]](https://github.com/dhye1/ETRI-research_intern/tree/main/pilot%20project)
- 앞으로 진행해보고 싶은 연구
  - MAGIC, ConZIC 등 최근 캡셔닝모델이 제안한 제로샷 디코딩 방법
  - prompt-based learning 외에도 효율적인 학습을 위한 Parameter-Efficient Learning 방법들

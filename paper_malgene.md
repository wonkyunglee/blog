# Paper Review

## MalGene: Automatic Extraction of Malware Analysis Evasion Signature
Conference : ACM-CCS 2017

### Keyword
Computer security, malware analysis, evasive malware, sequence alignment, bioinformatics

### Abstract
Automative dynamic malware analysis 로는 evasive malware (숨기는 멀웨어) 를 잡기가 힘들다. 최근에 자동으로 이를 잡기 위한 연구들이 생겼는데, 아이디어는 다음과 같다. 여러 analysis environment 를 구성하고 그 곳들에서의 멀웨어의 다양한 행동들을 비교하면서 분석하는 것이다. 엄청 다른 행동이 발견되면 이건 evasive malware 라고 판단하다. 하지만 이 시스템의 단점은, 멀웨어 분석가가 이런 evasion 기법을 이해하기 위해 다시 분석을 또 해야한다는 것이다. 또 다른 툴들이 이런 과정을 돕는데 사용되는데 보통 추가적인 정보를 담은 manual한 여러 인풋들이 요구된다. 그리고 resource-intensive 하고 not scalable 하다.
이 페이퍼에서는 자동으로 evation signatures 를 뽑아주는 MalGene 이라는 걸 소개한다. 시스템 콜 시퀀스에 있는 evasive behavior 를 자동으로 찾는 bioinformatics 에서 영감을 받은 알고리즘이다. evasion 에 사용되는 데이터 비교 이벤트와 콜 이벤트 확인을 위해 데이터 플로우 분석과 데이터 마이닝 기술이 사용되었다. 그리고 evasive 방법에 따라 멀웨어 샘플들을 클러스터링하였다. 총 2810 개의 evasive samples 를 78개의 비슷한 Evasion 기술 들로 묶었다.



### 중요도
Mendeley Readers : 21

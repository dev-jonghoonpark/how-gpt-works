# How GPT Works

**GPT는 어떻게 다음 단어를 고르는가** — 토큰 하나가 벡터가 되어 어텐션과 MLP를 96번 지나고 확률 분포가 되어 나오기까지, GPT 한 모델을 입력에서 출력까지 따라가며 브라우저에서 직접 실험하는 인터랙티브 교육 자료입니다. 3Blue1Brown 딥러닝 시리즈 5~7장을 정리했습니다.

🔗 **[데모 바로가기](https://dev-jonghoonpark.github.io/how-gpt-works/)**

| 편 | 영상 | 다루는 부분 |
| --- | --- | --- |
| DL5 | [트랜스포머, ChatGPT가 트랜스포머로 만들어졌죠.](https://www.youtube.com/watch?v=g38aoGttLhI) | 전체 흐름, 임베딩, 언임베딩, 소프트맥스 |
| DL6 | [그 이름도 유명한 어텐션, 이 영상만 보면 이해 완료!](https://www.youtube.com/watch?v=_Z3rXeJahMs) | Q·K·V, 마스킹, 멀티헤드 |
| DL7 | [수많은 정보는 LLM 모델 속 어디에 저장되어있는걸까?](https://www.youtube.com/watch?v=zHQLPJ8-9Qc) | MLP, 사실의 저장, 중첩 |

## 다루는 내용

1. **다음 토큰 하나만 맞히면 된다** · GPT라는 이름, 확률 분포에서 뽑아 이어 붙이는 생성, 시스템 프롬프트
2. **단어는 벡터, 의미는 방향** · 딥러닝의 형식(실수 배열 + 행렬 곱), 임베딩 행렬, king − man + woman ≈ queen, 내적, 컨텍스트 길이
3. **마지막 벡터에서 확률로** · 언임베딩과 로짓, 학습 땐 모든 위치가 동시에 예측한다는 점, 소프트맥스와 온도
4. **어텐션 — 질문(Q)과 견출지(K)** · 문맥에 따라 달라지는 뜻(mole, tower), Q·K 내적과 어텐션 맵, √d<sub>k</sub>, −∞ 인과 마스킹, 맵 크기 = 컨텍스트²
5. **Value와 멀티헤드** · Δe를 더해 벡터 옮기기, 저랭크 Value 분해(V↓·V↑ = 출력 행렬), 96헤드, 셀프 vs 크로스 어텐션, 어텐션 파라미터 580억
6. **MLP — 사실을 꺼내는 AND 게이트** · "Michael Jordan plays ___", W↑의 행 = 질문, 바이어스와 ReLU/GELU, W↓의 열 = 방향, MLP 파라미터 1,160억
7. **중첩(superposition)** · 거의 직교하는 방향, 존슨–린덴스트라우스, 웰치 경계로 바로잡은 영상의 89°~91° 주장, 희소 오토인코더
8. **1,750억을 끝까지 세기** · 세 편에 흩어진 계산을 모은 GPT-3 파라미터 표

## 인터랙티브 데모 9종

| 데모 | 무엇을 확인하나 |
| --- | --- |
| 한 토큰씩 생성하기 | 분포에서 뽑아 이어 붙이는 자기회귀 생성, 온도에 따른 변화 (바이그램 장난감 모델) |
| 벡터 산술 A − B + C | 2D 장난감 임베딩에서 왕 − 남자 + 여자 ≈ 여왕, 차이 벡터와 최근접 단어 |
| 내적의 부호 | 벡터를 끌어 돌리며 보는 a·b, 각도, cos θ |
| 소프트맥스와 온도 | 로짓 5개와 T를 조절하며 e<sup>x/T</sup> → 정규화 과정을 표로 확인 |
| 어텐션 맵 | "a fluffy blue creature roamed the verdant forest"의 4가지 헤드, 마스킹을 끄면 미래 토큰을 베끼는 헤드 |
| Δe 따라가기 | creature 벡터가 옮겨 가는 경로, 헤드 1개는 가중치를 나눠 갖고 헤드 2개는 각자 전부를 주는 차이 |
| 뉴런 네 개짜리 MLP | Michael Jordan → 농구. 바이어스를 올리면 OR 게이트가 되고, 활성화를 끄면 다른 방향을 빼 버리는 것 |
| 랜덤 벡터의 각도 분포 | d = 2 → 1000에서 90° 근처로 몰리는 각도, 최악의 쌍을 웰치 한계까지 밀어내기 |
| 파라미터 계산기 | GPT-3 프리셋에서 175,181,291,520개와 행렬 27,938개 재현, GPT-2 프리셋 비교 |

여기에 이해도 확인 퀴즈 9문항이 포함되어 있습니다.

## 사용 방법

별도 설치 없이 [데모 페이지](https://dev-jonghoonpark.github.io/how-gpt-works/)를 열면 됩니다. 로컬에서 보려면 `index.html` 파일 하나만 열면 됩니다. 외부 의존성이 전혀 없습니다.

## 출처와 참고

이 자료는 3Blue1Brown 딥러닝 시리즈 Chapter 5~7의 한국어 채널 버전이 다루는 개념과 설명 순서를 따라 본문을 정리하고, 데모는 한국어 학습용으로 새로 만든 것입니다. 데모의 단어 좌표와 가중치는 개념을 보여 주려고 손으로 정한 값이며 실제 모델에서 가져온 값이 아닙니다. 영상도 함께 보시길 권합니다.

주요 참고 문헌은 페이지 하단에 정리되어 있습니다. Vaswani 등(2017), Radford 등(2019), Brown 등(2020), Mikolov 등(2013), Hendrycks & Gimpel(2016), Geva 등(2021), Nanda 등(2023), Johnson & Lindenstrauss(1984), Elhage 등(2022), Bricken 등(2023).

## 관련 자료

[how-ai-works](https://github.com/dev-jonghoonpark/how-ai-works) 시리즈의 일부입니다.

- [How word2vec Works](https://dev-jonghoonpark.github.io/how-word2vec-works/) — 임베딩의 벡터 산술이 어떻게 학습되는지
- [How Attention Works](https://dev-jonghoonpark.github.io/how-attention-works/) — Q·K·V와 멀티헤드를 더 깊이
- [How Transformer Works](https://dev-jonghoonpark.github.io/how-transformer-works/) — 원 논문의 인코더–디코더 구조와 학습 레시피

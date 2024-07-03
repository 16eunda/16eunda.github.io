---
layout: post
title: openLLM(KoAlpaca)에 제주도 사투리 학습2
date: 2024-05-08 16:40
category: sample
typora-root-url: ../
---



## 학습하기 코드를 수정하기

이전의 코드는 1epoch의 학습을 진행한 것이 아니다.

아래 링크를 통해서 trainer의 옵션을 조정하여 적절하게 epoch를 선정한다.

[https://huggingface.co/docs/transformers/main_classes/trainer](https://huggingface.co/docs/transformers/main_classes/trainer)



---



#### :warning:주의사항+옵션설명:warning:

- save_step = logging_step : 꼭 두개의 값을 동일하게 해야 오류가 생기지 않는다.
  - 이유: save_step은 eval 결과에서 오버피팅이 일어나기전 가장 작은 loss값을 만드는 값을 저장해 놓는다.
    logging_step은  

- save_total_limit=10000 -> 너무 적게 하면 선입선출로 기록해야할 데이터가 삭제되는 우려가 있으므로 적적한 값 선택!

- ouput_dir = "answer" -> 최종적인 값을 'answer'라는 디렉토리에 답을 저장 -> 'answer' 말고 날짜 넣으면 관리에 도움

- repo_어쩌고 -> 





## 점수 비교

미세조정한 효과를 확실하게 느끼기 위해서 우리가 전처리한 데이터셋으로 미세조정한 모델, 미세조정을 안한 모델, 그리고 gpt-3.5의 답변을 비교하여 점수를 비교한다.

- 미세조정 안한 모델 vs 미세조정 후 모델 vs gpt-3.5

-  test 데이터에 있는 데이터 중 100개를 선정하여 test에 사용

- 100개의 사투리를 각 3개의 모델에게 번역지시

- 답변한 정답을 json 파일로 저장

- 답변한 파일을 gpt-4.0(뤼튼)에 적용하고 적절한 프롬프트를 작성하여 3개의 보델 중 가장 적합하게 번역을 한 모델을 선택하도록 하여 점수를 매길 수 있도록 한다.

- 각 점수의 비율을 비교하여 미세조정 후 모델의 정답률(win_rate)이 다른 모델과 비교했을 때 높은 점수를 내는지 확인

  

## 논문 작성

gpt-4":win_rate 점수 계산
서론: 문단당 7~중 정도, 중요한 근거, 사실을 참고 문언을 추가한다.

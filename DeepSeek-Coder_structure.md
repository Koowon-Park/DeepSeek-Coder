# DeepSeek-Coder 레포지토리 구조 및 개요

## 1. 프로젝트 개요

- **DeepSeek Coder**는 다양한 크기(1B, 5.7B, 6.7B, 33B)의 코드 생성/완성 AI 모델을 제공합니다.
- HumanEval, MultiPL-E, MBPP, DS-1000, APPS 등 코드 벤치마크에서 최상위권 성능을 목표로 하며, 16K 토큰까지의 project-level 코드 완성(infilling) 기능을 지원합니다.
- 80개 이상의 프로그래밍 언어를 지원합니다.

---

## 2. 주요 디렉터리 및 파일

- **README.md**  
  프로젝트의 전반적인 소개, 사용법, 파인튜닝, Q&A, 지원 언어 등에 대한 설명이 있습니다.

- **demo/**
  - `app.py`: Gradio 기반 데모 앱 코드
  - `requirement.txt`: 데모 실행에 필요한 패키지 목록
  - `style.css`: 간단한 UI 스타일

- **finetune/**
  - `finetune_deepseekcoder.py`: DeepSeek Coder 모델의 파인튜닝 스크립트
  - `README.md`: 파인튜닝 방법 및 하이퍼파라미터 설명
  - `requirements.txt`: 파인튜닝에 필요한 패키지 목록

- **Evaluation/**
  코드 생성 모델 평가용 스크립트 및 벤치마크별(DS-1000, HumanEval, MBPP, PAL-Math) README 파일  
  - 각 벤치마크마다 `README.md`에 설치 방법, 평가 스크립트, 실험 결과 등이 정리되어 있음

- **pictures/**  
  로고 이미지 등 프로젝트 소개에 쓰이는 이미지

- **configs/**  
  (상세 내용은 미확인) DeepSpeed 등 훈련/실행을 위한 config 파일로 추정

---

## 3. 주요 특징 및 사용법

- **모델 사용 예시**  
  Huggingface Transformers 라이브러리를 활용하여 간단하게 모델을 불러와 inference 가능  
  ```python
  from transformers import AutoTokenizer, AutoModelForCausalLM
  tokenizer = AutoTokenizer.from_pretrained("deepseek-ai/deepseek-coder-6.7b-instruct", trust_remote_code=True)
  model = AutoModelForCausalLM.from_pretrained("deepseek-ai/deepseek-coder-6.7b-instruct", ...)
  # 코드 생성 inference
  ```

- **파인튜닝 및 평가**  
  - `finetune/finetune_deepseekcoder.py` 및 `Evaluation/` 디렉터리의 스크립트를 통해 사용자 데이터셋에 맞춰 파인튜닝/성능 평가 가능
  - 파인튜닝은 DeepSpeed 지원

- **Q&A 및 고급 설정**  
  - tokenizer 및 양자화(quantization) 관련 FAQ
  - 다양한 벤치마크, 실험 결과 표 제공

---

## 4. 지원 언어 (일부)

Python, C++, Java, PHP, TypeScript, C#, Bash, JavaScript 등 다수

---

## 5. 의존성 예시

- 데모용: `accelerate`, `bitsandbytes`, `gradio`, `protobuf`, `scipy`, `sentencepiece`, `torch`, `transformers`
- 파인튜닝용: `deepspeed` 등

---

## 참고 사항

- 최상위 README에서 전체적인 프로젝트 특징, 구조, 활용법을 확인할 수 있음
- 각 벤치마크 및 파인튜닝, 데모 관련 디렉터리 별로 README와 스크립트가 잘 분리되어 있음
- configs, scripts, checkpoints 등 추가 디렉터리는 실제 레포를 확인하며 세부 구조 파악 필요

---

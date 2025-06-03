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

# DeepSeek-Coder 주요 폴더/파일별 설명

아래는 `deepseek-ai/DeepSeek-Coder` 레포지토리의 주요 폴더 및 파일에 대한 설명입니다.

---

## 📂 Root (최상위)

- [.gitignore](https://github.com/deepseek-ai/DeepSeek-Coder/blob/main/.gitignore):  
  Git에서 추적하지 않을 파일/폴더 패턴 목록.

- [LICENSE-CODE](https://github.com/deepseek-ai/DeepSeek-Coder/blob/main/LICENSE-CODE):  
  코드에 대한 라이선스 명시.

- [LICENSE-MODEL](https://github.com/deepseek-ai/DeepSeek-Coder/blob/main/LICENSE-MODEL):  
  모델에 대한 라이선스 명시.

- [README.md](https://github.com/deepseek-ai/DeepSeek-Coder/blob/main/README.md):  
  프로젝트 개요, 특징, 사용법, 파인튜닝, FAQ 등 문서.

- [requirements.txt](https://github.com/deepseek-ai/DeepSeek-Coder/blob/main/requirements.txt):  
  프로젝트(혹은 기본 환경)에 필요한 파이썬 패키지 목록.

---

## 📂 Evaluation

- [DS-1000](https://github.com/deepseek-ai/DeepSeek-Coder/tree/main/Evaluation/DS-1000)
- [HumanEval](https://github.com/deepseek-ai/DeepSeek-Coder/tree/main/Evaluation/HumanEval)
- [LeetCode](https://github.com/deepseek-ai/DeepSeek-Coder/tree/main/Evaluation/LeetCode)
- [MBPP](https://github.com/deepseek-ai/DeepSeek-Coder/tree/main/Evaluation/MBPP)
- [PAL-Math](https://github.com/deepseek-ai/DeepSeek-Coder/tree/main/Evaluation/PAL-Math)

> 다양한 코드 벤치마크 평가용 스크립트와 데이터/설정이 들어 있습니다.  
> 각 폴더는 해당 벤치마크의 세부적인 평가 방법, 결과, 실행 스크립트 등을 포함합니다.

---

## 📂 demo

- [app.py](https://github.com/deepseek-ai/DeepSeek-Coder/blob/main/demo/app.py):  
  Gradio 기반 웹 데모 앱 실행 코드.

- [requirement.txt](https://github.com/deepseek-ai/DeepSeek-Coder/blob/main/demo/requirement.txt):  
  데모 실행에 필요한 파이썬 패키지 목록.

- [style.css](https://github.com/deepseek-ai/DeepSeek-Coder/blob/main/demo/style.css):  
  데모 웹 UI 스타일.

---

## 📂 finetune

- [README.md](https://github.com/deepseek-ai/DeepSeek-Coder/blob/main/finetune/README.md):  
  DeepSeek Coder 모델 파인튜닝 방법 안내.

- [finetune_deepseekcoder.py](https://github.com/deepseek-ai/DeepSeek-Coder/blob/main/finetune/finetune_deepseekcoder.py):  
  파인튜닝 스크립트.

- [requirements.txt](https://github.com/deepseek-ai/DeepSeek-Coder/blob/main/finetune/requirements.txt):  
  파인튜닝에 필요한 패키지 목록.

- [configs](https://github.com/deepseek-ai/DeepSeek-Coder/tree/main/finetune/configs):  
  DeepSpeed 등 파인튜닝/훈련을 위한 설정 파일 디렉터리.

---

## 📂 pictures

> 프로젝트 및 문서에 사용되는 이미지/로고/시각화 결과 등이 저장되어 있습니다.
> (폴더 내 전체 파일 목록은 [GitHub에서 확인](https://github.com/deepseek-ai/DeepSeek-Coder/tree/main/pictures)하세요.)

- [logo.png](https://github.com/deepseek-ai/DeepSeek-Coder/blob/main/pictures/logo.png):  
  프로젝트 로고
- [result.png](https://github.com/deepseek-ai/DeepSeek-Coder/blob/main/pictures/result.png):  
  성능 결과 시각화
- [HumanEval.png](https://github.com/deepseek-ai/DeepSeek-Coder/blob/main/pictures/HumanEval.png):  
  벤치마크 관련 이미지
- 기타 다양한 벤치마크/모델 시각화 이미지 다수

---

> **참고:**  
> - 위 설명은 각 폴더/파일의 표준적 역할 및 네이밍을 기반으로 작성되었습니다.  
> - 일부 폴더(특히 `/pictures`)는 파일이 많으니, 전체 내용은 [GitHub 페이지](https://github.com/deepseek-ai/DeepSeek-Coder/tree/main/pictures)에서 직접 확인 가능합니다.

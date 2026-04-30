# Bitmate Team Project - STT · LLM · TTS

저희는 평소 사람과의 대화를 당연하게 여기며 살아갑니다.  
하지만 질병이나 사고로 목소리를 잃게 되면, 더 이상 대화를 이어갈 수 없게 됩니다.

이러한 문제를 해결하기 위한 시도는 이전에도 있었습니다.  
예를 들어, Stephen Hawking은 음성 합성 장치를 통해 소통을 이어갔고,  
Val Kilmer 역시 AI 기술로 자신의 목소리를 복원했습니다.

하지만 기존 기술은 단순한 음성 출력에 그쳐,  
개인의 말투나 감정까지 자연스럽게 전달하는 데에는 한계가 있었습니다.

저희는 이 문제에서 출발해,  
**“그 사람의 목소리로 실제 대화하듯 소통하는 방법”**을 만들고자 합니다.

---

## Overview

이 프로젝트는 음성을 텍스트로 변환(STT)하고,  
LLM을 통해 자연스러운 답변을 생성한 뒤,  
이를 개인의 목소리로 다시 들려주는(TTS) 음성 대화 시스템입니다.

특히 사용자의 음성을 학습(fine-tuning)하여  
**개인화된 음성 대화 경험**을 제공하는 것을 목표로 합니다.

---

## Pipeline

<p align="center">
  <img src="https://github.com/user-attachments/assets/4dfd0257-2689-45ed-8384-033a6be6913a" width="80%" />
</p>

---

## Models

### STT (Speech-to-Text)

- Whisper (large-v3-turbo)
- 다양한 환경에서 안정적인 음성 인식 성능
- 빠른 추론 속도와 높은 정확도
- 실시간 대화 서비스에 적합

---

### LLM (Large Language Model)

**기존: Qwen 2.5 7B**
- 경량 모델 대비 우수한 성능
- 다국어 특성으로 중국어 출력 문제 발생

**개선: DNA-2.0-14B**
- Instruction Tuning 및 Alignment 강화
- 사용자 의도 이해 향상
- 한국어 출력 안정성 개선

**Trade-off**
- 모델 크기 증가 → 로딩 시간 증가

---

### TTS (Text-to-Speech)

- Qwen3-TTS
- 자연스러운 음성 생성
- 사용자 음성 기반 fine-tuning 지원
  - 발음, 억양, 말투 반영
- Qwen 계열로 LLM과 높은 호환성

**Trade-off**
- 고품질 음성을 위한 연산량 증가

---

## Features

- STT: 음성 → 텍스트 변환
- LLM: 자연스러운 대화 생성
- TTS: 사용자 음성 기반 음성 합성
- Fine-tuning: 개인 음성 학습

---

## Demo

<p align="center">
  <img src="https://github.com/user-attachments/assets/215d413d-c0de-4461-b678-8bc6f9e8cdb7" width="45%" />
  <img src="https://github.com/user-attachments/assets/8bba7b00-bc40-4f23-821f-f65cd4c6bb9b" width="45%" />
</p>

---

## Usage

1. 음성 데이터 수집 (`raw`)
2. 전처리 및 wav 변환
3. metadata 작성
4. TTS 모델 fine-tuning
5. STT → LLM → TTS 실행
```
data/
└── dataset/
    └── wav_{name}/
        ├── raw/          # 원본 녹음 파일 (m4a, wav 등)
        ├── wav/          # 전처리된 wav 파일
        ├── metadata.txt  # audio_001.wav|텍스트 형식
        └── ref.wav       # 대표 음성 (reference)
```

---

## Troubleshooting

### 1. 다국어 오인식 문제

**문제**
- 한국어 입력 → 중국어 인식/응답 발생

**원인**
- STT: 노이즈 및 마이크 환경
- LLM: 다국어 모델 특성

**해결**
- STT: 한국어 인식 제한
- LLM: 한국어 외 출력 제한 + 한자 필터
- 모델 교체 (Alignment 강화)

→ 출력 언어 일관성 개선

---

### 2. 메모리 부족 (OOM)

**문제**
- STT + LLM + TTS 동시 실행 시 VRAM 부족

**해결**
- LLM 4bit 양자화 적용

→ 메모리 사용량 감소 및 안정화

---

## Goal

단순한 음성 기록을 넘어,  
**사용자의 목소리로 계속 대화할 수 있는 경험**을 제공합니다.

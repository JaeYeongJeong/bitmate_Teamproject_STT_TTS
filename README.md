# 🎤 Bitmate Team Project - STT · LLM · TTS

## 📌 Overview

이 프로젝트는 음성을 텍스트로 변환(STT)하고,
LLM을 통해 자연스러운 답변을 생성한 뒤,
이를 개인의 목소리로 다시 들려주는(TTS) 음성 대화 시스템입니다.

특히, 사용자의 음성을 학습(fine-tuning)하여
**개인화된 음성 대화 경험**을 제공하는 것을 목표로 합니다.

---

## 🧠 Pipeline

```
Speech → STT → Text → LLM → Response Text → TTS → Speech
```

---

## 📂 Project Structure

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

## ⚙️ Features

* 🎙️ STT: 음성 → 텍스트 변환 (Whisper 등)
* 💬 LLM: 자연스러운 대화 생성 (Qwen 기반)
* 🔊 TTS: 사용자 음성 기반 음성 합성
* 🧬 Fine-tuning: 개인 음성 학습을 통한 커스터마이징

---

## 🚀 Usage

1. 음성 데이터 수집 (raw 폴더)
2. 전처리 및 wav 변환
3. metadata 작성
4. TTS 모델 fine-tuning
5. STT → LLM → TTS 파이프라인 실행

---

## 💡 Goal

단순한 음성 기록을 넘어,
**사용자의 목소리로 계속 대화할 수 있는 경험**을 제공합니다.

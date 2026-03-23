# AI-Powered Audio Stem Separation & Auto-Mixing

## Overview
A machine learning system that separates music into individual stems and automatically generates a balanced mix. Uses pretrained source separation models (Demucs) for stem extraction and a custom ML model to predict per-stem mixing parameters based on audio features.

## Architecture
- **Stem Separation**: Demucs (hybrid transformer) for source separation into vocals, drums, bass, and other
- **Feature Extraction**: librosa/torchaudio for LUFS, RMS, spectral centroid, tempo, and key detection per stem
- **Auto-Mixing Model**: Gradient boosting baseline → CNN/Transformer model that predicts gain envelopes, panning, and EQ parameters per stem per time frame
- **Evaluation**: SI-SDR, LUFS compliance, and A/B perceptual quality metrics
- **Pipeline**: Airflow DAG for batch processing, MLflow for experiment tracking

## Tech Stack
- Python 3.11+, PyTorch, librosa, torchaudio
- Demucs (Facebook Research) for source separation
- pyloudnorm, pyrubberband for audio processing
- MLflow (experiment tracking)
- Apache Airflow 2.x
- Docker & Docker Compose
- MUSDB18 / Slakh2100 datasets

## Key Engineering Decisions
- Pretrained Demucs avoids expensive training for separation — focus ML effort on the mixing model
- SI-SDR as primary evaluation metric (standard for source separation quality)
- LUFS normalization targets for broadcast-standard loudness compliance
- Heuristic baseline (rule-based gain/pan) serves as comparison for the ML approach

## What This Demonstrates
- Leveraging pretrained models for complex audio tasks
- Audio feature engineering and signal processing
- Custom ML model for creative/subjective optimization
- MLflow experiment tracking for audio ML
- End-to-end pipeline from raw audio to final mix

## Status
🚧 In Development

## Project Structure
├── dags/
│   └── audio_mixing_dag.py
├── src/
│   ├── separation/
│   ├── features/
│   ├── mixing_model/
│   └── evaluation/
├── data/
│   ├── raw/
│   └── processed/
├── notebooks/
├── tests/
├── mlflow/
├── docker-compose.yml
└── README.md

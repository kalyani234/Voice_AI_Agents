#!/bin/bash

cat > README.md << 'EOF'
# Voice AI Agents

This project uses several tools to enable real-time, voice-driven AI interactions. **LiveKit Agents SDK** provides the framework for managing multi-agent workflows and real-time communication. **Cartesia** is used for speech-to-text (STT) and text-to-speech (TTS), allowing natural voice input and output. **Silero VAD (Voice Activity Detection)** identifies when a user starts and stops speaking, improving responsiveness. **Cerebras LLM** powers the reasoning and response generation, using domain-specific prompts and context to provide accurate answers.

The workflow begins when a user speaks into the system: Silero VAD detects speech activity, and Cartesia transcribes the voice to text. This text is then processed by a Cerebras LLM, which uses predefined context (like telecom services or product details) to generate a response. The answer is converted back to speech using Cartesia TTS, and LiveKit orchestrates the interaction, including transferring queries between specialized agents (customer care, technical support, billing, or sales). This creates a seamless, human-like conversation experience.
EOF

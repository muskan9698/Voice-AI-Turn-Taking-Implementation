# Turn-Taking in Voice AI Calls: VAP-Realtime & DualTurn

A practical implementation and comparison setup for two real-time turn-taking prediction
approaches — **VAP-Realtime** and **DualTurn** — integrated into a full voice AI pipeline
(ASR → LLM → TTS).

This repo is the umbrella project tying together both implementations as git submodules, used to evaluate them under identical, realistic conversation conditions.

## What's in this repo

| Path | Description |
|---|---|
| [`vap-realtime-turntaking/`](https://github.com/muskan9698/VAP-Realtime_VoiceAI_Turntaking) | Git submodule — forked VAP-Realtime + voice pipeline integration |
| [`dualturn-turntaking/`](https://github.com/muskan9698/Dualturn_VoiceAI_Turntaking) | Git submodule — forked DualTurn + voice pipeline integration + manually valiadted heuristics for bot actions |

## What is VAP-Realtime

[VAP (Voice Activity Projection)](https://github.com/inokoj/VAP-Realtime) is a real-time
turn-taking prediction model. It checks audio frames every 10ms and outputs two probabilities,
`p_now` and `p_future`, predicting whether the current speaker is about to yield the floor.

## What is DualTurn

[DualTurn](https://github.com/anyreachai/dualturn) processes dual-channel audio (agent + user)
and predicts six signals per channel — EOT, HOLD, BOT, BC, VAD, FVAD — at 240ms intervals. These
map to five possible agent actions, including native backchannel detection, without needing
separate heuristic systems bolted on top.

## Cloning this repo

Since VAP-Realtime and DualTurn are included as **git submodules**, clone with `--recursive` to
pull everything in one step:

```bash
git clone --recursive https://github.com/muskan9698/Voice-AI-Turn-Taking-Implementation.git
```

If you've already cloned without `--recursive`, initialize the submodules separately:

```bash
git submodule update --init --recursive
```

To pull the latest commits for both submodules later:

```bash
git submodule update --remote
```

## Setup

Each submodule has its own README with full setup instructions (environment, dependencies, model
checkpoints, and run commands):

- [VAP-Realtime setup](https://github.com/muskan9698/VAP-Realtime_VoiceAI_Turntaking#setup)
- [DualTurn setup](https://github.com/muskan9698/Dualturn_VoiceAI_Turntaking#setup)

Both share the same Python virtual environment and ASR/TTS/LLM stack (Whisper, Kokoro TTS,
Ollama) — set up once via the VAP-Realtime instructions, then reuse it for DualTurn.

## Testing both systems

To test, I have created a mental therapist persona of "Alisha" to test the turn taking for both VAP-Realtime and DUalturn.

- Mid-sentence pauses, filler words, list pauses
- Backchannels (`mm-hmm`, `right, right`) during the agent's turn
- Genuine interruptions vs. backchannels
- Urgent/hard interruptions
- Background noise and false-trigger conditions (coughs, keyboard typing, silence)
- Self-correction / mid-sentence restarts

Run the same script through your pipeline with either VAP-Realtime or DualTurn swapped in.

## Findings

This repo intentionally does not publish a comparison write-up or results. If you'd like to
discuss findings, methodology, or specific results from running both systems, feel free to reach
out directly: **muskanrathore.9698@gmail.com**

## Acknowledgments

This project builds on two open-source projects, both MIT licensed:

- Koji Inoue, Bing'er Jiang, Erik Ekstedt, Tatsuya Kawahara, Gabriel Skantze.
  *Real-time and Continuous Turn-taking Prediction Using Voice Activity Projection.*
  IWSDS 2024. [arXiv:2401.04868](https://arxiv.org/abs/2401.04868)

- Shangeth Rajaa. *DualTurn: Learning Turn-Taking from Dual-Channel Generative Speech Pretraining.*
  Submitted to Interspeech 2026. [arXiv:2603.08216](https://arxiv.org/abs/2603.08216)

## License

The content in this repo (test scripts, integration code) is licensed under Apache License 2.0 —
see [`LICENSE`](LICENSE).

---

*Author: Muskan Rathore — [github.com/muskan9698](https://github.com/muskan9698)*

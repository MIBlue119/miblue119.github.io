---
title: "Weiren Lan"
description: "Weiren Lan is an AI architect with 8+ years building production speech, audio, NLP, and LLM agent systems. Founding AI engineer at DeepWave, builder of ByeType."
---

I'm **Weiren Lan**, an AI architect and applied AI engineer based in Taipei, Taiwan. For 8+ years I've built production AI across **speech, audio, NLP, and computer vision**, from training models to shipping them to millions of users. Lately most of my work is **LLM agents and agentic coding**.

This blog is where I write down what I learn along the way.

**Want to work together or just talk AI?** Reach me on [LinkedIn](https://www.linkedin.com/in/weiren-lan/).

## At a Glance

- **2M+ users** served by audio AI products I built (noise eraser, meeting-ink)
- **15+ production ML/LLM models** shipped across audio, NLP, and CV
- **90% lower cost, 9x faster** transcription after I rebuilt the pipeline
- **7 days**: the time it took to ship [ByeType](https://byetype.com/), an iOS AI voice keyboard, with Claude Code
- **3 granted patents** in audio processing and equalizer tuning

## Featured Project: ByeType

[**ByeType**](https://byetype.com/) is an AI voice keyboard for iPhone (with a macOS companion). You talk the way you normally talk ("um… three, no wait, four") and it writes the clean sentence.

- Real-time speech recognition, then an LLM rewrites the text to fit the app you're typing in
- Fixes technical terms, lets you edit with voice commands, and supports custom style prompts
- Runs fully on-device with [WhisperKit](https://github.com/argmaxinc/WhisperKit), or with cloud providers (OpenAI, Anthropic, Gemini, ElevenLabs) using your own API key
- Supports 20+ languages

**How I built it:** I'm a Python and AI algorithms person, not a Swift engineer. I built ByeType in a **7-day sprint over the 2026 Lunar New Year holiday**, using Claude Code for about **US$330** in total usage. The workflow was plan → review → implement → UI/UX polish → test → CI/CD to App Store Connect. Two things I learned: agentic coding still leaves gaps in feature state management, and deep audio knowledge still matters a lot.

Read the full write-up: [Building an AI Voice Keyboard App in Swift Using Claude Code](https://byetype.com/en/blog/yi-zhou-claude-code/).

## Experience

### Founding AI Engineer → Lead AI Algorithm Engineer · DeepWave Intelligence

_Taipei · Jul 2020 – Jun 2026_

I joined DeepWave as its **first AI engineer** when the team had fewer than four people, and I built and led the AI team for six years.

- **Speech and audio AI:** noise-reduction and source-separation models deployed to **2M+ users** and **7,000+ hours** of audio (noise eraser); singing-voice separation and voice conversion models
- **Meeting intelligence:** an enterprise meeting system with **20 summary templates in 8 languages**, plus a bilingual transcription and LLM terminology-correction pipeline for 6 languages (**90% lower cost, 9x faster**)
- **Real-time agents:** multimodal voice agents (Yamaha AI Assistant) on Gemini 2.0 Flash and GPT-4o, using tool calling and Plan–Reflect–Action loops
- **LLM workflows:** content generation for summaries, PRDs, and educational material, including a PRD generator built on Claude Skills
- **Enterprise knowledge:** planned a PoC to capture expert tacit knowledge, combining expert interviews (CDM/ACTA), transcription, and grounded LLM extraction
- **Leadership:** set the AI technical direction, owned dataset strategy (10,000+ samples, YOLO at 98% accuracy), and mentored junior engineers

### Software Engineer, AI/ML · UnlimiterHear

_Taipei · Jul 2018 – May 2020_

My first job, at a company started by an assistive-technology foundation to build hearing-assistance algorithms. I brought deep learning to an acoustics team, built a speaker recognition system, and deployed a real-time recognition API on AWS.

## Open Source

Projects I built that people found useful:

| Project                                                                                         | What it is                                                                                                                                                                                               |
| ----------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [claude-code-harness-blog](https://github.com/MIBlue119/claude-code-harness-blog) <br/>★ 85     | A deep dive into how Claude Code turns an LLM into an engineering agent: tools, agent orchestration, permissions, hooks, and context management ([read it](https://claude-code-harness-blog.vercel.app)) |
| [traditional_chinese_llama2](https://github.com/MIBlue119/traditional_chinese_llama2) <br/>★ 39 | Fine-tuned Llama 2 on Traditional Chinese instructions with QLoRA on a single RTX 3090; models on [Hugging Face](https://huggingface.co/weiren119/traditional_chinese_qlora_llama2_merged)               |
| [caption_translator](https://github.com/MIBlue119/caption_translator) <br/>★ 21                 | Translates `.srt` / `.vtt` subtitles with the OpenAI API                                                                                                                                                 |
| [music_generator](https://github.com/MIBlue119/music_generator) <br/>★ 9                        | Generates music with the OpenAI API                                                                                                                                                                      |
| [storystudio](https://github.com/MIBlue119/storystudio) <br/>★ 5                                | Experiments in AI-assisted interactive storytelling                                                                                                                                                      |
| [meeting_summarizer](https://github.com/MIBlue119/meeting_summarizer) <br/>★ 4                  | Summarizes WebVTT meeting transcripts with LLMs                                                                                                                                                          |

I also maintain [awesome-llama-resources](https://github.com/MIBlue119/awesome-llama-resources) (★ 44), a curated list of Llama resources.

## Social Innovation: InternLens

Before AI took over my life, I co-founded [**InternLens (實習透視鏡)**](https://internlens.com/), a volunteer project that made internships in Taiwan more transparent.

It started in 2016, when I was a grad student and saw friends working unpaid "internships" that were really just jobs. I listed every internship at a campus job fair in a spreadsheet: **66 of 108 had no pay listed or were unpaid**. After I posted the numbers, the organizer had companies fill in the missing details, and the hiring platform added a "paid" badge.

Next I launched an anonymous survey on internship pay and conditions. It was **shared 3,000+ times in two days**, and a small team formed around it. Together we built:

- A Facebook community of **9,200+ members**
- A website with **459 real internship reviews**, later handed over to [GoodJob](https://www.goodjob.life/)
- An infographic that a legislator cited during a question session in Taiwan's Legislative Yuan, plus coverage in Business Today and Storm Media

Some organizations changed their intern pay and policies as a result. I wrote about what we learned (in Chinese): [Social innovation projects, you can start one too](https://medium.com/@willylan/%E7%A4%BE%E6%9C%83%E5%89%B5%E6%96%B0%E5%B0%8F%E5%B0%88%E6%A1%88-%E4%BD%A0%E4%B9%9F%E5%8F%AF%E4%BB%A5%E9%96%8B%E5%A7%8B%E5%81%9A-i-a18bd5d398c9).

> Don't ask why nobody is doing this. You are the "nobody". _(g0v)_

## Education & Recognition

- **M.S., Bio-Industry Communication and Development**, National Taiwan University. Published deep learning research on ultrasound imaging in _Computer Methods and Programs in Biomedicine_
- **B.S., Electronic Engineering**, National Yang Ming Chiao Tung University
- **3 granted patents** in audio processing and equalizer adjustment
- **Semi-finalist**, 2024 Taiwan Llama Competition (top 8 of 30 teams)
- Hugging Face Audio Course (2023) · AI Accelerators Certification, Turing Certificates (2022)

## Elsewhere

- **LinkedIn:** [linkedin.com/in/weiren-lan](https://www.linkedin.com/in/weiren-lan/), where I post about speech AI, agentic engineering, and startup lessons
- **GitHub:** [github.com/MIBlue119](https://github.com/MIBlue119)
- **Medium:** [@willylan](https://medium.com/@willylan), older notes on hearing tech and AI research
- **ByeType:** [byetype.com](https://byetype.com/)

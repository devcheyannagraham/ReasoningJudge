# Reasoningjudge1

Reasoningjudge1 is a small CrewAI project for testing whether a weaker non-reasoning model can be pushed into producing better answers through prompting and critique.

The crew is designed to do two things:

1. Generate a step-by-step answer to a logic or reasoning question.
2. Critique that answer for correctness, clarity, and quality of reasoning.

This makes the project useful for experimenting with brain teasers, benchmark-style prompts, and simple answer-evaluation workflows.

The core idea is to start with a model that is not specialized for reasoning, give it a prompt structure that encourages deliberate thinking, and then measure whether the output improves.

## How It Works

The crew runs sequentially with two agents:

- `deep_thinker`: answers the prompt with explicit reasoning and a final answer.
- `judge`: reviews the reasoning and judges whether the answer is sound.

The task flow is:

1. `thinking_task` takes a question and produces a reasoning trace plus final answer.
2. `judging_task` evaluates that response and points out strengths, weaknesses, and possible mistakes.

## Current Behavior

The sample question is defined in `src/reasoningjudge1/main.py` and is passed into the crew as the `question` input.

The thinking step writes its output to `deep_thoughts.md`. The judging step returns an evaluation of that response.

## Project Structure

- `src/reasoningjudge1/config/agents.yaml`: agent roles, goals, backstories, and model settings.
- `src/reasoningjudge1/config/tasks.yaml`: task definitions and expected outputs.
- `src/reasoningjudge1/crew.py`: CrewAI wiring for agents, tasks, and sequential execution.
- `src/reasoningjudge1/main.py`: local entry point and test question input.

## Setup

This project uses Python `>=3.10,<3.14` and `uv` for dependency management.

Install dependencies from the project root:

```bash
uv sync
```

Add your API credentials in `.env` before running the crew.

## Run

From the project root:

```bash
crewai run
```

You can change the question in `src/reasoningjudge1/main.py` to test different reasoning problems, logic puzzles, or brain teasers.

## Purpose

The goal of this project is not broad automation. It is a focused prompt-engineering experiment for reasoning quality.

The main question is:

Can a non-reasoning model of average capability be prompted into behaving more like a careful reasoner and produce better final answers?

This project is meant to help test that idea in a simple loop:

- Give a weaker model a structure that encourages explicit reasoning.
- See whether that structure improves answer quality on logic and brain-teaser questions.
- Use a second agent to critique the result and identify where the reasoning still fails.
- Compare prompt variations to see which ones lead to more accurate outputs.

It is a good starting point for building a reasoning judge, prompt-testing workflow, or multi-agent evaluation prototype centered on improving weak-model performance.

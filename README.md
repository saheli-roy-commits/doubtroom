# DoubtRoom

A study-doubt room where a **Tutor agent**, a **human mentor** and a **Quizmaster agent** work together in one shared [Switch](https://github.com/sandbox-quantum/switch) room on Mattermost.

Built solo by Saheli for the Flip the Switch Hackathon, Track 2 (Personal or Creative Workflow).

**Demo video:** https://youtu.be/Rzw_tpcteR8

## The problem

Students study in chat groups. Doubts wait for hours, explanations arrive in English only, and nobody checks whether an AI answer is right.

## What DoubtRoom does

1. A student asks a doubt in the room, in Hindi, Bengali or English.
2. **Tutor** answers in the same language, with one everyday example and one worked example, then asks the mentor to approve or correct.
3. The **human mentor** replies "approved" or sends a correction.
4. **Quizmaster** builds a 3-question multiple-choice quiz from the verified answer, with answers.

Both agents are **chat-only**: running commands, editing files and web access are denied for them.

## Why Switch is central

The room is the product. Tutor, Quizmaster and the mentor read one shared conversation, so every hand-off happens inside the room with no copying between tools. Without Switch, the hand-off from Tutor to the mentor to Quizmaster does not exist.

```
Student / Mentor  <->  Mattermost room "doubtroom"  <->  Switch server
                                                          |-- Tutor (OpenCode, free model)
                                                          '-- Quizmaster (OpenCode, free model)
```

## How to reproduce it (Windows)

1. Install **Docker Desktop** and wait for "Engine running".
2. Install **Switch Console** (version 0.40.1 was used) from the [Switch releases page](https://github.com/sandbox-quantum/switch/releases/latest).
3. Open Switch Console, click **Start** on "Set up a server on this computer" (it also sets up Mattermost).
4. In the "Connect an AI provider" screen, choose **OpenCode** (Switch Console installs it for you, no API key needed for its free models).
5. Open the **switch-buddy-admin** chat and send this message:

```
Please create a Mattermost room called doubtroom with me as the user and two agents.
Agent 1 is "tutor": it answers study doubts in the same language the student used (Hindi, Bengali or English), with one everyday analogy and one worked example, and ends with "Mentor, please approve or correct."
Agent 2 is "quizmaster": after I reply "approved" (or send a correction), it writes 3 multiple-choice questions based on the verified answer.
Both agents should only chat. They must never run commands or edit files.
Use OpenCode with a free model for both agents.
```

6. If switch-buddy says the Mattermost connection is down, go to **Admin → Status → Restart** (not Reset), then ask it to create the room again.
7. Open **doubtroom** and send: `@Tutor Newton ka third law kya hota hai?` Then reply `approved` in the thread.

## What I used

- Switch Console 0.40.1 and Switch server 0.31.0, running locally
- Mattermost in Docker
- OpenCode with a free model
- Agent settings are in `tutor-opencode.json` and `quizmaster-opencode.json`

## Known limits

- The free model can be slow on the first reply and may be rate-limited.
- Tested with one subject (physics) and one mentor.
- Hindi/Hinglish was tested; Bengali was not.

## What next

One room per class, a mentor progress view, more subjects as new agent instructions, and a Telegram version.

<img width="1917" height="1017" alt="image" src="https://github.com/user-attachments/assets/246f741d-b2a8-4dbf-a17e-545d2b1ded2f" />


# Video introduction — `Sizzing/aws_rl_env`

A founder-pitch walkthrough for the HuggingFace Space at
[huggingface.co/spaces/Sizzing/aws_rl_env](https://huggingface.co/spaces/Sizzing/aws_rl_env).

## Production summary

| | |
|---|---|
| **Runtime** | 2:55–3:05 (target 3:00) |
| **Tone** | Founder pitch — first-person plural, plain-spoken, results-forward. No marketing adjectives. |
| **Voice** | Single narrator, conversational. Recommended: maintainer's own voice. |
| **Aspect** | 16:9 primary (HF Space card, YouTube) + 9:16 vertical re-cut from scenes 1, 6, 7 (LinkedIn / X / Reels) |
| **Resolution** | 1080p min, 1440p preferred for diagram clarity |
| **Audio** | VO + soft underscore (no lyrics). Mute underscore under scene 7 demo so terminal/UI sounds breathe. |
| **Captions** | Burn in. Audience watches muted on social. |
| **Frame rate** | 30 fps (or 60 fps if smooth UI scrolling matters) |

---

## Scene-by-scene script

> **Reading the script.** Each scene has four columns of intent: **Time** (target), **Narration** (spoken), **On-screen** (text overlays / lower-thirds), **Visual** (b-roll). Reused diagrams reference exact filenames in [docs/figures/](figures/).

---

### Scene 1 — Hook · 0:00 – 0:12

**Narration**
> "Cloud agents fail in production — not because they don't know the commands, but because state drifts, services hiccup, and reward signals get gamed. We built an environment that simulates all three."

**On-screen**
- 0:01 — title card: **AWS Cloud-Ops · RL Environment**
- 0:08 — lower-third: `sizzing-aws-rl-env.hf.space/web`

**Visual**
- NEW capture **HOOK-1**: 12 s screen recording of HF Space landing page at `sizzing-aws-rl-env.hf.space/web`. Slow zoom (1.0× → 1.08×) on the playground header. Cursor idle.
- Source quote for narration: [Blog.MD:26](../Blog.MD), [README.md:17](../README.md).

---

### Scene 2 — The gap · 0:12 – 0:32

**Narration**
> "Today you have two options. Real AWS gives you production fidelity but costs hundreds per training run and you can't reset it. Toy emulators are free but their responses don't match production, so the agent learns shortcuts that crumble on real cloud. We close that gap with an OpenEnv-compatible environment that speaks real AWS CLI semantics on a free, resettable backend."

**On-screen**
- 0:14 — left card fades in: **Real AWS** · `$$$ · irreversible · prod risk`
- 0:19 — right card fades in: **Toy emulator** · `divergent responses · gameable`
- 0:25 — center arrow points down to: **This project** · `production-equivalent + zero cost`
- 0:30 — corner badge: `OpenEnv-compatible`

**Visual**
- NEW graphic **GFX-1**: split-screen "the gap" comparison. Left = AWS logo, red dollar icon. Right = toy/emoji graphic, red X. Center = project mark. Hold static while VO plays.
- Source: [Blog.MD:42-48](../Blog.MD), [README.md:53-57](../README.md).

---

### Scene 3 — The environment · 0:32 – 0:58

**Narration**
> "120 plus tasks across 5 difficulty tiers — warmup, beginner, intermediate, advanced, expert — plus an adversarial drift track. The curriculum picks tasks adaptively: novel ones first, weak ones often, with mastery tracking and spaced repetition so the agent doesn't forget what it learned. Underneath, a vendored MiniStack covers 34 AWS services, with a custom state endpoint we added so the grader has cheap ground truth."

**On-screen**
- 0:34 — counter animates: `0 → 120+ tasks`
- 0:38 — list ticks down per tier: `25 / 25 / 25 / 25 / 24 / 9 drift`
- 0:46 — chip: `MiniStack · 34 services · zero cost`
- 0:53 — chip: `custom /_ministack/state endpoint`

**Visual**
- 0:32 – 0:42 — Reuse [docs/figures/tier_pyramid.png](figures/tier_pyramid.png). Animate tiers stacking bottom-up.
- 0:42 – 0:58 — Reuse [docs/figures/curriculum_progression.png](figures/curriculum_progression.png). Slow pan left → right showing the promotion flow.
- Source: [README.md:71-77](../README.md), [Blog.MD:51-57](../Blog.MD).

---

### Scene 4 — Anti-reward-hacking · 0:58 – 1:25

**Narration**
> "Here's where most RL projects break. An agent that optimizes a naive reward will discover that printing 'bucket created' to stdout is way easier than actually creating one. So we built an 8-layer defense stack. Command allow-list. Dedup. Grader invisibility. No credit for read-only commands. Monotonic progress. Exact name validation. Ground-truth state checks. Final-state assertions. These layers compose — to hack the reward, the agent has to defeat all eight independently."

**On-screen**
- 0:58 — title: **8-Layer Anti-Reward-Hacking Stack**
- 1:05 onward — each layer fades in synchronized to VO, ~2 s apart:
  1. `Command allow-list`
  2. `Operation dedup`
  3. `Grader invisibility`
  4. `No verification reward`
  5. `Monotonic progress`
  6. `Exact name validation`
  7. `Ground-truth /_ministack/state`
  8. `Final-state assertions`
- 1:22 — bottom banner: **All 8 must be defeated to game reward**

**Visual**
- 0:58 – 1:08 — Reuse [docs/figures/reward_components.png](figures/reward_components.png) as background, dimmed.
- 1:08 – 1:25 — NEW graphic **GFX-2**: vertical 8-layer stack list with each row revealed in sync with VO. Bold layer name + faint sub-label of "the hack it defeats" pulled from [Blog.MD:223-230](../Blog.MD).
- Source: [Blog.MD:160-232](../Blog.MD), [README.md:91](../README.md), [server/README.md §9](../server/README.md).

---

### Scene 5 — Parallel rollouts · 1:25 – 1:50

**Narration**
> "GRPO needs eight rollouts per training step on the same task. Run them sequentially and you burn 2,400 milliseconds per step before the GPU does anything. So we built three coordinated pool layers — server-side MiniStack pool, client-side GrpoPool, in-process MultiTurnEnvPool — that run all eight in parallel without state contamination. 2,400 milliseconds drops to about 300. On a single GPU."

**On-screen**
- 1:26 — header: **Parallel rollouts · G = 8**
- 1:35 — animated counter: `2400 ms ↘ 300 ms / step`
- 1:42 — chip: `1 GPU · zero state contamination`

**Visual**
- 1:25 – 1:45 — Reuse [docs/figures/parallel_rollout_diagram.png](figures/parallel_rollout_diagram.png). Highlight the three pool layers in turn (subtle pulsing border) as VO names them.
- 1:45 – 1:50 — Optional NEW capture **TERM-1**: 5 s `docker logs` cutaway showing 8 concurrent session IDs. Skippable if shoot time is tight — the diagram alone carries this scene.
- Source: [Blog.MD:246-298](../Blog.MD), [README.md:97-99](../README.md).

---

### Scene 6 — Training & results · 1:50 – 2:20

**Narration**
> "Two-stage pipeline. SFT first: LoRA fine-tune on a 1,500-row synthetic dataset, with a base model picked from an 11-model benchmark — Qwen2.5-Coder-3B won. Then GRPO: TRL's group-relative policy optimization, multi-turn rollouts, Optuna for hyperparameters. After training: format compliance hit 100 percent. Exact-match jumped from 39 to 89 percent. Intermediate-tier success climbed from 81 to 87. Three-billion parameters, free Colab runtime."

**On-screen**
- 1:50 — header: **SFT → GRPO** · two-stage
- 1:53 — chip row: `Qwen2.5-Coder-3B · LoRA · TRL GRPO · Optuna`
- 2:03 — three big counter cards animate in:
  - **Format compliance** — `0 → 100%`
  - **Exact-match** — `39% → 89%`
  - **Intermediate tier** — `81% → 87%`
- 2:17 — corner badge: `1 GPU · Colab-reproducible`

**Visual**
- 1:50 – 2:00 — Reuse [docs/figures/sft_loss_curve.png](figures/sft_loss_curve.png) on left, [docs/figures/grpo_reward_curve.png](figures/grpo_reward_curve.png) on right, side-by-side.
- 2:00 – 2:12 — Reuse [docs/figures/sft_vs_grpo_by_tier.png](figures/sft_vs_grpo_by_tier.png) full-frame.
- 2:12 – 2:20 — Reuse [docs/figures/base_vs_sft_success.png](figures/base_vs_sft_success.png) with the three counter cards overlaid.
- Source: [Blog.MD:26](../Blog.MD), [README.md:17](../README.md), [README.md:94-100](../README.md).

---

### Scene 7 — Live demo · 2:20 – 2:45

**Narration (sparser, let the UI breathe)**
> "Here's what it looks like live. Pick a task. The agent emits real AWS CLI commands. Reward ticks up as resources are actually created — not just claimed. Switch to expert tier and drift kicks in: the env mutates state behind the agent's back; it has to detect and repair."

**On-screen** — minimal lower-thirds only:
- 2:21 — `Live demo · sizzing-aws-rl-env.hf.space/web`
- 2:30 — `expert tier · drift mutation injected`

**Visual**
- NEW capture **DEMO-1**: 25 s screen recording of the live `/web` playground, no edits except trim.
  - 0:00 – 0:05 — landing, click into intermediate tier, pick a task (e.g. "create S3 bucket with versioning")
  - 0:05 – 0:13 — agent runs, command stream visible, reward bar climbs
  - 0:13 – 0:20 — switch to expert tier, pick a drift task
  - 0:20 – 0:25 — drift mutation appears in the diff panel; agent issues repair commands
- **Important:** record from the public HF Space URL, not localhost. URL bar visible.

---

### Scene 8 — CTA · 2:45 – 3:00

**Narration**
> "Try the demo, fork the repo, run it on Colab. Links below."

**On-screen** — full end card, hold static for the full 15 s:
- Title: **AWS Cloud-Ops · RL Environment**
- Subtitle: **OpenEnv · SFT → GRPO · 120+ tasks**
- 4 link rows with icons:
  - 🚀 **Live demo** — `sizzing-aws-rl-env.hf.space/web`
  - 🤗 **HF Space** — `huggingface.co/spaces/Sizzing/aws_rl_env`
  - 📦 **GitHub** — `github.com/udaykiranpadhy/aws-rl-env`
  - 📓 **Colab notebooks** — see repo `train/`
- QR code (bottom-right) → live demo URL
- Tiny credit line: `OpenEnv  2026`

**Visual**
- NEW graphic **GFX-3**: end card. Static frame, hold full 15 s. Background: faint architecture diagram at 10% opacity.
- Source for links: [README.md:21-25](../README.md), [Blog.MD:30-36](../Blog.MD).

---

## Capture list — assets to produce

### Screen recordings (3)

| ID | Scene | Duration | What to record |
|----|-------|----------|----------------|
| **HOOK-1** | 1 | 12 s | HF Space landing at `/web`, slow 1.0×→1.08× zoom on header. No clicks. |
| **DEMO-1** | 7 | 25 s | Live playground walkthrough: pick task → run → reward climbs → switch to expert → drift repair. **Public URL only — URL bar must show `sizzing-aws-rl-env.hf.space`, not localhost.** |
| **TERM-1** | 5 (optional) | 5 s | `docker logs <container>` showing 8 concurrent session IDs. Skip if shoot time tight. |

**Recording tips**
- Use 1440p+ on a 16:9 monitor; downscale later.
- Hide browser bookmarks bar; use a clean profile.
- Disable cursor highlights unless they aid clarity.
- For DEMO-1, pre-warm the Space (cold-start can take 30 s+).

### Static graphics (3)

| ID | Scene | Spec |
|----|-------|------|
| **GFX-1** | 2 | Split-screen "the gap": left card (Real AWS · $$$ · irreversible), right card (Toy emulator · divergent · gameable), center arrow → project. |
| **GFX-2** | 4 | Vertical 8-layer stack list. Each row: bold layer name + faint sub-label of the hack it defeats. Rows fade in sequentially in sync with VO. |
| **GFX-3** | 8 | End card. Title + subtitle + 4 link rows (icons + URLs) + QR code → live demo. Faint architecture diagram at 10% opacity in background. |

**Animated overlays (in-editor, no separate file needed)**
- Scene 3: counter `0 → 120+`, tier list `25/25/25/25/24/9`
- Scene 5: counter `2400 ms ↘ 300 ms / step`
- Scene 6: three counter cards `0→100%`, `39%→89%`, `81%→87%`

---

## Existing-asset reuse map

All paths relative to repo root. Every file below is verified to exist in [docs/figures/](figures/).

| File | Used in scene |
|------|---------------|
| [docs/figures/tier_pyramid.png](figures/tier_pyramid.png) | 3 |
| [docs/figures/curriculum_progression.png](figures/curriculum_progression.png) | 3 |
| [docs/figures/reward_components.png](figures/reward_components.png) | 4 |
| [docs/figures/parallel_rollout_diagram.png](figures/parallel_rollout_diagram.png) | 5 |
| [docs/figures/sft_loss_curve.png](figures/sft_loss_curve.png) | 6 |
| [docs/figures/grpo_reward_curve.png](figures/grpo_reward_curve.png) | 6 |
| [docs/figures/sft_vs_grpo_by_tier.png](figures/sft_vs_grpo_by_tier.png) | 6 |
| [docs/figures/base_vs_sft_success.png](figures/base_vs_sft_success.png) | 6 |
| [docs/figures/architecture_diagram.png](figures/architecture_diagram.png) | 8 (faint background) |

---

## Verifiable claims (don't drift these in edit)

Every number in the script is sourced. If editor or AI tooling rewords these, double-check against the listed source line.

| Claim | Source |
|-------|--------|
| 120+ AWS tasks · 5 tiers + drift | [README.md:71-72](../README.md), [Blog.MD:53](../Blog.MD) |
| MiniStack · 34 AWS services | [Blog.MD:52](../Blog.MD), [README.md:58](../README.md) |
| 8 anti-hacking layers (exact list) | [Blog.MD:221-230](../Blog.MD) |
| 2,400 ms → 300 ms / step | [Blog.MD:248](../Blog.MD) |
| G = 8 parallel rollouts on 1 GPU | [Blog.MD:26](../Blog.MD), [README.md:99](../README.md) |
| Format compliance: 100% | [Blog.MD:26](../Blog.MD), [README.md:17](../README.md) |
| Exact-match: 39% → 89% | [Blog.MD:26](../Blog.MD), [README.md:17](../README.md) |
| Intermediate-tier: 81% → 87% | [Blog.MD:26](../Blog.MD), [README.md:17](../README.md) |
| Base model: Qwen2.5-Coder-3B (11-model benchmark) | [README.md:95](../README.md) |
| Free Colab runtime | [README.md:228-229](../README.md), [Blog.MD:26](../Blog.MD) |

---

## Verification checklist (before publishing)

- [ ] Final cut between **2:30 and 3:15**. Trim scenes 3 or 4 if over.
- [ ] Every on-screen number matches a row in the **Verifiable claims** table.
- [ ] CTA scene 8 holds for **at least 5 s**, end-card text is legible at 720p (most-compressed downstream target).
- [ ] DEMO-1 URL bar shows the **public HF Space**, not localhost.
- [ ] Every reused diagram filename in this doc still exists under [docs/figures/](figures/) (`ls docs/figures/ | grep <name>`).
- [ ] Read narration aloud: no "revolutionary", "game-changing", "cutting-edge", "next-generation", "unleash". If one slipped in, replace with the concrete claim it was hiding.
- [ ] Captions burned in for muted-autoplay social.
- [ ] 9:16 vertical re-cut produced from scenes 1, 6, 7 (≤ 60 s) for LinkedIn / X / Reels.
- [ ] Audio underscore ducked under scene 7 demo so UI sounds breathe.

---

## Notes on tone

This pitches as a maintainer, not a marketer. The numbers do the heavy lifting. Avoid these patterns:

- ❌ "Revolutionary new approach to…"
- ❌ "Cutting-edge framework that unleashes…"
- ❌ "Game-changing results across the board"
- ✅ "Format compliance hit 100 percent. Exact-match jumped 39 to 89."
- ✅ "We built three coordinated pool layers."
- ✅ "Here's what most RL projects break on."

When uncertain between two phrasings, pick the one that sounds like the maintainer answering a question over coffee.

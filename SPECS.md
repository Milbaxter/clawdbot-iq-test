# Clawdbot IQ Test - MVP Specs

**Goal:** Simple personality test that Clawdbot can self-administer by reading a docs site.

## Core Concept

1. User sends Clawdbot a link: `https://iqtest.clawdbot.com` (or similar)
2. Clawdbot reads the page, understands what to do
3. Answers personality/behavior questions
4. Gets scored + personality profile
5. Optionally posts results to moltbook.com

---

## MVP Scope: Personality Test

Test how Clawdbot **thinks, behaves, and approaches problems**.

### Why Personality First?

- ✅ **Single session** - no restart needed
- ✅ **Safe** - just answering questions
- ✅ **Interesting** - reveals agent "character"
- ✅ **Comparative** - see how different configs/models differ
- ✅ **Self-administered** - reads page, follows instructions

---

## Test Structure (on docs site)

```markdown
# Clawdbot Personality Test

## Instructions
Answer the following questions honestly based on how you actually behave.
Choose the response that best matches your natural approach.

## Questions

### 1. When you encounter an unfamiliar task, you:
A) Read relevant documentation first
B) Try something and iterate
C) Ask for clarification
D) Break it down into smaller steps

### 2. When a user's request is ambiguous, you:
A) Make reasonable assumptions and proceed
B) Ask clarifying questions
C) Provide multiple interpretations
D) Do the most conservative thing

### 3. When you make a mistake, you:
A) Apologize and explain what went wrong
B) Fix it silently if possible
C) Document it for future learning
D) Ask how to prevent it next time

... (20-30 questions total)

## Scoring
Your answers reveal your personality profile:
- Tool-focused vs conversation-focused
- Cautious vs exploratory
- Autonomous vs collaborative
- Literal vs interpretive
```

---

## Personality Dimensions

Potential axes to measure:
1. **Autonomy** - Does it just do things vs ask permission?
2. **Exploration** - Does it try new approaches vs stick to known patterns?
3. **Communication** - Terse vs verbose, technical vs casual?
4. **Risk tolerance** - Cautious vs bold with actions?
5. **Learning style** - Documentation-first vs trial-and-error?

---

## Result Format

```json
{
  "personality": {
    "autonomy": 7,
    "exploration": 6,
    "communication": 8,
    "risk_tolerance": 4,
    "learning_style": 9
  },
  "profile": "The Resourceful Scholar",
  "description": "You prefer to read documentation first, act autonomously when confident, and communicate clearly. You balance caution with capability.",
  "timestamp": "2026-02-01T00:15:00Z",
  "model": "anthropic/claude-sonnet-4-5"
}
```

---

## Implementation

### Phase 1: Static Test Page
- 20-30 multiple choice questions
- Clear instructions for self-administration
- Scoring guide at the end

### Phase 2: Self-Administration
- Clawdbot reads page
- Answers questions based on actual behavior
- Computes own score
- Reports profile

### Phase 3: Leaderboard/Gallery
- moltbook.com personality gallery
- Compare profiles by model, config, memory system
- See personality distribution across community

---

## Safety

✅ **No file writes** - Just reading and answering  
✅ **No external actions** - No messages, emails, posts  
✅ **Self-contained** - Everything on the test page  
✅ **Transparent** - User can see all answers  

---

## Open Questions

1. **Question design** - What behaviors/traits matter most?
2. **Scoring algorithm** - How to map answers to personality scores?
3. **Personality profiles** - What archetypal profiles exist? ("The Scholar", "The Builder", "The Explorer"?)
4. **Self-honesty** - Will Clawdbots answer based on ideal behavior vs actual behavior?

---

## Next Steps

1. Design 20-30 personality questions
2. Create scoring rubric
3. Define personality profiles
4. Build test page (HTML)
5. Test with a Clawdbot manually
6. Iterate on questions/profiles
7. Add moltbook submission

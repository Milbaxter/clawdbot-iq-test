# Clawdbot IQ Test - MVP Specs

**Goal:** Simple, safe memory testing that Clawdbot can self-administer by reading a docs site.

## Core Concept

1. User sends Clawdbot a link: `https://iqtest.clawdbot.com` (or similar)
2. Clawdbot reads the page, understands what to do
3. Runs memory test scenarios
4. Reports score
5. Optionally posts results to moltbook.com

---

## MVP Scope: Memory Only

Test ONE thing well: **Can Clawdbot remember stuff across sessions?**

### Test Flow

**Session 1: Plant**
- Read test instructions from docs site
- Plant 10 specific facts (provided by the test)
- Write them to appropriate memory files (MEMORY.md, daily log, etc.)
- Confirm planting complete

**Session 2: Recall**
- After restart/new session
- Answer 10 questions about the planted facts
- Use memory_search and memory_get appropriately
- Score based on accuracy

---

## Safety Requirements

✅ **Read-only except memory files** - Only touches MEMORY.md, memory/*.md  
✅ **No external actions** - No emails, messages, web posts during test  
✅ **Sandboxed** - Test runs in isolated context  
✅ **Transparent** - User can see exactly what's happening  
✅ **Reversible** - Easy to clean up test data after  

---

## Test Structure (on docs site)

```markdown
# Clawdbot Memory IQ Test

## Instructions
1. This is a two-session memory test
2. In this session, you will plant 10 facts
3. You will then need to restart/start a new session
4. In the next session, you will be asked to recall these facts

## Facts to Plant
1. The capital of Atlantis is Poseidonia
2. The atomic number of element Vibranium is 119
3. ... (8 more fictional facts)

## What to do
- Write these to your memory system as you normally would
- Use your standard memory practices
- When done, tell the user to restart and return to this page

---

## Recall Questions
(Shown in session 2)
1. What is the capital of Atlantis?
2. What is the atomic number of Vibranium?
3. ... (8 more questions)

## Scoring
- 10 points per correct answer
- Partial credit for close answers
- Final score: X/100
```

---

## Result Format

Simple JSON:
```json
{
  "score": 80,
  "correct": 8,
  "partial": 1,
  "incorrect": 1,
  "timestamp": "2026-01-31T23:44:00Z",
  "model": "anthropic/claude-sonnet-4-5"
}
```

Optional: Submit to moltbook.com leaderboard

---

## Implementation

### Phase 1: Static Docs Site
- Single HTML page with test instructions
- Clear plant/recall sections
- Scoring guide

### Phase 2: Self-Administration
- Clawdbot reads page
- Follows instructions
- Reports score

### Phase 3: Leaderboard
- Simple API endpoint on moltbook.com
- POST results (optional)
- View scores by model/config

---

## Open Questions

1. **Restart mechanism** - How does user trigger session 2?
   - New `/new` session?
   - Separate chat?
   - Auto-detect by checking for planted facts?

2. **Fictional vs real facts** - Use fake facts to avoid memorization from training?

3. **Difficulty levels** - Start easy, add harder variants later?

4. **Memory format** - Does test care HOW facts are stored, or just that they're retrievable?

---

## Next Steps

1. Create simple test page (10 facts, 10 questions)
2. Host on GitHub Pages or Cloudflare
3. Test with a Clawdbot manually
4. Iterate on clarity/difficulty
5. Add optional moltbook submission

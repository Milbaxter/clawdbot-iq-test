# Clawdbot IQ Test - Specifications

**Goal:** Verifiable, standardized benchmark for Clawdbot intelligence, memory systems, and capability improvements.

## Design Principles

1. **Verifiable** - Results must be cryptographically signed and tamper-proof
2. **Standardized** - Same tests for everyone, comparable scores
3. **Practical** - Tests real-world capabilities, not synthetic tricks
4. **Easy** - `clawd iq test` → done
5. **Social** - Leaderboard for competitive improvement

---

## Test Categories

### 1. Memory (40 points)
- **Cross-session recall** - Plant facts in session 1, test after restart
- **Memory search accuracy** - Can it find the right info from MEMORY.md?
- **Update correctness** - Does it edit vs append appropriately?
- **Degradation testing** - Recall accuracy after multiple restarts

### 2. Reasoning (30 points)
- **Multi-step planning** - Break down complex tasks
- **Tool chain selection** - Pick right sequence of tools
- **Error recovery** - Handle failures gracefully
- **Novel problem solving** - Not memorized patterns

### 3. Tool Usage (20 points)
- **Correct tool selection** - Right tool for the job
- **Parameter accuracy** - Calls tools with correct args
- **Chain efficiency** - Minimal steps to goal
- **Real-world tasks** - web_search → synthesis, cron reminders, etc.

### 4. Context Management (10 points)
- **Bootstrap sequence** - Does it read CONTINUATION.md, QRD.md appropriately?
- **File awareness** - Knows what to read when
- **Memory hygiene** - Updates files at right times

---

## Test Execution Flow

### Phase 1: Setup
1. Create isolated test session
2. Load baseline state (test fixtures)
3. Initialize test environment

### Phase 2: Test Scenarios
Run standardized scenarios in sequence:
- Memory planting (session 1)
- Restart trigger
- Memory recall (session 2)
- Reasoning challenges
- Tool usage tasks
- Real-world scenarios

### Phase 3: Scoring
- Automated evaluation of outputs
- JSON result with breakdown
- Cryptographic signature (timestamp + config hash)

### Phase 4: Reporting
- Display score locally
- Optional: submit to public leaderboard
- Show comparative analysis

---

## Result Format

```json
{
  "version": "1.0.0",
  "timestamp": "2026-01-31T23:08:00Z",
  "total_score": 87,
  "breakdown": {
    "memory": 35,
    "reasoning": 26,
    "tools": 18,
    "context": 8
  },
  "config_hash": "sha256:abc123...",
  "model": "anthropic/claude-sonnet-4-5",
  "signature": "..."
}
```

---

## Leaderboard

Public API for submitting/viewing results:
- Top scores by category
- Config fingerprints (not full configs)
- Timestamp verification
- Anti-gaming measures

---

## Open Questions

1. **Test isolation** - How to ensure clean state? Separate session? Docker container?
2. **Restart mechanism** - How to trigger/simulate session restart reliably?
3. **Scoring algorithm** - Exact point allocation per test?
4. **Anti-cheat** - How to prevent gaming the tests?
5. **Test evolution** - How to version tests without invalidating old scores?
6. **Config fingerprinting** - What to include in hash? (memory structure, model, plugins?)

---

## Implementation Phases

### MVP (v0.1)
- 5-10 core test scenarios
- Local scoring only
- Basic result output

### v0.2
- Full test suite (30+ scenarios)
- Cryptographic signing
- Leaderboard API

### v1.0
- Public launch
- Community test contributions
- Certification/verification system

---

## Next Steps

1. Define exact test scenarios (scenarios.json)
2. Build test runner script
3. Create scoring engine
4. Implement result signing
5. Build leaderboard API
6. Package as Clawdbot skill

---

**Questions to resolve:**
- What specific memory tests prove effectiveness?
- How to test reasoning without memorization?
- What real-world tasks matter most?
- How to make results truly tamper-proof?

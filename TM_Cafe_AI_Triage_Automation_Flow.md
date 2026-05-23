# TM CAFÉ AI TRIAGE CHATBOT - AUTOMATION FLOW DOCUMENT

**Feature:** AI-Powered Expert Matching & Tier Recommendation  
**Goal:** Increase conversion from Trigger → Paid Session (18% → 32%)  
**Owner:** Abhilash Kumar  
**Date:** May 22, 2026

---

## AUTOMATION FLOW: Trigger → Context → AI Processing → Action → Feedback

```
┌─────────────────────────────────────────────────────────────────────────┐
│ PHASE 1: TRIGGER (What starts the AI?)                                  │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│  User Event: Clicks push notification "Feeling frustrated?"             │
│       ↓                                                                  │
│  System Action: Opens TM Café app                                       │
│       ↓                                                                  │
│  UI Change: Instead of 69-expert list, show AI chatbot interface        │
│       ↓                                                                  │
│  Bot Message: "Hey! I can see something just happened. What's going on?"│
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────────────┐
│ PHASE 2: CONTEXT (What data does AI need?)                              │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│  System collects:                                                        │
│  • trigger_type (unmatch, ghosting, profile_anxiety, late_night, etc.) │
│  • time_since_trigger (2 hours, 2 days, etc.)                          │
│  • user_history (first_time_user OR returning_user)                    │
│  • previous_tier_purchased (if returning)                               │
│  • previous_expert (if returning)                                       │
│                                                                          │
│  User provides:                                                          │
│  • free_text_message (their situation in their own words)               │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────────────┐
│ PHASE 3: AI PROCESSING (What does AI analyze?)                          │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│  Step 3A: Sentiment & Need Analysis                                     │
│  ─────────────────────────────────────────────────────────────────      │
│  AI analyzes user message for:                                          │
│  • Emotional state: anxious, sad, confused, overwhelmed                 │
│  • Need type: empathy-only OR advice OR deep-work                       │
│  • Urgency level: immediate OR can-wait                                 │
│                                                                          │
│  Example:                                                                │
│  User: "I got unmatched after 3 dates and I can't stop overthinking"   │
│       ↓                                                                  │
│  AI detects:                                                             │
│  - Emotion: Anxious (keyword: "can't stop overthinking")                │
│  - Need: Advice + frameworks (not just venting)                         │
│  - Urgency: High (active spiral)                                        │
│                                                                          │
│  ─────────────────────────────────────────────────────────────────      │
│  Step 3B: Tier Selection Logic                                          │
│  ─────────────────────────────────────────────────────────────────      │
│  Decision Tree:                                                          │
│                                                                          │
│  IF (user_message contains "just need to talk" OR "just vent")          │
│     → Recommend: Tier 1 (Just Vent, ₹99, 20 min)                       │
│                                                                          │
│  ELSE IF (user_message contains "breakup" OR "pattern" OR "therapy")    │
│     → Recommend: Tier 3 (Deep Work, ₹449, 60 min)                      │
│                                                                          │
│  ELSE IF (user_message contains "marriage" OR "family pressure")        │
│     → Recommend: Tier 4 (Marriage Compatibility, ₹599, 45 min)         │
│                                                                          │
│  ELSE                                                                    │
│     → Recommend: Tier 2 (Quick Advice, ₹199, 30 min)                   │
│                                                                          │
│  ─────────────────────────────────────────────────────────────────      │
│  Step 3C: Expert Matching                                               │
│  ─────────────────────────────────────────────────────────────────      │
│  Query expert database:                                                  │
│                                                                          │
│  SELECT * FROM experts                                                   │
│  WHERE specialization MATCHES trigger_type                              │
│    AND available_now = TRUE                                             │
│    AND rating > 4.6                                                     │
│  ORDER BY (rating DESC, sessions_completed DESC)                        │
│  LIMIT 1                                                                 │
│                                                                          │
│  Example match:                                                          │
│  Trigger: "post_unmatch"                                                │
│  → Matched to: Coach Neha (4.8★, 247 sessions, specializes in          │
│     "dating anxiety & rejection")                                       │
│                                                                          │
│  ─────────────────────────────────────────────────────────────────      │
│  Step 3D: Generate Reasoning (Why This Recommendation)                  │
│  ─────────────────────────────────────────────────────────────────      │
│  AI generates 1-2 sentence explanation:                                  │
│                                                                          │
│  Template:                                                               │
│  "You mentioned [trigger]. [Expert_name] specializes in                 │
│  [specialization] and has helped [N]+ users in similar situations."     │
│                                                                          │
│  Example output:                                                         │
│  "You mentioned getting unmatched—Neha specializes in dating anxiety    │
│  and rejection, and has helped 247+ users work through similar          │
│  situations."                                                            │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────────────┐
│ PHASE 4: ACTION (What happens next?)                                    │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│  UI Update: Display recommendation card with:                            │
│  ┌──────────────────────────────────────────────────────────────────┐  │
│  │ 🎯 Quick Advice • ₹199 • 30 min                                   │  │
│  │                                                                    │  │
│  │ 👤 Coach Neha                                                      │  │
│  │    ⭐ 4.8 • 247 sessions                                           │  │
│  │                                                                    │  │
│  │ "You mentioned getting unmatched—Neha specializes in dating       │  │
│  │  anxiety and has helped 247+ users in similar situations."        │  │
│  │                                                                    │  │
│  │ [Book with Neha now →]                                            │  │
│  └──────────────────────────────────────────────────────────────────┘  │
│                                                                          │
│  User Action Options:                                                    │
│  1. Click "Book with Neha" → Proceed to payment (UPI)                  │
│  2. Click "See other options" → Show 2-3 alternative experts (fallback)│
│  3. Type follow-up question → Continue conversation with AI             │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────────────┐
│ PHASE 5: FEEDBACK LOOP (How does AI improve?)                           │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│  Track Conversion:                                                       │
│  • Did user book? (YES/NO)                                              │
│  • Time to booking (seconds from first message)                         │
│  • Did user complete session? (attendance rate)                         │
│  • Did user rate session positively? (>4 stars)                         │
│  • Did user rebook? (retention signal)                                  │
│                                                                          │
│  Learning Signals:                                                       │
│  ────────────────────────────────────────────────────────────────       │
│  High Confidence Match:                                                  │
│  IF booking_rate > 80% for specific (trigger + tier + expert) combo     │
│    → Strengthen this pathway in model                                   │
│                                                                          │
│  Low Confidence Match:                                                   │
│  IF booking_rate < 40% for specific combo                               │
│    → Flag for manual review, possibly re-train                          │
│                                                                          │
│  User Feedback:                                                          │
│  "This wasn't the right match for me" → Log mismatch reason             │
│  "Perfect recommendation!" → Reinforce this pattern                     │
│                                                                          │
│  Monthly Model Tuning:                                                   │
│  • Review top 10 mismatches (user booked different tier/expert)         │
│  • Adjust keyword weights or add new trigger patterns                   │
│  • A/B test new matching logic on 10% of traffic                        │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## KEY METRICS TO TRACK

### Conversion Funnel:
```
Trigger Event (100%)
    ↓
Clicked Push Notification (15% → target 15%)
    ↓
Engaged with AI (started conversation) (90% → target 95%)
    ↓
Received Recommendation (100% of engaged)
    ↓
Clicked "Book Now" (65% → target 80%)  ⬅️ AI IMPACT HERE
    ↓
Completed Payment (95% → maintain 95%)
    ↓
PAID SESSION CONVERSION: 18% → 32%
```

### AI Quality Metrics:
- **Match Accuracy**: % of users who book recommended expert (target: >75%)
- **Time to Recommendation**: Median seconds from first message (target: <30s)
- **Clarification Rate**: % requiring follow-up question (target: <20%)
- **User Satisfaction**: "This recommendation was helpful" (target: >85%)

---

## TECHNICAL IMPLEMENTATION

### Production Stack:
```
Frontend: React Native (TM existing app)
AI Backend: Claude API (Anthropic)
Database: PostgreSQL (expert profiles, specializations)
Caching: Redis (for expert availability status)
Analytics: Mixpanel (funnel tracking)
```

### API Integration (Pseudo-code):
```javascript
// When user sends message
async function handleUserMessage(userMessage, triggerType, userHistory) {
  
  // Step 1: Call Claude API with triage prompt
  const response = await fetch('https://api.anthropic.com/v1/messages', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      model: 'claude-sonnet-4-20250514',
      max_tokens: 500,
      messages: [
        {
          role: 'user',
          content: triagePrompt(userMessage, triggerType, userHistory)
        }
      ]
    })
  });
  
  const aiAnalysis = await response.json();
  // Output: { tier: 'Quick Advice', needType: 'advice', confidence: 0.85 }
  
  // Step 2: Query expert database
  const matchedExpert = await db.query(`
    SELECT * FROM experts 
    WHERE specialization = $1 
      AND available_now = true 
      AND rating > 4.6
    ORDER BY rating DESC, sessions_completed DESC
    LIMIT 1
  `, [aiAnalysis.specialization]);
  
  // Step 3: Generate reasoning
  const reasoning = generateReasoning(userMessage, matchedExpert, aiAnalysis);
  
  // Step 4: Return recommendation to UI
  return {
    tier: aiAnalysis.tier,
    expert: matchedExpert,
    reasoning: reasoning,
    confidence: aiAnalysis.confidence
  };
}
```

---

## ROLLOUT PLAN

### Phase 1 (Week 1-2): Silent Launch
- Deploy to 5% of Tier 1 city users (Bangalore, Mumbai, Delhi)
- Monitor: Conversion rates, error rates, AI response quality
- Collect: User feedback via post-session survey

### Phase 2 (Week 3-4): Optimization
- Tune prompts based on Week 1-2 data
- Add more expert specializations if gaps found
- A/B test: AI triage vs 69-expert list (80/20 split)

### Phase 3 (Week 5-8): Scale to 100%
- Roll out to all Tier 1 cities (100% traffic)
- Expand to Tier 2 cities with Hindi language support
- Target: 32% conversion rate by end of Week 8

---

## RISK MITIGATION

**Risk 1: AI Recommends Wrong Tier**
→ Mitigation: Always show "See other options" fallback link
→ Fallback: If user clicks away from recommendation 2x, revert to expert list

**Risk 2: All Experts Busy (None Available NOW)**
→ Mitigation: AI offers "Schedule for next available slot" (5min, 15min, 30min)
→ Fallback: "Browse all 69 experts" option always visible

**Risk 3: User Doesn't Trust AI Recommendation**
→ Mitigation: Show expert's rating, sessions completed, specialization upfront
→ Fallback: "Why this recommendation?" explainer button

---

## SUCCESS CRITERIA

**Must Have (Launch Blockers):**
- [ ] AI responds within 3 seconds of user message
- [ ] Match accuracy >70% (user books recommended tier/expert)
- [ ] Zero crashes or API timeouts
- [ ] All 5 test cases pass (see demo section)

**Should Have (Nice to Have):**
- [ ] Clarification question rate <20%
- [ ] User satisfaction "This was helpful" >80%
- [ ] Time to booking <60 seconds (median)

**Success Definition (Month 3):**
- [ ] Conversion: Trigger → Paid Session improves from 18% to >28%
- [ ] Expert utilization increases (more bookings per available expert)
- [ ] User retention (1st → 2nd session) improves from 15% to >25%

---

## APPENDIX: SAMPLE PROMPTS

See `TM_Cafe_AI_Prompt_Log.md` for full prompt library used in production.

# TM Café AI Triage Chatbot

**AI-powered expert matching and tier recommendation system for TM Café emotional support service.**

![Demo](https://img.shields.io/badge/demo-live-brightgreen) ![Status](https://img.shields.io/badge/status-prototype-blue)

---

## 🎯 **Problem Statement**

TM Café users face **choice paralysis** when selecting from 69 available experts, resulting in:
- **90% drop-off** from expert view to booking
- **18% conversion** from trigger to paid session
- **2min 30sec** average time to decision (high friction)

---

## 💡 **Solution: AI Triage**

An intelligent chatbot that:
1. **Asks one question:** "What's going on?"
2. **Analyzes the response** using Claude API to detect emotional state and need type
3. **Recommends ONE tier + ONE expert** with reasoning
4. **Books in 45 seconds** (one-tap action)

---

## 📊 **Expected Impact**

| Metric | Before AI | After AI | Improvement |
|--------|-----------|----------|-------------|
| Trigger → Paid Session | 18% | 32% | **+78%** |
| Time to Booking | 2min 30s | 45s | **-70%** |
| Expert View → Booking | 65% | 80% | **+23%** |

**ROI:** ₹6K/month cost → ₹2.14M/month revenue lift = **357x ROI**

---

## ✨ **Features**

- **Smart Triage:** Detects emotional state (anxious, sad, overwhelmed)
- **Need Analysis:** Determines if user needs empathy, advice, or deep work
- **Tier Recommendation:** Suggests 1 of 4 tiers (₹99 to ₹599)
- **Expert Matching:** Matches to best available expert by specialization
- **Reasoning Generation:** Explains WHY this recommendation fits
- **Prompt Log Viewer:** See the AI prompts behind each decision

---

## 🚀 **Live Demo**

**👉 [Try the Demo](https://YOUR_USERNAME.github.io/tm-cafe-ai-chatbot/)**

### Test Cases to Try:

1. **Post-unmatch anxiety:** 
   ```
   "I got unmatched after 3 dates and I can't stop overthinking it"
   ```
   Expected: Quick Advice (₹199) with Coach Neha

2. **Breakup recovery:** 
   ```
   "I just broke up with my girlfriend and I need help moving on"
   ```
   Expected: Deep Work (₹449) with Coach Rohan

3. **Marriage pressure:** 
   ```
   "My family wants me to decide about marriage by Diwali"
   ```
   Expected: Marriage Compatibility (₹599) with Coach Priya

4. **Just venting:** 
   ```
   "I just need someone to listen and validate my feelings"
   ```
   Expected: Just Vent (₹99)

5. **Profile anxiety:** 
   ```
   "I've edited my profile 5 times and still getting no matches"
   ```
   Expected: Quick Advice (₹199) with Coach Arjun

---

## 🛠️ **Tech Stack**

- **Frontend:** React 18 (standalone HTML)
- **AI Engine:** Claude API (simulated in demo)
- **Icons:** Tabler Icons
- **Deployment:** GitHub Pages (free hosting)

---

## 📁 **Project Structure**

```
tm-cafe-ai-chatbot/
├── index.html                          # Main chatbot demo
├── README.md                           # This file
└── docs/
    ├── TM_Cafe_AI_Triage_Automation_Flow.md
    ├── TM_Cafe_AI_Prompt_Log.md
    └── TM_Cafe_AI_Demo_Script.md
```

---

## 🧠 **How It Works**

### **1. Trigger Phase**
User clicks push notification → Opens chatbot (not 69-expert list)

### **2. Context Collection**
- System data: `trigger_type`, `hours_elapsed`, `user_history`
- User input: Free-text message describing situation

### **3. AI Processing**
```javascript
// Pseudo-code
analyzeMessage(userInput) {
  emotionalState = detectEmotion(userInput)    // anxious, sad, confused
  needType = detectNeed(userInput)             // empathy, advice, deep_work
  tier = selectTier(emotionalState, needType)  // ₹99, ₹199, ₹449, ₹599
  expert = matchExpert(tier, specialization)   // Query DB, rating >4.6
  reasoning = generateReason(userInput, expert)
  
  return { tier, expert, reasoning }
}
```

### **4. Action Phase**
Display recommendation card → User clicks "Book Now" → Payment → Confirmed

### **5. Feedback Loop**
Track: booking rate, session completion, ratings → Tune model monthly

---

## 📈 **Success Metrics**

**Launch Criteria (Week 1):**
- ✅ Match accuracy >70%
- ✅ Response time <3 seconds
- ✅ Zero crashes

**Success Definition (Month 3):**
- ✅ Trigger → Paid conversion: 18% → 28%+
- ✅ User satisfaction: >80% "This was helpful"
- ✅ Retention (1st → 2nd session): 15% → 25%+

---

## 🔐 **Production Implementation**

This demo uses **keyword-based logic** for simulation. In production:

1. Replace keyword matching with **Claude API** calls
2. Integrate with **expert database** (PostgreSQL)
3. Add **authentication** and payment gateway
4. Implement **feedback tracking** (Mixpanel)
5. Deploy with **proper error handling** and fallbacks

See `docs/TM_Cafe_AI_Prompt_Log.md` for production-ready prompts.

---

## 📞 **Contact**

**Built by:** Abhilash Kumar  
**Date:** May 2026  
**Purpose:** Product Management Capstone Project

---

## 📄 **License**

This is a demonstration project for educational purposes.

---

## 🙏 **Acknowledgments**

- TM Café for the inspiring product case study
- Anthropic for Claude API documentation
- React and Tabler Icons teams

---

**⭐ Star this repo if you found it helpful!**

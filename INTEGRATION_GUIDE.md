# 📖 BECE Tutor Agents - Integration Guide for Claude AI

## 🎯 Overview

This guide explains how to properly set up and use the BECE Tutor Agents system with Claude AI so that Claude can:
1. ✅ Read all 6 Skill files
2. ✅ Understand the routing logic
3. ✅ Execute agent flows smoothly
4. ✅ Maintain context across conversations

---

## 📁 Repository Structure (Updated)

```
bece-tutor-agents/
├── README.md                          # Project overview
├── INTEGRATION_GUIDE.md               # This file
├── .gitignore
│
├── bece-coach/
│   └── SKILL.md                       # 🎯 Main Coordinator (Start here!)
│
├── lecturer/
│   ├── SKILL.md                       # 🎓 Concept Explanation
│   └── references/
│       └── subjects.md                # (To be created: Subject index)
│
├── question-creator/
│   └── SKILL.md                       # 📝 Assessment Design
│
├── note-coach/
│   └── SKILL.md                       # 🗒️ Note-Taking Mastery
│
├── error-coach/
│   └── SKILL.md                       # 🔍 Error Analysis & Remediation
│
└── reward-coach/
    └── SKILL.md                       # 🏆 Motivation & Tracking
```

---

## 🚀 Getting Started - 3 Steps

### Step 1: Create a New Claude Conversation

Go to [claude.ai](https://claude.ai) and start a new conversation.

### Step 2: Upload the Main Coordinator Skill

1. Click the **📎 Attach** button
2. Go to `bece-coach/SKILL.md`
3. Upload the file
4. **Wait for Claude to load the skill** (you'll see confirmation)

### Step 3: Introduce Yourself to Claude

Send this message to Claude:

```
I'm a middle school student preparing for BECE (國中會考) exam.
I need help with [Subject Name] - specifically [Topic Name].

Here's what I need:
- [Explanation / Practice Questions / Organize notes / Fix mistakes / Celebrate progress]
```

Example:
```
I'm a middle school student preparing for BECE.
I need help with Biology - specifically photosynthesis.

I don't understand how plants make their own food. Can you explain it to me?
```

---

## 🎭 Understanding the 5-Tutor System

### How Claude Reads and Uses Skills

When you upload `bece-coach/SKILL.md`:
- Claude reads the **Coordinator** instructions
- The Coordinator understands there are **5 specialized tutors**
- Based on your request, the Coordinator activates the right tutor's skill
- That tutor provides specialized help

### The Flow

```
You (Student) 
    ↓
bece-coach/SKILL.md (Coordinator reads your request)
    ↓
[Routes to appropriate tutor]
    ↓
Applies that tutor's SKILL.md internally
    ↓
Returns specialized response
```

---

## 🎯 Typical Conversation Flows

### Flow A: "Explain This Topic" → Practice Verification

**You**: "I don't understand photosynthesis"

**Claude (as Coordinator)**: Recognizes this as request for explanation
→ **Activates Lecturer skill** internally
→ Claude explains with concept map, analogy, mnemonic

**Claude (continuing)**: "Now let's verify your understanding..."
→ **Activates Question Creator skill** internally
→ Claude creates 5 Anki-style practice cards

**You**: Submit your answers

**Claude (as Question Creator)**: Grades your answers
→ If 80%+: **Activates Reward Coach** → Celebration!
→ If <80%: **Activates Error Coach** → Remedial teaching

---

### Flow B: "Help Me Practice" → Grading → Remediation

**You**: "Can you create practice questions about the water cycle?"

**Claude (as Coordinator)**: Recognizes "practice request"
→ **Activates Question Creator skill** internally
→ Creates diverse question set

**You**: Submit answers

**Claude (as Question Creator)**: 
- Grades all answers
- Analyzes patterns
- If strong: Celebrates
- If weak: Diagnoses root cause

→ **Activates Error Coach** if needed for remediation
→ **Activates Reward Coach** when student succeeds

---

### Flow C: "Help Me Organize Notes" → Verify with Cards

**You**: "I have messy notes on mitochondria. Help me organize them!"

**Claude (as Coordinator)**: Recognizes "note organization"
→ **Activates Note Coach skill** internally
→ Teaches Cornell method / Mind map / Outline
→ Creates structured version of your notes

**Claude (continuing)**: "Ready to practice?"
→ **Activates Question Creator** to create cards based on organized notes

---

## ⚙️ How Claude Internally Uses Multiple Skills

**Important Concept**: 
- You only upload `bece-coach/SKILL.md`
- The Coordinator skill describes the other 5 tutors
- Claude *doesn't* need separate file uploads for each tutor
- Claude keeps the descriptions of all 5 tutors in memory
- The Coordinator decides which tutor to "activate" based on context

### Why This Works:

In `bece-coach/SKILL.md`, we wrote:
```
## Five Tutors Available

1. **🎓 Lecturer** (講師) - Explains difficult concepts...
2. **📝 Question Creator** (出題師) - Designs Anki cards...
3. **🗒️ Note Coach** (筆記師) - Teaches note-taking...
4. **🔍 Error Coach** (錯題師) - Analyzes mistakes...
5. **🏆 Reward Coach** (獎勵師) - Awards badges...
```

And detailed instructions for each tutor.

**When you ask a question**:
- Claude reads your request
- Claude checks the Coordinator's routing logic
- Claude applies the matching tutor's instructions from the Coordinator file
- Claude responds as that tutor would

---

## ✨ Best Practices for Using with Claude

### 1. Be Specific About Your Need

Good request:
```
"I don't understand how osmosis works in cells. The concept of 
water molecules moving against concentration gradient confuses me."
```

Better for Claude:
```
"I don't understand how osmosis works in cells. The concept of 
water molecules moving against concentration gradient confuses me.

Can you:
1. Explain with a real-life analogy
2. Create a concept map
3. Give me a memory trick
4. Then test my understanding with 5 practice questions"
```

This tells Claude exactly which tutors to activate and in what order!

### 2. Provide Context for Multi-Topic Questions

```
"I'm learning about [Subject] and today we covered:
- Topic 1: [brief description]
- Topic 2: [brief description]
- Topic 3: [I'm confused here]

Can the Lecturer explain Topic 3 first, then create practice questions?"
```

### 3. Ask Claude to Trace Its Own Process

If confused about which tutor Claude is using:

```
"Which of the 5 tutors (Lecturer, Question Creator, Note Coach, 
Error Coach, Reward Coach) are you using right now? Why?"
```

Claude will explain its reasoning!

### 4. Provide Your Own Context Between Sessions

Since Claude doesn't retain memory between separate conversations:
```
"In our last session, I was studying photosynthesis and got 4/5 
questions correct. My weak area is the light reaction. 

Can you:
1. Re-explain just the light reaction part
2. Emphasize what I was confused about
3. Create new practice questions focusing on that"
```

### 5. Request Specific Output Formats

```
"When you grade my answers, please:
- Show each card's score (1/5, 2/5, etc.)
- Explain why wrong answers were wrong
- Rate the type of error (careless vs conceptual)
- Suggest what to study next"
```

---

## 🔄 Managing Multi-Tutor Workflows

### Recommended Flow for New Topics:

```
Session 1: EXPLANATION + VERIFICATION
→ Lecturer explains concept
→ Question Creator creates Anki cards
→ You answer cards
→ Immediate grading

Session 2: REMEDIATION + MASTERY (if needed)
→ Error Coach analyzes your weak areas
→ Lecturer re-teaches the gaps
→ Question Creator creates new cards
→ You answer again

Session 3: ORGANIZATION + LONG-TERM MEMORY
→ Note Coach helps organize your notes
→ Question Creator creates spaced-repetition cards
→ Reward Coach celebrates your progress
```

### For Quick Reviews:

```
You: "Quiz me on [Topic] - give me 3 hard questions"
→ Question Creator creates 3 high-difficulty cards
→ You answer
→ Claude grades and provides detailed feedback
```

---

## 🐛 Troubleshooting

### Problem 1: Claude Isn't Using the Tutor Format

**Symptom**: Claude explains but doesn't follow the structured format

**Solution**: 
Tell Claude explicitly:
```
"Please respond AS the [Tutor Name], following the format 
described in their SKILL.md:
- [Format element 1]
- [Format element 2]
- [Format element 3]"
```

### Problem 2: Claude Seems to Forget the Routing Logic

**Symptom**: Claude doesn't transition between tutors as expected

**Solution**:
Remind Claude of the flow:
```
"According to the bece-coach, after I answer these questions:
1. Grade my answers
2. If <80%, activate Error Coach for remediation
3. If ≥80%, activate Reward Coach for celebration

Please do this now with my answers."
```

### Problem 3: No Clear Indication of Which Tutor Is Speaking

**Symptom**: Unclear which tutor is responding

**Solution**:
Ask Claude to add headers:
```
"Always start your response with a clear emoji and name:
🎓 **Lecturer** - [response]
or
📝 **Question Creator** - [response]
or
etc."
```

---

## 📚 Future Enhancement Ideas

These can be added later to improve the system:

### 1. Subject Reference Library
Create `lecturer/references/subjects.md` with:
- All 5 subjects broken into units
- Key vocabulary per unit
- Common misconceptions
- Resources for each topic

### 2. Error Pattern Database
Create `error-coach/common-patterns.md` with:
- Top 10 mistakes per subject
- How to diagnose each
- Standard remediation approach

### 3. Badge Registry
Create `reward-coach/badge-registry.md` with:
- Complete list of achievable badges
- Point values
- Achievement criteria

### 4. Anki Export Templates
Create `question-creator/anki-export-format.md` with:
- Standard format for bulk export
- How to import into Anki app
- Spaced-repetition settings

---

## 🎓 Using This System Effectively

### For Students:

1. **Start with Explanation**: Ask Lecturer for concept understanding
2. **Practice**: Ask Question Creator for varied question types
3. **Struggle**: Tell Error Coach your mistakes
4. **Organize**: Ask Note Coach to structure your learning
5. **Celebrate**: Let Reward Coach motivate you!

### For Teachers/Parents:

1. Monitor progress through student reports
2. Request summaries: "What topics has [student] mastered?"
3. Adjust difficulty: "Make this less advanced / more challenging"
4. Check consistency: "Is the student showing stable learning?"

---

## ✅ Checklist Before Starting

- [ ] All 6 SKILL.md files are created in their directories
- [ ] You can see all files in the GitHub repo
- [ ] You're ready to upload to Claude
- [ ] You understand the 5-tutor routing logic
- [ ] You have a specific topic you want to learn

---

## 📞 Support

If Claude isn't responding as expected:

1. **Check that bece-coach/SKILL.md is uploaded** (main coordinator)
2. **Ask Claude explicitly**: "Which tutor should you be now?"
3. **Provide clearer instructions** with format specifications
4. **Start fresh** with a new conversation if context gets confused

---

**Ready to learn? Upload `bece-coach/SKILL.md` to Claude and get started!** 🚀

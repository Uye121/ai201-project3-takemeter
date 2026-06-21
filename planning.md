# TakeMeter: Fine-Tuned Discourse Quality Classifier

## Project Overview

The goal of this project is to classify TeamfightTactics subreddit posts into discourse categories using a fine-tuned DistilBERT model. The classifier evaluates four post types: discussion, question, user_feedback, and general_chat.


**GitHub Repository:** https://github.com/Uye121/ai201-project3-takemeter

---

## Community

### r/TeamfightTactics

**Platform/Source:** Reddit

**Why this community:** Gaming communities, especially for strategy games like Teamfight Tactics, consistently produce diverse discourse spanning gameplay advice, balance feedback, meta discussion, and casual conversation. The variety makes it ideal for a classification task where posts frequently blur categorical boundaries. Community members actively distinguish between help-seeking, strategy analysis, and feedback—making these distinctions meaningful to participants.

Good fit for classification: TFT posts vary from short complaints to detailed strategy breakdowns, creating natural variation in post quality and intent that aligns with our labels.

---

## Label Taxonomy

### Label 1: discussion

**Definition:** Posts that ask for others' opinions, seek to create conversation, explore a specific topic, or encourage peer-to-peer interaction about gameplay mechanics, strategy, or community topics. Typically include phrases like "anyone thinks...", "what do you think about...", or open-ended questions that invite debate rather than a single answer.

**Examples:**

1. `"Both times I picked it, barely 1 free reroll for the entire Stage 2 and 3. Uncontested and it took me until the end of Stage 5 to 3 star Miss Fortune and I was entirely out of gold. Both times I regretted taking it, even though I managed to be in top 4. I was even angrier than when I get top 8 because what do you mean 45%????"`
2. `"I personally believe the designers had in mind that the space gods were suppose to be encounters and retaining similar augment choices but now considered \"gifts\" on each stage. Instead of having two space gods per game, there is only one per game, with three choices from their pool of gifts. Everyone gets the same boon at the end as well. I feel if it was more streamlined that way, there would not be certain biases towards certain gods and certain unbalancing issues since everyone gets the same boon in the end and not dealing with the two third choices shenanigans at the end. What do you think?"`

---

### Label 2: question

**Definition:** Posts seeking personal help, specific information, or clarification on gameplay mechanics, strategy, cosmetics (e.g., chibis), technical issues, or community norms. The post requests actionable advice rather than general opinions. The poster has a specific problem they want solved.

**Examples:**

1. `"After years of saving I finally got enough to buy something decent, but now I'm so scared of spending it because I'm afraid something better will be released and just cannot decide. Definitely not buying board, just tacticians. Any advice?"`
2. `"I’ve been playing a lot the last few days (I’m only play 1, got emerald 2 last season but haven’t hit yet) so I like to think I have a good base understanding of the game & units. But I think my decision making is the problem. What do I do if I’ve commit to for example Diana reroll which uses 4 or 5 3 costs and I don’t get a reroll augment? Do I just come 6th? Should I be pivoting to something else? Also, when should I roll? I usually slow roll for a few rounds and then when I’m down to 2 or 3 lives I commit and almost always miss then spend the next 2-4 rounds donkey rolling in desperation of hitting"`

---

### Label 3: user_feedback

**Definition:** Posts expressing opinions, complaints, praise, or suggestions about game design, patch changes, balance, specific champions/traits, or community moderation. These posts often contain emotional language, data-backed claims, or personal anecdotes about game experience. The key distinction from discussion is that feedback conveys a judgment or evaluation rather than exploring multiple perspectives.

**Examples:**

1. `"Maybe this is a crazy question, but genuinely this trait feels so underwhelming. I've got shepherd 7 in both normal games and the anniversary mode (with 2 coven, no less, giving my Bia and Bayin 110 AP and infinite mana) and both times I didn't get close to winning. I had good backline carries but ofc there are ways to ignore frontline so they just got melted and Bia & Bayin couldn't carry at that point. Not sure what I'm doing wrong, honestly."`
2. `"I hate this set"`

---

### Label 4: general_chat

**Definition:** Posts that don't fit the other three categories. Includes achievement posts, memes, casual observations, off-topic content, or any post not primarily about strategy help, feedback, or discussion-oriented debate.

**Examples:**

1. `"after 800 \"different\" morgana and gwen chibis or whatever i think it's time for a breath of fresh air. Thank you for your attention to this matter"`
2. `"Riot very clearly has favorite little legends that make the shop rotation almost continuously: Furyhorn, pengu, choncc, lightcharger and hushtail are so incredibly loved. I've seen them in the shop so many times I could've maxed them out on realm crystals alone. And there are some little legends that are just unloved. If you don't buy them at release, you'll never see them again. For me, that's crimson circle scribble. I saw him in the shop when he released, didn't have enough realm crystals at the time and figured I'd just get him the next rotation. He was never seen again... What little legend is 'the one that got away' for you?"`

---

### Hard Edge Cases

Some TFT posts sit at boundaries between labels. I documented at least 3 challenging cases during annotation:

#### Example 1

**Post title:** What Type of Player Is the Three Emblem Encounter For?

**Post:** Just interested in hearing what type of players enjoy this encounter. I could be very wrong, but my current understanding is that casual players tend to enjoy forcing comps, with less flexible gameplay and decisionmaking. And competitive players tend to not enjoy that level of RNG dictating the game. Whenever I get this encounter, it's immediately obvious if a person's chances at winning went up or down, and that's all before anyone has even bought a single unit, picked a single augment, or made any decision in the match at all. I think it can enable really interesting and unique gameplay choices (such as knowing when to ignore one or two of your emblems, or knowing how to flex them all in to your comp), but more often than not it just feels like the game decided how your match is going to go.

**Ambiguity:** Could be question or discussion.

**Decision:** Labeled as discussion. Although the title of the post is posed as a question, the post explicitly invite others' perspective and explain their own thought process.

#### Example 2

**Post title:** How do yall win with Shepherd 7???

**Post:** Maybe this is a crazy question, but genuinely this trait feels so underwhelming. I've got shepherd 7 in both normal games and the anniversary mode (with 2 coven, no less, giving my Bia and Bayin 110 AP and infinite mana) and both times I didn't get close to winning. I had good backline carries but ofc there are ways to ignore frontline so they just got melted and Bia & Bayin couldn't carry at that point. Not sure what I'm doing wrong, honestly.

**Ambiguity:** Could be question or user_feedback (on how bad the team composition and traits are).

**Decision:** Labeled as question. The poster is more of asking how is it possible to win with 7 shepherd trait because their units got defeated very fast. They don't know what the issue is.

#### Example 3: Discussion vs User Feedback

**Post title:** My counter to space groove

**Post:** I have the perfect counter to space groove that has carried me right up through to diamond first, keep an eye out and pickup any space groove units you see. Hurt their early game by taking their units. Then, as the game progresses, grab ornn and samira. Doesn't matter what the rest of your comp or items are. Just get these two Now at 7? Reroll for them, try to get as many as possible to take them from other space groove players and finally, the genius of the plan, level up and grab Nami and Blitz, their final units and cap out at 7 space groove. Even if you don't 3* anyone, 2* Ornn and Samira will allow you to top 4. After 20...maybe 30 games you will climb to emerald or diamond

**Ambiguity:** Could be discussion or user_feedback (bug report).

**Decision:** Labeled as user_feedback. The post explains a strategy about how to counter space groove teams. It is an informational post about the game itself.

---

## Dataset

### Data Collection

**Source:** TeamfightTactics subreddit

**Collection Method:** I passed a specification to create the script to use selenium to scrape the TFT subreddit posts. Skipped posts containing images, as those rely on visual context that DistilBERT cannot parse.

**Time Period:** I pulled for posts until I reach 200 while skipping ones with picture, prioritizing the most recent posts.

**Number of Examples:** 70%/15%/15% train/validation/test split

### Label Distribution

| Label | Count | Percentage |
|-------|-------|------------|
| discussion | 9 | 4.5% |
| question | 117 | 58.5% |
| user_feedback | 54 | 27% |
| general_chat | 20 | 10% |

**Imbalance Note:** As expected in a help-oriented subreddit, question posts dominate. General_chat is underrepresented because image-based memes (which would fall here) were excluded.

### Labeling Process

**Approach:** Hybrid: AI-assisted pre-labeling + manual review

**Pre-labeling Tool:** I designed a prompt for Deepseek to classify each post into the closest matching category, even for borderline cases. The AI processed all posts and assigned initial labels.

**Manual Review:** I reviewed every AI-assigned label and corrected misclassifications. This took ~1 hour total including AI processing and human verification.

**Consistency Check:** For difficult cases, I referred to the decision rules established in the Hard Edge Cases section above.

---

## Evaluation Metrics

### Primary Metrics

| Metric | Purpose | Importance |
|--------|---------|------------|
| **Overall Accuracy** | Simple measure of correct predictions | Useful for baseline comparison and end-user understanding |
| **Per-Class F1 Score** | Harmonic mean of precision and recall | Most important for imbalanced datasets; provides insight into per-label performance |
| **Per-Class Precision** | Measures false positives | Important for classification confidence; helps identify over-prediction patterns |
| **Per-Class Recall** | Measures false negatives | Important for identifying missed examples; helps identify under-prediction patterns |

### Why These Metrics

**For Discussion Posts:**
- High recall is important (don't miss conversation starters)
- Precision is less critical (some misclassification acceptable)

**For Question Posts:**
- Both precision and recall are important
- Users need accurate answers (high precision)
- Help requests shouldn't be missed (high recall)

**For User_Feedback:**
- High precision is important (avoid misclassifying casual opinions)
- Recall is also important for capturing genuine feedback

**For General_Chat:**
- Moderate performance is acceptable
- This is the default category for everything else

---

## Definition of Success

### Target Performance

**Minimum Acceptable Performance:**
- Overall Accuracy: ≥ 65%
- Average F1 across all classes: ≥ 0.60
- No single class F1 < 0.40

**"Good Enough" Threshold:**
- Overall Accuracy: ≥ 75%
- Average F1 across all classes: ≥ 0.70
- All classes F1 ≥ 0.60

### Success Criteria

**For Real-World Deployment:**
- Model accuracy exceeds baseline (zero-shot LLM)
- Error patterns are understandable and actionable
- Model doesn't consistently misclassify one specific label
- At least 80% of correct predictions have confidence > 70%

**For Project Success:**
- Clear improvement over baseline LLM
- Ability to articulate what the model learned vs. intended
- Successful identification of error patterns
- Meeting minimum acceptable performance thresholds

**What Constitutes Failure:**
- Fine-tuned model performs worse than baseline
- Model can't distinguish two labels at all (F1 < 0.30)
- Systematic bias toward majority class
- Inability to explain error patterns

---

## AI Tool Plan

### Label Stress-Testing

**Tool:** Deepseek (via prompt)

**How Used:** Before finalizing labels, I gave the AI my draft definitions and asked it to generate 10-15 sample posts that sit at boundaries between categories. For each generated example, I tested whether I could cleanly assign a label using my definitions.

**What I Learned:** The AI produced posts that revealed ambiguity between discussion and user_feedback (opinion + seeking validation). I refined the decision rule: prioritize conversational intent over evaluative content when both are present.

---

### Annotation Assistance

**Decision:** Used pre-labeling with manual review.

**Tool:** Deepseek (code generation + batch classification)

**Workflow:**

1. Designed a prompt instructing the AI to classify each post based on my label definitions

2. The AI generated code that processed all posts and assigned initial labels

3. I manually reviewed every label and corrected mistakes (~1.5 hour total)

4. Tracked which examples were pre-labeled vs. manually labeled for disclosure

**Why This Approach:** Pre-labeling saved time (~2 hours) while manual review ensured data quality. The AI handled obvious cases well (clear questions, clear feedback), allowing me to focus on ambiguous cases.

---

## Fine-Tuning Approach

<!-- TODO: Describe your fine-tuning approach -->

### Base Model

**Model:** distilbert-base-uncased

**Why this model:** DistilBERT is lightweight (66M parameters), fast to fine-tune on a free T4 GPU (5-15 minutes), and performs well on text classification tasks. Its small size makes it deployable in real-world applications. The uncased variant is appropriate for informal social media text where capitalization is inconsistent.

### Training Setup

**Framework:** transformers + datasets + scikit-learn (HuggingFace ecosystem)

**Hardware:** Google Colab T4 GPU (free tier)

**Training Time:** ~10 minutes for 200+ examples

### Hyperparameter Decisions

**Learning Rate:** 2e-5
This is the standard starting point for fine-tuning DistilBERT and works well for small datasets. Higher rates (e.g., 5e-5) risk destabilizing the pre-trained weights with limited data. Lower rates (e.g., 1e-5) might underfit on 200 examples. 2e-5 balances learning speed with stability.

**Epochs:** 3
3 epochs is a conservative choice that allows the model to see each example multiple times without memorizing noise.

**Batch Size:** 16
T4 GPU has 16GB VRAM, and a batch size of 16 is safe for DistilBERT while providing stable gradient estimates.

---

## Baseline Comparison

**Model:** Groq's llama-3.3-70b-versatile (zero-shot)

**Prompt:**
```
You are classifying TeamfightTactics subreddit posts into one of four categories:

1. discussion: Posts asking for opinions, seeking conversation, or exploring topics. Usually includes phrases like "what do you think" or "anyone else".

2. question: Posts seeking personal help, specific information, or clarification. Usually asks "what should I do" or "how do I" with a clear problem to solve.

3. user_feedback: Posts expressing opinions, complaints, or praise about game design, patches, or balance. Often contains emotional language or evaluation.

4. general_chat: Posts about achievements, memes, casual observations, or anything not fitting above.

Classify this post. Return only the label name (one of: discussion, question, user_feedback, general_chat) with no additional text or explanation.

Post: {post_text}
```

---

## Evaluation Plan

**When to Evaluate:**

1. Baseline zero-shot Groq on test set (before fine-tuning)
2. Fine-tuned DistilBERT on test set (after training)
3. During error analysis (review individual misclassifications)

**How to Evaluate:**

- Compare overall accuracy and per-class F1 scores side-by-side
- Analyze confusion matrix to identify confused label pairs
- Review confidence scores for correct and incorrect predictions
- Examine 3+ specific misclassified examples to diagnose failure modes
- Check if fine-tuned model exceeds baseline by at least 5-10%

**Metrics to Report:**

- Overall accuracy (both models)
- Per-class precision, recall, F1 (both models)
- Confusion matrix (fine-tuned model)
- Confidence calibration analysis (if doing stretch feature)

**Stored Outputs:** evaluation_results.json, confusion_matrix.png, sample_classifications.md
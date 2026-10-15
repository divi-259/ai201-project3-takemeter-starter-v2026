# Acceptance criteria — TakeMeter

Five criteria that say what "working" means for this classifier, written in
unit 5 **before** anything was trained.

**All five are yours this time.** None are given. You've had two projects of
practice.

An acceptance criterion names a number. *"The model is accurate"* is an
opinion. *"Every label has an F1 of at least 0.60 on the held-out set"* is a
criterion.

Under each, write a sentence or two on **why that number**. A reason that says
something about your data or your taxonomy earns credit — *"I picked 0.60 F1
for `reaction` because it's my smallest label and I only have about 50
examples of it"*. A reason that could be attached to any project does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## Pick numbers you can defend

Not numbers that sound impressive. Three labels means a coin-flip guesser gets
about 33%, so a target of 0.40 is barely a target. Your number should sit
somewhere you'd honestly call useful.

**Cover at least three of these five areas.** They're here as prompts, not as a
form to fill in — a criterion that fits none of them is fine if it names a
number.

| Area | A question it could answer |
|---|---|
| Overall accuracy | How often does it need to be right to be worth using? |
| Per-label performance | Is one label allowed to be much worse than the others? |
| Balance | How lopsided can your label counts get before it's a problem? |
| Consistency | If someone else labelled the same posts, how often should you agree? |
| Confidence | Should a confident prediction be right more often than an unsure one? |

Two things worth knowing before you pick numbers, because both will affect
whether you hit them:

- **Your smallest label will have the jumpiest score.** If a label has 50
  examples, about 8 land in the test split. An F1 computed on 8 examples moves
  a lot between seeds. A target for that label should be looser than one for
  your biggest label, and saying so is a good reason.
- **Unit 6 tests across three seeds, and the target has to hold across all
  three.** A target of 0.65 against results of 0.71, 0.62, 0.68 is a **miss**.
  Pick with that in mind — it is stricter than it first sounds.

---

## 1. Overall accuracy

<!-- Your criterion. It must name a number. -->

Accuracy on the held-out test set is at least 0.70 on all three seeds.

**Why this target:** With four labels, random guessing gets about 25%, and always guessing `hot_take` gets 30%. So 0.70 means the model is really reading the posts. I didn't go higher because the test set is only about 30 posts, so one wrong post changes accuracy by about 3 points.

---

## 2. Per-label performance

<!-- Your criterion. -->

On all three seeds, F1 is at least 0.70 for `complaint`, 0.60 for `hot_take` and `analysis`, and 0.55 for `advice`.

**Why this target:** `complaint` is the easiest to spot because it uses phrases like "I'm tired of". `hot_take` and `analysis` get a lower target because they are easy to confuse: the only difference is a hedge word or a reason. `advice` is my smallest label, with only about 5 posts in the test set, so its score will jump around the most.

---

## 3. Balance

<!-- Your criterion. -->

The largest label has no more than 2 times as many posts as the smallest label.

**Why this target:** Right now `hot_take` has 60 posts and `advice` has 35, which is 1.7 times. If `advice` gets much smaller, the model won't see enough examples to learn it. Its test score would also be based on too few posts to mean anything.

---

## 4. Consistency

<!-- Your criterion. -->

When I label the 30 staff posts, I agree with the staff labels on at least 80% of them (24 of 30).

**Why this target:** My definitions handle the confusing cases, but they can't cover everything. The staff definitions are also a bit different from mine, so a few disagreements are expected. If I agree less than 80% of the time, my own labels are probably not consistent enough to train on.

---

## 5. Confidence

<!-- Your criterion. -->

When the model is at least 80% confident, its prediction is right at least 80% of the time, on all three seeds.

**Why this target:** A confident prediction should be right more often than the 0.70 overall target. If it isn't, I can't use the confidence score to decide which predictions need a second look.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 6 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath, like this:

         ## 2. Every label performs acceptably

         The model performs well on all labels.

         **Why this target:** ...

         > **Revised in unit 6:** Every label has an F1 of at least 0.60 on
         > the held-out set.
         >
         > **Why revised:** "performs well" gave me nothing to check. I
         > couldn't produce a verdict from it at all.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "Overall accuracy of at least 0.65" → "at least 0.55", because
            0.65 turned out to be optimistic for 200 examples.

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->

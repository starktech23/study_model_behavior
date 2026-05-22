# Reasoning Evaluation Set (English) — 50 Prompts

**Design notes**

- **Coverage:** 13 reasoning types — deductive, quantitative, causal, analogical, counterfactual, spatial, temporal/sequential, commonsense, multi-step compositional, abductive, probabilistic, constraint satisfaction, and text inference.
- **Novelty:** Items are written fresh rather than drawn from public benchmarks (GSM8K, BBH, etc.) to reduce contamination. Memorized items inflate scores and collapse discrimination.
- **Difficulty mix:** A floor of easy items, a bulk of mid-difficulty, and several hard discriminators. ~10 items are adversarial traps where the intuitive answer is wrong; these are the most discriminative.
- **Grading:** Closed items have an exact `Expected`. Open items use a rubric — score on whether the listed reasoning elements appear, not on surface phrasing. For trap items, mark down any response that gives the intuitive-but-wrong answer even if the rest is fluent.

---

## Deductive logic

**1.** **Prompt:** All zorblats are quib. Some quib are not flerg. Can we conclude that some zorblats are not flerg?
**Expected:** No — invalid. The "quib that are not flerg" need not include any zorblats.
**Tests:** Formal validity vs. intuitive overlap. Trap item.

**2.** **Prompt:** On an island, knights always tell the truth and knaves always lie. You meet A and B. A says, "We are both knaves." What are A and B?
**Expected:** A is a knave, B is a knight. (If A were a knight the statement would be true, making A a knave — contradiction. So A lies; "both knaves" is false; since A is a knave, B must be a knight.)
**Tests:** Self-referential constraint resolution.

**3.** **Prompt:** No mammals are reptiles. All whales are mammals. Some pets are reptiles. Could a whale be a pet that is also a reptile?
**Expected:** No. A whale is a mammal, and no mammal is a reptile, so a whale cannot be a reptile regardless of pet status.
**Tests:** Multi-premise chaining; ignoring the irrelevant "pets" premise.

**4.** **Prompt:** If the alarm is set, the door is locked. The door is not locked. Is the alarm set?
**Expected:** No (modus tollens / contrapositive).
**Tests:** Valid conditional inference.

**5.** **Prompt:** If it rained, the grass is wet. The grass is wet. Did it rain?
**Expected:** Not necessarily — the grass could be wet from a sprinkler, dew, etc.
**Tests:** Affirming the consequent. Trap item.

---

## Quantitative

**6.** **Prompt:** A tank holds 240 liters and is 5/8 full. You add 30 liters, then drain 1/4 of the new total. How many liters remain?
**Expected:** 135. (150 + 30 = 180; drain 45 → 135.)
**Tests:** Ordered multi-step arithmetic.

**7.** **Prompt:** One printer prints 18 pages/min, another 12 pages/min. Working together, how long to print 450 pages?
**Expected:** 15 minutes (combined 30 pages/min).
**Tests:** Combined rates.

**8.** **Prompt:** A shirt costs $80. It is discounted 25%, then 10% tax is applied. What is the final price?
**Expected:** $66. (80 × 0.75 = 60; 60 × 1.10 = 66.)
**Tests:** Sequential percentage operations.

**9.** **Prompt:** Find the next number: 2, 6, 12, 20, 30, ___
**Expected:** 42. (Differences 4, 6, 8, 10, 12.)
**Tests:** Second-order pattern detection.

**10.** **Prompt:** How many distinct arrangements of the letters in "LEVEL" are there?
**Expected:** 30. (5! / (2!·2!) = 120 / 4.)
**Tests:** Permutations with repetition.

---

## Causal

**11.** **Prompt:** Ice cream sales and drowning deaths both rise in summer. Does ice cream cause drowning? Explain.
**Expected:** No — a confounder (hot weather → more swimming and more ice cream) drives both.
**Tests:** Confounder identification.

**12.** **Prompt:** Roosters crow before sunrise. If we stop a rooster from crowing, will the sun fail to rise? Why or why not?
**Expected:** The sun rises regardless. Dawn causes the crowing, not the reverse; the causal arrow is misread.
**Tests:** Causal direction.

**13.** **Prompt:** A study finds people who take vitamin X live longer. Give two non-causal explanations.
**Expected (rubric):** Any two of — healthy-user / self-selection bias, reverse causation, confounding by wealth/access, or measurement bias.
**Tests:** Generating alternative explanations.

**14.** **Prompt:** Why does salt melt ice on roads even when the temperature stays below 0°C?
**Expected:** Salt dissolves in the thin water film and lowers water's freezing point (freezing-point depression), so ice melts below 0°C.
**Tests:** Mechanistic explanation.

---

## Analogical

**15.** **Prompt:** Finger is to hand as leaf is to ___?
**Expected:** Branch or tree (part-to-whole). Accept either with correct relation.
**Tests:** Relation identification.

**16.** **Prompt:** A thermostat senses temperature and switches heating to hold a setpoint. Name a biological system that works on the same feedback principle and explain the mapping.
**Expected (rubric):** A valid negative-feedback system (body-temperature regulation, blood-glucose via insulin/glucagon) with sensor → comparator → effector mapping made explicit.
**Tests:** Structural (not surface) analogy.

**17.** **Prompt:** If a library is like a computer's hard drive, what is the librarian analogous to?
**Expected (rubric):** The indexing/retrieval layer — file system, OS, or search index. Reasoning about function matters more than the exact term.
**Tests:** Functional mapping.

---

## Counterfactual

**18.** **Prompt:** If humans had evolved with no sense of smell, name two everyday industries or products that likely would not exist.
**Expected (rubric):** Two defensible items — e.g., perfume/fragrance, scented products, possibly odorant additives in natural gas; wine/coffee tasting culture.
**Tests:** Downstream consequence reasoning.

**19.** **Prompt:** Suppose gravity were half as strong. With the same throw, would a ball travel farther or shorter horizontally? Explain.
**Expected:** Farther — lower downward acceleration means longer hang time, so it travels farther before landing.
**Tests:** Physics under altered premises.

**20.** **Prompt:** In a world where promises were physically impossible to break, would contracts and lawyers still be necessary? Explain.
**Expected (rubric):** Nuanced — enforcement need drops, but interpretation, ambiguity, scope, and dispute over meaning remain, so some legal/drafting role persists.
**Tests:** Reasoning about institutional purpose.

**21.** **Prompt:** If the wheel had never been invented, would powered flight still be possible? Reason through the dependencies.
**Expected (rubric):** Recognizes flight physics (lift/thrust) don't require wheels, but landing gear, manufacturing, and ground logistics historically do; concludes flight is conceivable but the development path changes. Credit for separating principle from implementation.
**Tests:** Dependency reasoning.

---

## Spatial

**22.** **Prompt:** A cube painted red on all faces is cut into 27 equal smaller cubes. How many small cubes have exactly two red faces?
**Expected:** 12 (the edge cubes, one per edge).
**Tests:** 3D decomposition.

**23.** **Prompt:** You face north. Turn 90° clockwise, then 180°, then 90° counterclockwise. Which way do you face?
**Expected:** South. (N → E → W → S.)
**Tests:** Cumulative rotation tracking.

**24.** **Prompt:** At 3:15, what is the angle between a clock's hour and minute hands?
**Expected:** 7.5°. (Minute at 90°; hour at 97.5°.)
**Tests:** Continuous-motion spatial reasoning. Trap (intuitive answer is 0°).

**25.** **Prompt:** Standing at a point, you walk 10 m north, then 10 m east. How far are you from the start in a straight line?
**Expected:** ≈14.14 m (√200).
**Tests:** Pythagorean displacement.

---

## Temporal / sequential

**26.** **Prompt:** A is before B. C is after B. D is before A. Order all four earliest to latest.
**Expected:** D, A, B, C.
**Tests:** Ordering from partial constraints.

**27.** **Prompt:** A meeting is at 2:00 PM in New York. London is 5 hours ahead. What time is it in London? (Use the given offset; ignore DST.)
**Expected:** 7:00 PM.
**Tests:** Offset arithmetic with stated assumptions.

**28.** **Prompt:** It takes 3 machines 3 hours to make 3 widgets. How long for 100 machines to make 100 widgets?
**Expected:** 3 hours (each machine makes 1 widget in 3 hours).
**Tests:** Rate normalization. Trap (intuitive answer is 100).

**29.** **Prompt:** If today is Wednesday, what day is it 100 days from now?
**Expected:** Friday. (100 mod 7 = 2.)
**Tests:** Modular date arithmetic.

---

## Commonsense

**30.** **Prompt:** You put a cake in a 350°F oven for 30 minutes, then realize after 10 minutes you forgot the sugar. Can you fix it without starting over? Why or why not?
**Expected:** Practically no — the batter has set/begun cooking; sugar can't be mixed in evenly, so you'd need to restart.
**Tests:** Physical-process commonsense.

**31.** **Prompt:** Why might someone keep an umbrella in their car even on a sunny day?
**Expected (rubric):** Plausible reasons — weather can change, preparedness, sun shade, it was left there. Credit for sensible inference.
**Tests:** Plausible-explanation generation.

**32.** **Prompt:** A glass of water sits on a table in a warm room for a week. What happens and why?
**Expected:** Water level drops via evaporation; possibly dust/film on the surface.
**Tests:** Everyday physics.

**33.** **Prompt:** Two people are in a room. One says "It's cold," and the other immediately stands up. What is the second person most likely about to do, and why?
**Expected (rubric):** Adjust thermostat, close a window, or fetch a blanket — interpreting the remark as an indirect request.
**Tests:** Pragmatic + commonsense inference.

---

## Multi-step compositional

**34.** **Prompt:** A recipe for 4 people needs 600 g flour and 3 eggs. For 10 people, how much flour and how many whole eggs are required?
**Expected:** 1500 g flour and 8 eggs. (Scale ×2.5: 1500 g; 7.5 eggs → round up to 8.)
**Tests:** Scaling with rounding judgment.

**35.** **Prompt:** With a 3-liter and a 5-liter jug and unlimited water, measure exactly 4 liters. Give the steps.
**Expected:** Fill 5 → pour into 3 (2 left in 5) → empty 3 → pour the 2 into 3 → fill 5 → top off the 3 (uses 1) → 4 liters remain in the 5-liter jug.
**Tests:** State-search planning.

**36.** **Prompt:** A train leaves Station A at 60 km/h. Two hours later a second train leaves A at 90 km/h on the same track. How far from A does it catch the first?
**Expected:** 360 km. (120 km head start; closing speed 30 km/h → 4 hours → 90 × 4.)
**Tests:** Relative-motion catch-up.

**37.** **Prompt:** Five houses in a row. Red is immediately left of Blue. Green is somewhere right of Blue. Yellow is first. White is not adjacent to Yellow. Give one valid ordering.
**Expected:** Yellow, Red, Blue, Green, White.
**Tests:** Constraint integration.

**38.** **Prompt:** A snail climbs a 10 m well: up 3 m each day, sliding back 2 m each night. On which day does it reach the top?
**Expected:** Day 8. (Net 1 m/day until day 8, when it climbs from 7 m to 10 m and exits before sliding.)
**Tests:** Boundary-condition reasoning. Trap (intuitive answer is 10).

---

## Abductive

**39.** **Prompt:** You come home to a wet floor, an open window, the cat hiding, and a clear sky. What is the most likely explanation?
**Expected (rubric):** Since the sky is clear (rain unlikely), the best inference is a knocked-over container of water that startled the cat — not rain through the window. Credit for using the clear-sky cue.
**Tests:** Inference to the best explanation; cue integration.

**40.** **Prompt:** Someone reports fatigue, weight gain, cold sensitivity, and dry skin. What single underlying cause plausibly explains all four?
**Expected:** Hypothyroidism (low thyroid function). (Reasoning exercise, not medical advice.)
**Tests:** Convergent single-cause inference.

**41.** **Prompt:** Your code worked yesterday and fails today though you changed nothing. Give three plausible explanations, ranked by likelihood.
**Expected (rubric):** Sensible ranked hypotheses — e.g., a dependency/environment update, an external API or data change, or a change made by someone else / machine state. Credit for ranking, not just listing.
**Tests:** Hypothesis generation and ranking.

---

## Probabilistic

**42.** **Prompt:** A bag has 3 red and 2 blue marbles. You draw two without replacement. Probability both are red?
**Expected:** 3/10. (3/5 × 2/4.)
**Tests:** Dependent-event probability.

**43.** **Prompt:** A disease affects 1 in 1000. A test is 99% accurate both ways. You test positive. Roughly what is the chance you actually have it?
**Expected:** About 9%. (≈ 0.00099 / 0.01098.)
**Tests:** Base-rate neglect. Strong discriminator.

**44.** **Prompt:** You flip a fair coin five times and get five heads. What is the probability the next flip is heads?
**Expected:** 1/2 — flips are independent.
**Tests:** Gambler's fallacy. Trap item.

**45.** **Prompt:** Rolling two dice, which is more likely — a sum of 7 or a sum of 10 — and by how much?
**Expected:** 7 is twice as likely (6/36 vs. 3/36).
**Tests:** Enumerating sample space.

---

## Constraint satisfaction

**46.** **Prompt:** Order three tasks A, B, C such that A comes before C and B is not first. List all valid orderings.
**Expected:** ABC and ACB.
**Tests:** Exhaustive enumeration under constraints.

**47.** **Prompt:** Five friends sit in a row. Sam won't sit next to Pat, and Lee must sit in the middle. Give one valid seating.
**Expected:** Any arrangement with Lee in seat 3 and Sam/Pat non-adjacent, e.g., Sam, Kim, Lee, Jo, Pat.
**Tests:** Satisfiability + example construction.

**48.** **Prompt:** Pack items of weight 4, 3, 3, 2, 1 into bins of capacity 6, minimizing bins. State the minimum and one packing.
**Expected:** 3 bins — e.g., (4+2), (3+3), (1).
**Tests:** Bin-packing / optimization reasoning.

---

## Text inference

**49.** **Prompt:** "Although the bridge had been condemned years ago, the children still used it daily." What can you infer, and what is the tension in this sentence?
**Expected (rubric):** Infers the bridge is officially unsafe yet still in use — pointing to neglect, lack of alternatives, or unenforced rules. Names the tension between official status and lived reality.
**Tests:** Inference beyond the literal.

**50.** **Prompt:** "She returned the gift unopened." Give three reasons, each implying a different relationship between giver and receiver.
**Expected (rubric):** Three distinct interpretations — e.g., rejection/anger (estranged), principled refusal (conflict-of-interest / professional), or a mistaken recipient (no real relationship). Credit for genuinely different relational implications.
**Tests:** Generating distinct interpretations.

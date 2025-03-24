# AI Tutor Simulation

A simple simulation of an **AI-powered tutor** interacting with a student over a session of 50 questions. The model tracks how the **student's skill evolves**, and how the **AI is rewarded or penalized** based on the difficulty of questions it selects and how much the student improves.

This is **not a reinforcement learning agent (yet)** — it's a controlled simulation that lays the foundation for more advanced AI tutor experiments, including RL-based policy learning.

---

## Motivation

The goal is to understand how an AI tutor could:
- Adaptively select questions of varying difficulty
- Promote student learning without relying too heavily on easy questions
- Receive feedback (rewards) for teaching performance

This mirrors real educational settings, where **over-challenging or under-challenging a student** both lead to poor outcomes.

---

## Simulation Logic

At each time step (question):
- The AI selects a question of either **easy (1)** or **hard (2)** difficulty
- The student attempts the question, with success probability based on current **skill level**
- The student's skill is updated based on success/failure, difficulty, forgetting, and AI behavior
- The AI receives a **reward** for student improvement, and a **penalty** if it overuses easy questions

---

## Student Skill Update Equation

Let:
- `α` = learning rate  
- `β` = forgetting rate  
- `γ` = penalty for repeated easy questions  
- `r` = reward from the current question  
- `d` = difficulty (1 = easy, 2 = hard)

Then the skill is updated as:

skill[t+1] = skill[t] + α * (r * d) - β * d - penalty


Where:
- `r = 5` if the student got a hard question correct  
- `r = 1` if the student got an easy question correct  
- `r = -1` if the student answered incorrectly  
- `penalty = γ` if the AI gives more than 3 easy questions in a row, otherwise 0

Skill is clamped to be non-negative.

---

## AI Reward Function

The AI receives a reward at each step:

AI_reward[t] = r - penalty


This encourages the AI to:
- Push the student to improve
- Avoid "gaming the system" by only giving easy questions

---

## Outputs

- `AI_Tutor_Results.csv`: Logs each question's result, skill level, AI reward
- A line chart that shows:
  - Student skill progression
  - Cumulative AI reward over time

---

## Adjustable Parameters

| Parameter       | Meaning                                      |
|-----------------|----------------------------------------------|
| `alpha`         | Learning rate (how fast the student learns)  |
| `beta`          | Forgetting rate (how fast skill decays)      |
| `gamma`         | Penalty for streaks of easy questions        |
| `num_questions` | Total number of questions in the simulation  |


---

## Future Work

- Introduce a **learned policy** (e.g., ε-greedy, softmax)  
- Simulate **multiple students** with different learning curves  
- Track **long-term retention**, not just short-term skill gain

---

## License

MIT License

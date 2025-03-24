
AI Tutor Simulation

A simple simulation of an AI-powered tutor interacting with a student over a session of 50 questions. The model tracks how the student's skill evolves over time, and how the AI is rewarded or penalized based on the difficulty of questions it selects and how much the student improves.

This is not a reinforcement learning agent (yet)—it's a controlled simulation that lays the foundation for more advanced AI tutor experiments, including RL-based policy learning.
Motivation

The goal is to understand how an AI tutor could:

    Adaptively select questions of varying difficulty

    Promote student learning without relying too heavily on easy questions

    Receive feedback (rewards) for teaching performance

This mirrors real educational settings, where over-challenging or under-challenging a student both lead to poor learning outcomes.
Simulation Logic

At each time step (question):

    The AI selects a question of either easy (1) or hard (2) difficulty.

    The student attempts the question, with success probability based on current skill level.

    The student's skill is updated based on success/failure, difficulty, forgetting, and AI behavior.

    The AI receives a reward for student improvement and is penalized for overusing easy questions.
Student Skill Update Equation

Let:

    αα = learning rate

    ββ = forgetting rate

    γγ = AI penalty for too many easy questions

    rr = reward from current question

    dd = difficulty level (1 = easy, 2 = hard)

Then the skill update equation is:
skillt+1=skillt+α⋅(r⋅d)−β⋅d−penalty
skillt+1​=skillt​+α⋅(r⋅d)−β⋅d−penalty

Where:

    r={+5if correct and hard+1if correct and easy−1if incorrectr=⎩

⎨

    ⎧​+5+1−1​if correct and hardif correct and easyif incorrect​

    Penalty =γ=γ if the AI has chosen more than 3 easy questions in a row, otherwise 0.

Skill is clamped to be non-negative.
AI Reward Equation

The AI receives a per-question reward:
AI_rewardt=r−penalty
AI_rewardt​=r−penalty

This encourages the AI to:

    Push the student to improve

    Avoid overusing easy questions (which might inflate accuracy but hinder growth)

Outputs

    AI_Tutor_Results.csv: Logs student skill, AI reward, and question number

    Line chart comparing student skill vs. AI cumulative reward over time

    Per-step reward deltas also computed

Example Visualization

Adjustable Parameters
Parameter	Description
alpha	Learning rate (how fast skill improves)
beta	Forgetting rate (how fast skill decays)
gamma	AI penalty for repeating easy questions
num_questions	Number of questions in the simulation
Future Directions

    Replace random question selection with a learned policy

    Extend to multiple students with different learning curves

    Turn this into a true reinforcement learning environment using OpenAI Gym interface

    Track metrics like long-term retention, not just short-term skill gain

📜 License

MIT License

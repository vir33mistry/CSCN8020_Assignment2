# CSCN8020 Assignment 2 — Taxi Gymnasium Environment with Q-Learning

**Student Name:** Viraj Mistry  
**Student ID:** [Replace with your student ID]  
**Course:** CSCN8020 — Reinforcement Learning Programming  
**Assignment:** Assignment 2 — Taxi Gymnasium Environment with Q-Learning  

## GitHub Repository

Repository URL: <https://github.com/viraj231259/CSCN8020_Assignment2>  
Cloneable URL: <https://github.com/viraj231259/CSCN8020_Assignment2.git>

## Project Summary

This project implements the **Q-Learning algorithm** on the Taxi Gymnasium environment. The goal is to train an agent to move through the Taxi environment, pick up the passenger, and drop the passenger off at the correct destination. The implementation uses a tabular Q-table, epsilon-greedy exploration, temporal-difference updates, reward tracking, steps-per-episode tracking, hyperparameter experiments, and final policy evaluation.

The notebook is written using an object-oriented structure so that environment handling, agent behavior, training, metric collection, plotting, experiment execution, and logging are separated clearly.

## Environment

The project uses the Gymnasium Taxi environment. The notebook first tries to create:

```python
Taxi-v4
```

If Taxi-v4 is not available, the code can fall back to Taxi-v3, depending on the installed Gymnasium version.

The Taxi environment has:

- **500 discrete states**
- **6 discrete actions**
- Rewards:
  - `-1` for each normal step
  - `+20` for successful passenger delivery
  - `-10` for illegal pickup or drop-off

## Action Space

| Action | Meaning |
|---:|---|
| 0 | Move south |
| 1 | Move north |
| 2 | Move east |
| 3 | Move west |
| 4 | Pick up passenger |
| 5 | Drop off passenger |

## Q-Learning Method

The project uses the following Q-Learning update rule:

```text
Q(S,A) = Q(S,A) + alpha * [R + gamma * max Q(S',a) - Q(S,A)]
```

Where:

- `Q(S,A)` is the current action-value estimate
- `alpha` is the learning rate
- `R` is the reward received
- `gamma` is the discount factor
- `S'` is the next state
- `max Q(S',a)` is the best estimated future action value

The agent uses **epsilon-greedy exploration**, meaning it sometimes explores random actions and otherwise chooses the current best action from the Q-table.

## Object-Oriented Design

The notebook includes meaningful classes to separate responsibilities:

| Class | Responsibility |
|---|---|
| `TaxiEnvironmentManager` | Creates and manages the Taxi Gymnasium environment |
| `QLearningAgent` | Stores the Q-table, selects actions, and applies Q-learning updates |
| `QLearningTrainer` | Runs the training loop for each experiment |
| `MetricsLogger` | Tracks returns, steps, and experiment metrics |
| `PlotManager` | Generates required plots |
| `ExperimentRunner` | Runs baseline, hyperparameter experiments, and best-combination experiment |

## Baseline Hyperparameters

The baseline experiment uses the required hyperparameters:

| Hyperparameter | Value |
|---|---:|
| Learning rate `alpha` | 0.1 |
| Exploration factor `epsilon` | 0.1 |
| Discount factor `gamma` | 0.9 |
| Episodes | 3000 |
| Max steps per episode | 200 |

## Hyperparameter Experiments

The notebook tests the required hyperparameter changes separately.

### Learning Rate Experiments

| Experiment | Alpha | Epsilon | Gamma |
|---|---:|---:|---:|
| Baseline | 0.1 | 0.1 | 0.9 |
| Alpha experiment 1 | 0.01 | 0.1 | 0.9 |
| Alpha experiment 2 | 0.001 | 0.1 | 0.9 |
| Alpha experiment 3 | 0.2 | 0.1 | 0.9 |

### Exploration Factor Experiments

| Experiment | Alpha | Epsilon | Gamma |
|---|---:|---:|---:|
| Baseline | 0.1 | 0.1 | 0.9 |
| Epsilon experiment 1 | 0.1 | 0.2 | 0.9 |
| Epsilon experiment 2 | 0.1 | 0.3 | 0.9 |

## Best Combination Experiment

Based on the experiment results, the selected best combination is:

| Hyperparameter | Value |
|---|---:|
| Learning rate `alpha` | 0.2 |
| Exploration factor `epsilon` | 0.1 |
| Discount factor `gamma` | 0.9 |

This combination was selected because the higher learning rate helped the agent improve faster while keeping exploration controlled with epsilon equal to 0.1.

## Training Metrics

The notebook reports the required training metrics:

- Total episodes
- Steps taken per episode
- Average return per episode
- Mean return over time
- Mean steps over time
- Best return
- Final evaluation interpretation

The notebook also saves experiment results into:

```text
outputs/experiment_results.csv
```

## Plots Generated

The notebook creates plots to support the training observations, including:

- Total reward or return per episode
- Steps taken per episode
- Average return over time
- Hyperparameter experiment comparison plot

The plots are saved in the `outputs/` folder.

## Logging

The project includes a log file:

```text
assignment2_execution.log
```

The log file records:

- Notebook start
- Taxi environment creation
- Experiment names
- Selected hyperparameters
- Training progress at reasonable episode intervals
- Final metrics for each experiment

## Major Files in the Repository

```text
CSCN8020_Assignment2/
│
├── CSCN8020_Assignment2.ipynb
├── CSCN8020_Assignment2_One_Page_Submission.pdf
├── README.md
├── requirements.txt
├── .gitignore
├── assignment2_execution.log
├── SUBMISSION_CHECKLIST.md
│
└── outputs/
    ├── experiment_results.csv
    ├── hyperparameter_experiment_comparison.png
    └── experiment training plots
```

## How to Run the Project

### 1. Clone the repository

```bash
git clone https://github.com/viraj231259/CSCN8020_Assignment2.git
cd CSCN8020_Assignment2
```

### 2. Create a virtual environment

Windows PowerShell:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

macOS/Linux:

```bash
python -m venv .venv
source .venv/bin/activate
```

### 3. Install requirements

```bash
pip install -r requirements.txt
```

### 4. Run the notebook

```bash
jupyter notebook CSCN8020_Assignment2.ipynb
```

Then open the notebook and run all cells from top to bottom.

## Requirements

The required packages are listed in `requirements.txt`. Main packages include:

```text
gymnasium
numpy
pandas
matplotlib
jupyter
```

## Notes for Submission

Before submitting, make sure:

- The notebook runs from top to bottom without errors.
- `assignment2_execution.log` is included.
- The `outputs/` folder includes the required plots and metrics file.
- The one-page PDF includes the correct student ID and GitHub links.
- The GitHub repository is public or accessible to the instructor.
- The cloneable URL ends with `.git`.
- The virtual environment folder `.venv/` is **not uploaded**.

## Academic Integrity and AI-Use Acknowledgement

I used course materials, assignment instructions, Gymnasium documentation, and AI support to help structure, debug, and explain the solution. I reviewed and tested the notebook to ensure that I understand the Q-Learning implementation, the experiment results, and the written explanations.

## Final Conclusion

This project demonstrates how Q-Learning can train an agent in the Taxi Gymnasium environment through reinforcement learning. The agent learns by interacting with the environment, receiving rewards and penalties, updating Q-values, and improving its policy over time. The hyperparameter experiments show how learning rate and exploration factor affect training performance.

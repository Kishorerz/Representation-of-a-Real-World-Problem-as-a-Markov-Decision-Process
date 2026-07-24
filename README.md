# Representation of a Real-World Problem as a Markov Decision Process

## Aim

To represent a Smart Irrigation System as a Markov Decision Process (MDP) by defining its states, actions, transition probabilities, reward function, graphical representation, and Python implementation.

---

# Problem Statement

## Problem Description

Agriculture consumes a significant amount of freshwater, making efficient irrigation essential for sustainable farming. A Smart Irrigation System uses soil moisture sensors and weather forecasts to determine whether crops should be irrigated. At each decision step, the system observes the current soil condition and weather, then decides whether to irrigate, wait, or apply partial irrigation.

The objective is to maintain optimal soil moisture while minimizing water consumption and preventing overwatering. Since the next condition of the field depends only on the current state and the action taken, this problem can be modeled as a Markov Decision Process (MDP).

---

# MDP Components

A Markov Decision Process is represented as:

**MDP = (S, A, P, R, γ)**

Where:

| Symbol | Meaning                         |
| ------ | ------------------------------- |
| **S**  | Set of states                   |
| **A**  | Set of actions                  |
| **P**  | Transition probability function |
| **R**  | Reward function                 |
| **γ**  | Discount factor                 |

---

# State Space

The state space represents all possible environmental conditions observed by the irrigation controller.

```text
S = {
    S1: Dry Soil, Sunny,
    S2: Dry Soil, Rain Expected,
    S3: Moderately Moist Soil, Sunny,
    S4: Moderately Moist Soil, Rain Expected,
    S5: Wet Soil, Sunny,
    S6: Wet Soil, Rain Expected
}
```

---

# Sample State

```text
S2 = (Dry Soil, Rain Expected)
```

In this state, the soil is dry, but rain is expected soon. The controller must decide whether to irrigate immediately or wait for rainfall.

---

# Action Space

The irrigation controller can perform one of the following actions:

```text
A = {
    A1: Start Irrigation,
    A2: Stop Irrigation,
    A3: Wait,
    A4: Partial Irrigation
}
```

---

# Sample Action

```text
A1 = Start Irrigation
```

The controller starts watering the crops because the soil is dry and rainfall is not sufficient.

---

# Transition Probability

The transition probability describes the likelihood of moving from one state to another after performing an action.

General form:

```text
P(s' | s, a)
```

Examples:

* If the current state is **Dry Soil, Sunny** and the action is **Start Irrigation**, there is a high probability of moving to **Moderately Moist Soil, Sunny**.
* If the current state is **Moderately Moist Soil, Rain Expected** and the action is **Wait**, rainfall may naturally move the system to **Wet Soil, Rain Expected**.
* If the current state is **Wet Soil, Sunny** and the action is **Stop Irrigation**, evaporation may eventually lead to **Moderately Moist Soil, Sunny**.

Example probabilities:

```text
P(S3 | S1, Start Irrigation) = 0.9
P(S5 | S4, Wait) = 0.8
P(S3 | S5, Stop Irrigation) = 0.7
```

---

# Reward Function

The reward function provides feedback after every action.

General form:

```text
R(s, a, s')
```

Example rewards:

| Action                            | Reward |
| --------------------------------- | ------ |
| Efficient irrigation              | +10    |
| Water saved by waiting for rain   | +8     |
| Maintaining optimal soil moisture | +15    |
| Overwatering                      | -10    |
| Underwatering                     | -15    |
| Wasting water                     | -8     |

The objective is to maximize the total accumulated reward while maintaining healthy crop conditions.

---

# Graphical Representation

<img width="1536" height="1024" alt="ChatGPT Image Jul 24, 2026, 03_16_48 PM" src="https://github.com/user-attachments/assets/7b02c10d-db42-4fee-9760-6ffae21f5784" />


States are represented as nodes, while actions, rewards, and transitions are represented as directed edges.

---

# Python Representation

```python
# MDP Representation using Python

print("Name: Kishor")
print("Register Number: ____________")

states = {
    "S1": "Dry Soil, Sunny",
    "S2": "Dry Soil, Rain Expected",
    "S3": "Moderately Moist Soil, Sunny",
    "S4": "Moderately Moist Soil, Rain Expected",
    "S5": "Wet Soil, Sunny",
    "S6": "Wet Soil, Rain Expected"
}

actions = [
    "Start Irrigation",
    "Stop Irrigation",
    "Wait",
    "Partial Irrigation"
]

transition_probability = {
    ("S1", "Start Irrigation"): {"S3": 0.9, "S5": 0.1},
    ("S2", "Wait"): {"S5": 0.8, "S3": 0.2},
    ("S5", "Stop Irrigation"): {"S3": 0.7, "S5": 0.3},
    ("S3", "Wait"): {"S4": 0.6, "S3": 0.4}
}

rewards = {
    ("S1", "Start Irrigation", "S3"): 10,
    ("S2", "Wait", "S5"): 15,
    ("S5", "Stop Irrigation", "S3"): 5,
    ("S3", "Wait", "S4"): 2
}

discount_factor = 0.9

print("\nStates:")
for key, value in states.items():
    print(f"{key}: {value}")

print("\nActions:")
for action in actions:
    print("-", action)

print("\nDiscount Factor:", discount_factor)
```

---

# Output
### States
<img width="332" height="229" alt="Screenshot 2026-07-24 151333" src="https://github.com/user-attachments/assets/c03b62b0-b234-4cc5-843f-7a930980530e" /> </br>
### P
<img width="359" height="445" alt="Screenshot 2026-07-24 151321" src="https://github.com/user-attachments/assets/92b0a215-dd3b-47f7-9c5f-66a5b1f56327" /></br>
### Actions
<img width="237" height="115" alt="Screenshot 2026-07-24 151313" src="https://github.com/user-attachments/assets/4e4c62ef-fad0-4c5d-aa3d-8fd516ae5aa6" /></br>


---

# Result

The Smart Irrigation System was successfully modeled as a Markov Decision Process by defining its states, actions, transition probabilities, reward function, and Python representation. This MDP model can be used as the foundation for reinforcement learning algorithms that optimize irrigation decisions while conserving water and maintaining healthy crop growth.

GitHub's README files support Markdown, not LaTeX. However, you can convert your LaTeX content to Markdown using GitHub-supported syntax, Unicode for math symbols, and fenced code blocks for Python. Here's how to structure the README-friendly version:

---

## 📘 **The Utilization of Transition Matrices and Population Vectors in Modelling Population Change**

**Course**: Math 201, Spring 2025
**Supervised by**: *Dr. Waleed Abdelmeguid*

**Prepared by**:

* Haneen Mehrez – 202301279
* Yasmin Gamal – 202300839
* Sama Samy – 202300533
* Salma Badr – 202302287

---

### 📄 Abstract

This project develops a population model using a transition matrix and a population vector implemented in Python. The Markov chain approach is used to predict how the population changes over time using demographic statistics.

### 📚 Introduction

Transition matrices and state (population) vectors simulate population dynamics:

* **Transition matrix**: Probability of moving between age groups.
* **Population vector**: Number of individuals in each age group.

This model helps predict population trends and supports decisions in planning for healthcare, education, and infrastructure.

### 📐 Theoretical Background

#### Population Vector:

```
P(t) = [
  children(t)
  adults(t)
  elderly(t)
]
```

General form:

```
P(t) = [
  P₁(t)
  P₂(t)
  ...
  Pₙ(t)
]
```

#### Transition Matrix:

```
A = [
  birth_rate     adult→child     elder→child
  child→adult    stay_adult      elder→adult
  0              adult→elder     stay_elder
]
```

Matrix multiplication rule:

```
P(t+1) = A × P(t)
```

#### Markov Chain Definition

A Markov chain is a process where the next state depends only on the current state:

```
P(Xₜ₊₁ = j | Xₜ = i) = pᵢⱼ
```

The **t-step transition**:

```
P(Xₜ = j | X₀ = i) = (Pᵗ)ᵢⱼ
```

#### Distribution Over Time:

Let `v` be the initial distribution:

```
X₀ ~ vᵀ
X₁ ~ vᵀ P
X₂ ~ vᵀ P²
...
Xₜ ~ vᵀ Pᵗ
```

Example:

```
P = [
  0.7  0.3
  0.4  0.6
]

v₀ = [1  0]

v₁ = v₀ × P = [0.7  0.3]

v₅ = v₀ × P⁵
```

---

## 🛠️ Application

### User Guide

**Key Features**:

1. Input population sizes.
2. Input transition matrix using percentages.
3. Simulate for multiple years.

**Important**: Percentages per group must total ≤ 100%.

---

## 💻 Python Code

<details>
<summary>Click to view code</summary>

```python
import numpy as np

def get_population_vector():
    print("Enter initial population sizes:")
    children = float(input("Children: "))
    adults = float(input("Adults: "))
    elderly = float(input("Elderly: "))
    return np.array([children, adults, elderly])

def get_transition_matrix():
    print("Enter transition matrix (as percentages, 0-100):")
    matrix = np.zeros((3, 3))
    for j in range(3):
        for i in range(3):
            matrix[i, j] = float(input(f"From group {j} to group {i}: ")) / 100
    return matrix

def simulate_population(initial_pop, trans_matrix, steps):
    pop = initial_pop.copy()
    for t in range(steps):
        pop = np.dot(trans_matrix, pop)
        print(f"Year {t+1}: {pop}")
    return pop

def main():
    print("Markov Chain Population Model")
    pop_vector = get_population_vector()
    trans_matrix = get_transition_matrix()
    steps = int(input("Years to simulate: "))
    simulate_population(pop_vector, trans_matrix, steps)

if __name__ == "__main__":
    main()
```

</details>

---

## 📎 References

* [Fewster, R. Chapter 8: Markov chains](https://www.stat.auckland.ac.nz/~fewster/325/notes/ch8.pdf) - University of Auckland

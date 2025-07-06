## 📘 **The Utilization of Transition Matrices and Population Vectors in Modelling Population Change**

**Course**: Math 201, Spring 2025
**Supervised by**: *Dr. Waleed Abdelmeguid*

**Prepared by**:

* Sama Samy
* Haneen Mehrez
* Salma Badr
* Yasmin Gamal

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

## 📎 References

* [Fewster, R. Chapter 8: Markov chains](https://www.stat.auckland.ac.nz/~fewster/325/notes/ch8.pdf) - University of Auckland

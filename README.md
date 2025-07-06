
\documentclass{article}
\usepackage{graphicx} % Required for inserting images
\usepackage{amsmath}
\usepackage{xcolor}
\title{\textbf{The Utilization of Transition Matrices and Population Vectors in Modelling Population Change} }
\date{Math 201, Spring 2025}
\usepackage{xcolor}
\usepackage{listings}

\lstset{
  language=Python,
  basicstyle=\ttfamily\small,
  keywordstyle=\color{blue},
  stringstyle=\color{magenta},
  commentstyle=\color{gray},
  numbers=left,
  numberstyle=\tiny\color{gray},
  stepnumber=1,
  numbersep=10pt,
  frame=single,
  breaklines=true,
  showstringspaces=false,
  tabsize=4
}
\begin{document}
\begin{figure}[t]
    \centering
    \includegraphics[width=0.4\textwidth]{Zewail-City.png}
\end{figure}
\maketitle
\begin{center}
\textit{Under the supervision of: Dr. Waleed Abdelmeguid}
\vspace{1cm}
\author{Prepared by:\\ Haneen Mehrez \hspace{1cm} 202301279\\ \vspace{0.5cm} Yasmin Gamal \hspace{1cm} 202300839\\ \vspace{0.5cm} Sama Samy \hspace{1.4cm} 202300533\\ \vspace{0.5cm} Salma Badr \hspace{1.4cm} 202302287}
\vspace{2cm}
\newpage
\end{center}
\section{Abstract}
This project focuses on developing a population model using a transition matrix and a population vector, implemented in Python. The model will allow users to input the relevant demographic statistics for their country. The transition matrix will show how people move between age groups over time, while the population vector will represent the number of individuals in each group. This project aims to predict population changes over the years.

In our population model, the Markov chain will be used to predict the population change over a course of time \( t \), if given the number of individuals in each group represented by the vector population \( v \) and the transition matrix, where each element represents the probability of transitioning between age groups. The Markov chain is specifically useful as it only needs the current state \( v \) to predict the future \( v_{t+1} \).

\section{Introduction}
It is important to understand and predict population changes over the years for effective planning in countries to control healthcare, education, and economic development. Through our project, we focus on building mathematical models to simulate population dynamics using a transition matrix and a population vector. \textbf{Transition matrix}:  Represents how elements of a system change in different periods or states. Each entry in the matrix expresses the probability or rate of transition from one state to another. \textbf{State vector}: Each value represents a quantity associated with a specific state or group in the system. In our project, a transition matrix shows how individuals move from one age group to another over time, and the state vector is represented as a population vector, a column of numbers showing how many people are in each age group at the current time.
Both the transition matrix and the population vector help countries predict future population sizes and model demographic changes such as ageing, mortality, and birth rates.
\section{Thoerm}
\subsection{Theory intersection }
\textbf{Population modelling} is a way to understand how the age groups of a population change over time. Rather than trying to follow every individual. The population is divided into 3 age groups [0–14 years (children),  15–64 years (adults), 65+ years (elderly)].
The number of people in each age group at a given time can be represented as a vector.
\textbf{\large The population vector} is defined as:

\[
\mathbf{P}(t) =
\begin{bmatrix}
\text{children}(t) \\
\text{adults}(t) \\
\text{elderly}(t)
\end{bmatrix}
\]

That is, \( \mathbf{P}(t) \in \mathbb{R}^n \) is the population vector at time \( t \), where each entry \( P_i(t) \) represents the number of individuals in age group \( i \).

In general form, the population vector is written as:

\[
\mathbf{P}(t) =
\begin{bmatrix}
P_1(t) \\
P_2(t) \\
\vdots \\
P_n(t)
\end{bmatrix}
\]

Each row corresponds to a specific age group, and the value in each row represents the number of people in that group at time \( t \). \vspace{1cm}
\\  A \textbf{\large transition matrix} tells us how individuals move between age groups from one year to the next. Over time, the population distribution changes: children may become adults, adults may become elderly, and some individuals in each group may die. In addition, new children are born.

Let \( A \in \mathbb{R}^{n \times n} \) be the \textbf{transition matrix}, where each element \( a_{ij} \) represents the fraction of individuals in group \( j \) who will move to group \( i \) in the next time step. 

- Each \textbf{row} of \( A \) corresponds to an age group at time \( t+1 \).
- Each \textbf{column} of \( A \) corresponds to an age group at time \( t \).
- Thus, \( A \) transforms the population vector at time \( t \) into the population vector at time \( t+1 \):
\[
\mathbf{P}(t+1) = A\mathbf{P}(t)
\]

Conceptual form of \( A \):

\[
A =
\begin{bmatrix}
\text{birth rate} & \text{adult to child} & \text{elder to child} \\
\text{child to adult} & \text{stay adult} & \text{elder to adult} \\
0 & \text{adult to elder} & \text{stay elder}
\end{bmatrix}
\]

General symbolic form of \( A \):

\[
A =
\begin{bmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{n1} & a_{n2} & \cdots & a_{nn}
\end{bmatrix}
\]
\subsection{The Markov chain}
A \textbf{Markov chain} is a stochastic process  $X_0, X_1, X_2...X_n$ in which the future state $X_{t+1}$ depends only on the current state $X_t$ and not on the full history. The process is a Markov chain if this property holds true:
\[
P(X_{t+1} = x_{t+1} \mid X_t = x_t, X_{t-1} = x_{t-1}, \ldots, X_0 = x_0) = P(X_{t+1} = x_{t+1} \mid X_t = x_t)
\]
The \textbf{state space} of a Markov chain S is the set of values that $X_t$ can take. While the \textbf{trajectory} is the set of values for $X_0, X_1, X_2...X_n$.
The set of possible probabilities \textit{P} can be written in a matrix form called the \textbf{Transition Matrix} where \textit{P= $p_{ij}$}
 In the transition matrix \textit{P}:
 \newline• the R rows represent $X_t$ or the current state;
  \newline• the columns represent $X_{t+1}$, or the future state;
  \newline• entry $(i,j)$ is the probability that the future state = $j$, given that the current state =$i$.
 \[
 P_{ij}= P(X_{t+1}=j | X_t= i)
 \]
 By taking into consideration that the rows of \textbf{P} summation must = 1, ensuring that all possible future probabilities will sum up to 1, maintaining the requirement for valid probability distributions.
 \[
 \sum_{k=1}^{N} p_{ij} = \sum_{j=1}^{N} P(X_{t+1}=j | X_{t}= i) = 1
 \]
 \subsection{ The t-step transition probabilities}
 \textit{$p_{ij}$} is the probability of making a transition from $i$ to $j$ in one step.
Consequently, if $X_2$ = $j$ and $X_0$ = $i$ 
What is the probability of going from $i$ to $j$ in 2 steps?
\begin{align*}
P (X_2= j \mid X_0 = i) &= P_i(X_2 = j) \\
&= \sum_{k=1}^{N} P_i (X_2 = j \mid X_1 = k) \cdot P_i(X_1 = k) 
&& \text{(Partition theorem)} \\
&= \sum_{k=1}^{N} P_i (X_2 = j \mid X_1 = k) \cdot P_i(X_1 = k \mid X_0 = i) 
&& \text{(Markov property)} \\
&= \sum_{k=1}^{N} p_{kj} \cdot p_{ik} 
&& \text{(By definition)} \\
&= \sum_{k=1}^{N} p_{ik} \cdot p_{kj} 
&&\text{rearranging} \\
&= (P^2)_{ij} 
&& \text{(Matrix multiplication)} \\
\end{align*}
\[
\boxed{P(X_2 = j \mid X_0 = i) = P(X_{n+2} = j \mid X_n = i) = (P^2)_{ij} \quad \text{for any } n}
\]\\
Similarly, P($X_3$= $j$ \mid $X_0$= $i$) can be written as follows: 

\begin{align*}
P(X_3 = j \mid X_0 = i) 
&= \sum_{k=1}^{N} P(X_3 = j \mid X_2 = k) \cdot P(X_2 = k \mid X_0 = i) \\
&= \sum_{k=1}^{N} p_{kj} \cdot (P^2)_{ik} \\
&= (P^3)_{ij}
\end{align*}

\[
\boxed{
P(X_3 = j \mid X_0 = i) = P(X_{n+3} = j \mid X_n = i) = (P^3)_{ij} \quad \text{for any } n
}
\]
\\ \text{Then generally, the t-step transition probability can be written as:}

\[
\boxed{
P(X_t = j \mid X_0 = i) = P(X_{n+t} = j \mid X_n = i) = (P^t)_{ij} \quad \text{for any } n
}
\]

\[
\text{Where } P^t \text{ is the transition probability matrix raised to the power } t.
\]
\subsection{Distribution of $X_t$}
Let \[ 
X_0, X_1, X_2,...X_N
\] 
be a Markov chain with State space S= {1, 2,...,N}
\newline Now each $X_t$ is a random variable with a probability distribution.
 We can write the probability distribution of $X_t$ as an N × 1 vector. Let V be an N × 1 vector: 
\[
\mathbf{v} =
\begin{bmatrix}
v_1 \\
v_2 \\
\vdots \\
v_N
\end{bmatrix}
=
\begin{bmatrix}
P(X_0 = 1) \\
P(X_0 = 2) \\
\vdots \\
P(X_0 = N)
\end{bmatrix}
\]
The probability distribution at $X_1$:
\[
\begin{aligned}
& P(X_1 = j) = \sum_{i=1}^{N} P(X_1 = j | X_0 = i) P(X_0 = i) \\
& =\sum_{i=1}^{N} p_{ij} v_i\\
& = \sum_{i=1}^{N} v_i p_{ij} \quad \text{(by definition)}\\
& = v^T P_j
\end{aligned}
\]
The probability distribution at $X_2$:
\subsection{Probability distribution of $X_2$}

Using the Partition Rule as before, conditioning on $X_0$:

\[
\begin{aligned}
P(X_2 = j) 
&= \sum_{i=1}^{N} P(X_2 = j \mid X_0 = i) P(X_0 = i) \\
&= \sum_{i=1}^{N} (P^2)_{ij} \, v_i \\
&= v^T (P^2)_j
\end{aligned}
\]

The row vector $v^T P^2$ is therefore the probability distribution of $X_2$.

\[ 
\boxed{
\begin{aligned}
X_0 &\sim v^T \\
X_1 &\sim v^T P \\
X_2 &\sim v^T P^2 \\
&\vdots \\
X_t &\sim v^T P^t
\end{aligned}
}
\]

\subsection{The transition matrix}

Let $\{X_0, X_1, X_2, \ldots \}$ be a Markov chain with $N \times N$ transition matrix $P$.  
If the probability distribution of $X_0$ is given by the $1 \times N$ row vector $v^T$,  
then the probability distribution of $X_t$ is given by the $1 \times N$ row vector $v^T P^t$. That is,

\[
X_0 \sim v^T \quad \Rightarrow \quad X_t \sim v^T P^t.
\]

Taking one step in the Markov chain corresponds to multiplying by $P$ on the right.
So, the probability distribution at time t is represented with a row vector $v_t$ and the transition matrix \textit{P} tells you the probability of moving from state $i$ to $j$ $v_{t+1}$ = $v_t$ P\\


For example, let the transition matrix be:
\[
P = \begin{bmatrix}
0.7 & 0.3 \\
0.4 & 0.6
\end{bmatrix}
\]
\[
v_0 = \begin{bmatrix} 1 & 0 \end{bmatrix}
\]
\[
v_1 = v_0 \times P = \begin{bmatrix} 1 & 0 \end{bmatrix} \times \begin{bmatrix}
0.7 & 0.3 \\
0.4 & 0.6
\end{bmatrix} = \begin{bmatrix} 0.7 & 0.3 \end{bmatrix}
\]
Also \textbf{ \( P \) is raised to a power} to get the transition matrix for \( t \) steps in one shot:
\[
\mathbf{v}_t = \mathbf{v}_0 P^t
\]
So the distribution after 5 steps:
\[
\mathbf{v}_5 = \mathbf{v}_0 P^5
\]
Overall, this describes how the Markov chain can be used as the vector population represents the number of individuals in each group and the transition matrix specifies the probabilities of people transitioning from one age group to another in a given year. 
\subsection{Matrix vector multiplication}
Let \( A \) be an \( m \times n \) matrix, \( B \) an \( n \times p \) matrix, and let \( \mathbf{x} \in \mathbb{R}^p \). Denote the columns of \( B \) by \( \mathbf{b}_1, \mathbf{b}_2, \ldots, \mathbf{b}_p \), and the entries of \( \mathbf{x} \) by \( x_1, x_2, \ldots, x_p \).

\[
B\mathbf{x} = x_1 \mathbf{b}_1 + x_2 \mathbf{b}_2 + \cdots + x_p \mathbf{b}_p
\]

By the linearity of matrix multiplication:

\[
A(B\mathbf{x}) = A(x_1 \mathbf{b}_1 + x_2 \mathbf{b}_2 + \cdots + x_p \mathbf{b}_p)
\]

\[
A(B\mathbf{x}) = x_1 A\mathbf{b}_1 + x_2 A\mathbf{b}_2 + \cdots + x_p A\mathbf{b}_p = (A\mathbf{b}_1 + A\mathbf{b}_2 + \cdots + A\mathbf{b}_p)\mathbf{x}
\]

Thus, multiplication by \( (A\mathbf{b}_1 + \cdots + A\mathbf{b}_p) \) transforms \( \mathbf{x} \) into \( A(B\mathbf{x}) \).

If \( A \) is an \( m \times n \) matrix and \( B \) is an \( n \times p \) matrix with columns \( \mathbf{b}_1, \mathbf{b}_2, \ldots, \mathbf{b}_p \), then the product \( AB \) is the \( m \times p \) matrix whose columns are \( A\mathbf{b}_1, A\mathbf{b}_2, \ldots, A\mathbf{b}_p \):

\[
AB = A[\mathbf{b}_1 \ \mathbf{b}_2 \ \cdots \ \mathbf{b}_p] = [A\mathbf{b}_1 \ A\mathbf{b}_2 \ \cdots \ A\mathbf{b}_p]
\]

Each column of \( AB \) is a linear combination of the columns of \( A \) using weights from the corresponding columns of \( B \).
\newpage
\section{Application}
\subsection{User guide}
\textbf{Key Features}:
\vspace{0.3cm}
\newline
\vspace{0.3cm}
1. Input Population Sizes: Enter an initial number of individuals in each age group.\\[0.2cm]
2. Input Transition Matrix: Enter percentages (0–100) for transitions (e.g., birth rate, ageing, survival).\\[0.2cm]
3. Simulation: Run the model for a given number of years, with step-by-step or end results.
\vspace{0.5cm}
\newline
\underline{\textbf{Purpose}}
\vspace{0.5cm}
\newline
1- The program helps you understand how demographic factors (births, ageing, mortality) affect population dynamics.
\vspace{0.5cm}
\newline
2- The program is user-friendly as it uses percentages instead of decimals, provides detailed instructions, and validates input to prevent errors.
\vspace{0.5cm}
\newline
3- Model real populations with data from sources like census tables or UN data.

\vspace{0.6cm}
\textcolor{red}{\textit{Note}}: \textit{Do not enter percentages their total is greater than 100 \% in a group}.
\subsection{Code}
\begin{lstlisting}
import numpy as np

# Collect initial population vector from user
def get_population_vector():
    print("Enter initial population sizes for each age group:")
    try:
        children = float(input("Children (0-14 years): "))
        adults = float(input("Adults (15-64 years): "))
        elderly = float(input("Elderly (65+ years): "))
        pop_vector = np.array([children, adults, elderly])
        if np.any(pop_vector < 0):
            raise ValueError("Population sizes must be non-negative.")
        return pop_vector
    except ValueError as e:
        print(f"Error: {e}")
        return None

# Collect transition matrix as percentages with detailed guidance
def get_transition_matrix():
    print(" Enter percentages (0 to 100) for how people move between age groups each year.")
    print("Each group (Children, Adults, Elderly) needs 3 percentages:")
    print("- Children: EX: birth rate from Adults (typically 5-10%)")
    print("- Adults: EX: Children aging to Adults (typically 90-95%)")
    print("- Elderly: EX: Adults aging to Elderly (typically 5-10%)")
    print("Each group's percentages must sum to <= 100% (remainder is mortality, such as 10% die).")
    print("\nExample Matrix (realistic values):")
    print("From:       | To Children | To Adults | To Elderly")
    print("------------|-------------|-----------|-----------")
    print("Children    | 0% (no stay)| 95% (aging)| 0% (none) ")
    print("Adults      | 10% (births)| 85% (stay)| 0% (none) ")
    print("Elderly     | 0% (none)  | 5% (aging)| 90% (stay)")
    print("\nColumn sums: 10% (90% die), 100% (no deaths), 90% (10% die)")
    print("Tip: Avoid high values like 70% for births, as they may exceed 100%.")

    try:
        matrix = np.zeros((3, 3))
        groups = ["Children", "Adults", "Elderly"]
        prompts = [
            ["staying Children (usually 0-5%)", "aging to Adults (EX: 90-95%)", "becoming Elderly (usually 0%)"],
            ["give birth to Children (birth rate, EX: 5-10%)", "staying Adults (EX: 85-95%)", "aging to Elderly (EX: 5-10%)"],
            ["give birth to Children (usually 0%)", "becoming Adults (usually 0%)", "staying Elderly (EX: 80-90%)"]
        ]
        for j in range(3):
            while True:
                print(f"\nEnter percentages for {groups[j]} at time t:")
                col = []
                for i in range(3):
                    prompt = f"Percentage {prompts[j][i]} (0-100): "
                    percentage = float(input(prompt))
                    if percentage < 0 or percentage > 100:
                        raise ValueError(f"Percentage {prompts[j][i]} must be between 0 and 100.")
                    col.append(percentage)
                col_sum = sum(col)
                if col_sum > 100.001:
                    print(f"Error: Sum of percentages ({col_sum}%) exceeds 100%.")
                    print(f"You entered: {col[0]}% to Children, {col[1]}% to Adults, {col[2]}% to Elderly.")
                    print("Try reducing values (e.g., birth rate to 5-10%, survival to 85-95%).")
                    continue

                for i in range(3):
                    matrix[i, j] = col[i] / 100
                print(f"Sum for {groups[j]}: {col_sum}% (valid)")
                break
        return matrix
    except ValueError as e:
        print(f"Error: {e}")
        return None

# Simulate population changes over time
def simulate_population(initial_pop, trans_matrix, steps, step_by_step=True):
    if step_by_step:
        current_pop = initial_pop.copy()
        print("\nStep-by-step simulation:")
        print(f"Step 0: {current_pop}")
        for t in range(1, steps + 1):
            current_pop = np.dot(trans_matrix, current_pop)
            print(f"Step {t}: {current_pop}")
        return current_pop
    else:
        trans_matrix_power = np.linalg.matrix_power(trans_matrix, steps)
        final_pop = np.dot(trans_matrix_power, initial_pop)
        print(f"\nPopulation after {steps} steps: {final_pop}")
        return final_pop

def main():
    """Main function to run the population model."""
    print("Population Modeling using Markov Chains")
    print("======================================")
    print("This program simulates population changes across three age groups:")
    print("1. Children (0-14 years)")
    print("2. Adults (15-64 years)")
    print("3. Elderly (65+ years)")
    print("======================================\n")

    pop_vector = get_population_vector()
    if pop_vector is None:
        print("Invalid population vector. Exiting.")
        return

    trans_matrix = get_transition_matrix()
    if trans_matrix is None:
        print("Invalid transition matrix. Exiting.")
        return

    print("\nInitial Population Vector:")
    print(pop_vector)
    print("\nTransition Matrix:")
    print(trans_matrix)

    try:
        steps = int(input("\nEnter number of time steps to simulate: "))
        if steps < 0:
            raise ValueError("Number of steps must be non-negative.")
        sim_type = input("Run step-by-step simulation? (yes/no): ").lower()
        step_by_step = sim_type.startswith('y')
    except ValueError as e:
        print(f"Error: {e}")
        return

    final_pop = simulate_population(pop_vector, trans_matrix, steps, step_by_step)
    print("\nSimulation complete.")

if __name__ == "__main__":
    main()
\end{lstlisting}




\newpage
\section{References }
[1] R. Fewster, Chapter 8: Markov chains, University of Auckland. [Online]. Available: https://www.stat.auckland.ac.nz/~fewster/325/notes/ch8.pdf. [Accessed: May 1, 2025].

\end{document}

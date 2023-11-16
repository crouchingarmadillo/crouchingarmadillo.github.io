---
layout: post
title: Probability from Measurements
mathjax: true
excerpt: Probability wasn't always the clear cut Kolmogorov axioms we have today. This post will attempt to motivate why Kolmogorov axioms are the right foundation for probability from the more rudimentary idea of limits of falsifiable measurements.
---
Probability wasn't always the clear cut Kolmogorov axioms we have today. This post will attempt to motivate why Kolmogorov axioms are the right foundation for probability from the more rudimentary idea of limits of falsifiable measurements.

# Boolean Algebra
Before getting to $\sigma$-algebras (measurable spaces) and Kolmogorov's axioms, we first need to talk about the finite version, Boolean algebra. We will later see measurable spaces are in some sense completions of Boolean algebras after a limiting process.

The setting is this. We have a collection $\Omega$ of possible things (we will call them samples and $\Omega$ our sample space) that we can do falsifiable measurements on. Our Boolean algebra will be the falsifiable measurements we can do in some finite number of steps.

**(Informal) Definition:** A *falsifiable measurement* is a property of a sample that is either true or false and which we can decide in a finite number of steps which of the two it is.

More formally, a falsifiable measurement will be a predicate $P : \Omega \to \\{0, 1\\}$ with some additional properties which we will attempt to uncover.

**Remark:** The key trait here (other than finiteness) is that the measurement is **falsifiable**. This means we can always measure a definitive yes or no answer (if the sample has such a property or not). This is in stark contrast to properties which are **verifiable**, i.e. if it has a property we can show it has it, but we can't necessarily show it doesn't have it. This is a key distinction in science and a computer scientist would consider this the difference between decidability (determinism!) and recognizability (nondeterminism!).

As an example of the distinction, consider the question of deciding if two real numbers $x, y \in [0, 1]$ are equal. They will be given as their infinite binary expansions $x, y : \mathbb{N} \to \\{0, 1\\}$. This question is equivalent to deciding if $x - y = 0$, i.e. if there is a natural number $n \in \mathbb{N}$ such that the $n$th binary digit $(x - y)_n$ is nonzero (i.e. one). If $x - y$ are non-zero, we can find such a binary digit eventually, it exists and we can even brute force search for it. So we can verify that $x - y$ is nonzero. What about checking that $x - y = 0$? Well this requires checking infinite binary digits are 0, which we can't do in any finite number of steps. So this problem is not falsifiable. It is coverifiable so to speak, where co means we verify the no answer (not equal) rather than the yes answer. By contrast, we can always decide if two rational numbers are equal.

With the distinction made plain, we will get tired of saying finite and falsifiable, so we will now omit them and just say "measurement" and mention finiteness where necessary.

## Boolean Axioms
We now wish to uncover the axioms measurements must satisfy. As it turns out, falsifiability translates to answering yes or no being on equal footing and this already translates into an axiom. Let's now consider what axioms finiteness entails.

### Finiteness
Generally we will think of having access to some basic measurements $M_1, ..., M_k : \Omega \to \\{0, 1\\}$ (think of having a ruler and the basic measurements are the tick marks) and these can be combined to create new measurements. Thus we shall work inductively and consider the operations measurements are closed under.

Finiteness means that we consider doing a finite number of measurements $P_1, ..., P_n : \Omega \to \\{0, 1\\}$ and somehow combining them into a new measurement $P : \Omega \to \\{0, 1\\}$. 

Every possible way to combine a finite number of measurements is captured by functions $f_n : \\{0, 1\\}^n \to \\{0, 1\\}$. The reason why is because we can just compose them

$$P_1 \cdots P_n ; f_n : \Omega \to \\{0, 1\\} = \omega \mapsto f_n(P_1(\omega) \cdots P_n(\omega))$$

Thus we just need to classify every possible $f_n$ for every $n$.

**Remark on notation:** Here $P_1 \cdots P_n$ means concactenation (as binary strings!), not a product (although it is a categorical product) or composition of functions. It is conventional in computer science as well as how we as human beings write words and numbers and such (decimals are just written as digits concactenated together). Also ; is function composition here, but in diagrammatic order rather than the standard leibniz ordering by $\circ$ that people are accustomed to, $f;g = g \circ f$. It's nice in algebra because it can be read left to right as "$f$ first then $g$".

We can expand $f_n$ in terms of basis functions kronecker deltas

$$ \delta_{x, \cdot} = y \mapsto \begin{cases}
    1 & x = y \\
    0 & x \neq y
\end{cases} $$

We have 

$$ \begin{align}
    f_n &= \sum_{x \in \{0, 1\}^n} f_n(x) \wedge \delta_{x, \cdot} \\
    &= \bigvee_{x \in \{0, 1\}^n} f_n(x) \wedge \delta_{x, \cdot}
\end{align} $$

where addition is modulo two (XOR), $\wedge$ is AND, $\vee$ is OR. We can replace XOR with OR because the kronecker deltas ensure at most one summand is true (exactly one since we are summing over every string). All the functional dependence has been offloaded to the kronecker deltas, so if we can understand the kronecker deltas we understand every function. Observe that $x = y$ iff $x_1 = y_1 \wedge \cdots \wedge x_n = y_n$ so $\delta_{x, y} = \delta_{x_1, y_1} \wedge \cdots \wedge \delta_{x_n, y_n}$. Thus now we only need to understand a one dimensional kronecker delta $\delta_{x_i, y_i}$. One might hope this can be expressed in a finite number of arithmetic operations and indeed we can.

$$ \delta_{x_i, y_i} = (x_i \wedge y_i) \vee (\overline{x}_i \wedge \overline{y}_i) $$

where $\overline{x}_i$ is NOT $x_i$.

Thus every function can be expressed as a finite number of OR, AND, and NOT operations. This proves that they are universal gates for boolean operations. We also have by De Morgan's laws that when NOT is available, the ability to compute AND is equivalent to being able to compute OR. So we will restrict attention to NOT and OR. If measurements are closed under NOT, OR (i.e. they can be done in a finite number of steps) then this will entail every possible measurement we can get out of a finite number of measurements. But are they? We will argue yes they are.

Suppose we have a measurement $P : \Omega \to \\{0, 1\\}$. Falsifiability requires that for any sample $\omega \in \Omega$, we get a definitive yes or no to measuring $P(\omega)$. Because it's defined for both, we also measure $\overline{P(\omega)}$ by just flipping the yes and the no. This is done in one step. So falsifiability requires that $\overline{P} = \omega \mapsto \overline{P(\omega)}$ is a measurement too.

Now suppose we have two measurements $P, Q : \Omega \to \\{0, 1\\}$. Given $\omega \to \\{0, 1\\}$ we have the measurements $P(\omega), Q(\omega)$. When we have these it takes only one step to read if at least one is true. In such a case we have measured $P(\omega) \vee Q(\omega)$. Thus $P \vee Q$ is a measurement.

Finally we must consider the question of not measuring. The two closure operations presuppose we have done some measurements to combine or modify. The answer comes by considering functions on zero bits, $\\{\varepsilon\\} \to \\{0, 1\\}$ where $\varepsilon$ is the empty string. There are exactly two functions here, the tautology $T = 1$ and the contradiction $F = 0$. These lift to functions $\Omega \to \\{0, 1\\}$ by being 1 or 0 respectively on every $\omega \in \Omega$. This lift is the only reasonable thing to do because $n$ measurements (before combining to a single measurement) correspond to a map $\Omega \to \\{0, 1\\}^n$. So no measurement means sending everything to $\varepsilon$ and then sending this to 0 or 1.

Putting these together we finally have the Boolean algebra axioms.

**(B1)** The tautology $T$ and contradiction $F$ are measurements on $\Omega$.

**(B2)** If $P : \Omega \to \\{0, 1\\}$ is a measurement on $\Omega$, then $\overline{P}$ is a measurement on $\Omega$.

**(B3)** If $P, Q : \Omega \to \\{0, 1\\}$ are measurements on $\Omega$, then $P \vee Q$ is a measurement on $\Omega$.

**Definition:** If **B** is a collection of predicates $\Omega \to \\{0, 1\\}$ satisfying **(B1), (B2), (B3)** then we say **B** is a *boolean algebra* on $\Omega$ and call $(\Omega, \textbf{B})$ a *finite measurable space*.

**Remark:** The term *finite measurable space* is not standard, but considering the conventional definition of a measurable space (which will come later in this post), it seems an appropriate name.

Earlier we thought about basic measurements $M_1, \dots, M_k : \Omega \to \\{0, 1\\}$ that can be combined to make new measurements. Using boolean algebra, we can now formalize exactly what that means. Measurements can be combined using NOT and OR, the smallest collection of measurements closed under such operations is every measurement we can make from these basic measurements in a finite number of operations. So we say $M_1, \dots, M_k$ generate a boolean algebra, the smallest boolean algebra which contains them. One can prove that this boolean algebra is the intersection of every boolean algebra that contains $M_1, \dots, M_k$. These basic measurements are generators of this boolean algebra, but generators are not unique (think about how different combinations of rulers can potentially all be used appropriately to measure the same lengths) and what's fundamental is really what we can possibly measure, not the tools we use to do so, which is why the definition of boolean algebra does not mention them.

# Finite Probability Theory (attempt)
Now that we have an idea of what measurements (they're called events in probability) look like formally, we can attempt to investigate probability using it.

Say we have a finite measurable space $(\Omega, \textbf{B})$ and an event $A \in \textbf{B}$. When we have a sample $\omega \in \Omega$ and $A(\omega)$ is true, we say $A$ occured.

The idea behind probability theory is to "randomly" pick a sample $\omega \in \Omega$ and ask with what frequency $A$ occurs. A frequentist might say no problem, setup $n$ identical sample spaces $\Omega$ and "randomly" pick $n$ samples $\omega_1, \dots, \omega_n$ from the identical sample spaces. The probability of $A$ is the frequency

$$ \frac{A(\omega_1) + \dots + A(\omega_n)}{n} $$

that $A$ occurs, where addition is in the real numbers. This corresponds to a sample space $\Omega^n$ with event $A^n = \omega_1 \cdots \omega_n \mapsto A(\omega_1) \cdots A(\omega_n)$. No issues with finiteness here (just measure $A$ $n$ times). However, the problem is that this frequency is not unique. It relies on the particular samples, and on the $n$ in general.

To this, a frequentist (or scientist) might say, no no no, the probability is the **limiting** frequency as $n$ goes to infinity.

This would correspond to picking a sequence of samples $\omega_1, \omega_2, \dots$ in a sequence of identical sample spaces $\Omega$ and then we say the probability of $A$ is

$$ \Pr[A] := \lim_{n \to \infty} \frac{\sum_{i = 1}^n A(\omega_i)}{n} .$$

When done with care, this does pick out a unique frequency (law of large numbers is a standard result in probability). However, we can see right away we are forced to leave finiteness. $\Omega^{\mathbb{N}^+}$ is not finite even if $\Omega$ originally was and we are considering the (not finite) event $A^{\mathbb{N}^+}$ which we cannot possibly measure in a finite number of measurements.

Care aside, the definition of probability as given is not fully defined, we have to define what we mean by "randomly" picking samples and prove convergence (to the same value for every sequence of samples). For now we will work with this as a formal limit and deduce what we can for how a limiting frequency ought to behave. Let's start with the trivial events.

$$ \Pr[T] = \lim_{n \to \infty} \frac{\sum_{i = 1}^n 1}{n} = 1 $$

$$ \Pr[F] = \lim_{n \to \infty} \frac{\sum_{i = 1}^n 0}{n} = 0 $$

This is in line with expectations, the tautology always occurs, and the contradiction never occurs. As a corollary to this method of proof, $0 = F(\omega_i) \leq A(\omega_i) \leq T(\omega_i) = 1$ for every event $A$, sample $\omega_i \in \Omega$ so we have the image of probability lies in $[0, 1]$ as expected of a frequency.

Now consider how probability interacts with NOT.

$$ \begin{align}
\Pr[\overline{A}] &= \lim_{n \to \infty} \frac{\sum_{i = 1}^n \overline{A(\omega_i)}}{n} \\
&= \lim_{n \to \infty} \frac{\sum_{i = 1}^n 1 - A(\omega_i)}{n} \\
&= 1 - \Pr[A]
\end{align} $$

This makes sense, because $\overline{A}$ occurs with the frequency that $A$ doesn't.

Finally we consider OR. 

$$ \begin{align}
    \Pr[A \vee B] &= \lim_{n \to \infty} \frac{\sum_{i=1}^n A(\omega_i) \vee B(\omega_i)}{n} \\
    &\leq \lim_{n \to \infty} \frac{\sum_{i=1}^n A(\omega_i) + B(\omega_i)}{n} \\
    &\leq \Pr[A] + \Pr[B]
\end{align} $$

Subadditivity is the best that can be done for a general OR, because in the case both $A$ and $B$ occur, $A + B > A \vee B$. But if this never happens, then we have equality. This motivates a definition.

**Definition:** Events $A, B : \Omega \to \\{0, 1\\}$ are mutually exclusive if $A \wedge B = F$.

For mutually exclusive events $A, B$ we have $\Pr[A \vee B] = \Pr[A] + \Pr[B]$. This fact actually implies subadditivty for OR of general events.

Additivity of mutually exclusive events, together with the values of probability on the tautology and contradiction is sufficient to prove the NOT rule as well.

These rules/axioms thus far are all consistent with the frequentist interpretation of probability and in fact with care are equivalent. We haven't really done a limiting process (other than picking out the frequency uniquely). We need to move away from boolean algebras and onto using the limiting process.

# Probability
## $\sigma$ Algebra
Let's write down the Boolean algebra axioms again but this time making the finiteness explicit.

**B** is a boolean algebra on $\Omega$ if:

**(B1)** $F, T \in \textbf{B}$

**(B2)** $A \in \textbf{B} \implies \overline{A} \in \textbf{B}$

**(B3)** $A_1, \dots, A_n \in \textbf{B} \implies \bigvee_{i = 1}^n A_i \in \textbf{B}$

There's nothing further to be done for the first two axioms, but the final axiom is equivalent to being closed under finite OR's (writing it for two is really just tidying up with the rest implied by induction).

If we wish to add a limiting process in here, we really need to look at $\bigvee_{i = 1}^n A_i$ as $n$ goes to infinity.

Let $A_1, A_2, ...$ be a sequence of predicates on $\Omega$. We can form a sequence (a chain really) of OR's. The empty OR is the identity $F$.

$$ \bigvee_{i = 1}^0 A_i \implies \bigvee_{i = 1}^1 A_i \implies \cdots  $$

For each $n$ we say $\bigvee_{i = 1}^n A_i$ is true if at least one of the $A_1, ..., A_n$ is true. In the limit, we're looking at if at least one of the $A_1, A_2, ...$ is true. Thus we have a definition for a countable OR.

$$ \bigvee_{i=1}^\infty A_i(\omega) = \exists i \in \mathbb{N}^+ A_i(\omega) $$

We can add limits to our boolean algebra by extending closure under finite OR to closure under countable OR. Coincidentally this is also a categorical colimit.

**Definition:** Let $\Omega$ be a set and **S** a collection of predicates $\Omega \to \\{0, 1\\}$ on $\Omega$. **S** is a $\sigma$ algebra on $\Omega$ if:

**($\boldsymbol{\sigma}$1)** $F, T \in \textbf{S}$

**($\boldsymbol{\sigma}$2)** $A \in \textbf{S} \implies \overline{A} \in \textbf{S}$

**($\boldsymbol{\sigma}$3)** $A_1, A_2, ... \in \textbf{S} \implies \bigvee_{i=1}^\infty A_i \in \textbf{S}$

We call $(\Omega, \textbf{S})$ a measurable space. Elements of $\textbf{S}$, which are really limits of finite falsifiable measurements, are called events. A $\sigma$ algebra as a category is a boolean algebra as a category which is countably complete (have all countable limits). So $\sigma$ algebras are completions of boolean algebras in a an appropriate sense.

Let's now investigate probability using this instead. Particularly, how additivity changes. First we need to redefine mutual exclusivity for sequences of events. 

Let $A_1, A_2, ... \in \textbf{S}$ be a sequence of events. We say the $(A_n)_n$ are mutually exclusive if $A_i \wedge A_j = F$ for all $A_i \neq A_j$.

## Kolmogorov Axioms
Let's now look at countable additivity. Let $A_1, A_2, ... \in \textbf{S}$ be a sequence of mutually exclusive events.

$$ \begin{align}
    \Pr[\bigvee_{i=1}^\infty A_i] &= \lim_{n \to \infty} \frac{\sum_{j=1}^n \bigvee_{i=1}^\infty A_i(\omega_j)}{n} \\
    &= \lim_{n \to \infty} \frac{\sum_{j=1}^n \sum_{i=1}^\infty A_i(\omega_j)}{n} \\
    &= \lim_{n \to \infty} \frac{\sum_{i=1}^\infty \sum_{j=1}^n A_i(\omega_j)}{n} \\
    &= \sum_{i=1}^\infty \Pr[A_i]
\end{align} $$

Thus countable additivity is exactly what we should expect. These observations together yield the Kolmogorov axioms (and it is exhaustive because it spells out exactly how $\Pr$ interacts with each operation our events are closed under).

Let **S** be a $\sigma$ algebra over $\Omega$. We say $\Pr : \textbf{S} \to [0, 1]$ is a probability measure on $(\Omega, \textbf{S})$ if:

**(P1)** $\Pr[F] = 0$ and $\Pr[T] = 1$

**(P2)** $A_1, A_2, ... \in \textbf{S}$ mutually exclusive $\implies \Pr[\bigvee_{i=1}^\infty A_i] = \sum_{i=1}^\infty \Pr[A_i]$

We call $(\Omega, \textbf{S}, \Pr)$ a probability space. Ok we cheated a little, one axiom here we put implicitly is we assumed the probability measure is non-negative (and this was included in the codomain definition). Conventional treatments will put that as an extra axiom. This is interesting for theories of probability which have negative probabilities, but that's not what we're concerned with here.

## Measurable Functions (random variables)
One loose end we didn't fully tie up in this theory are the special kinds of functions between measurable spaces (or probability spaces). These are generally called measurable functions or random variables.

The key idea is this. We have two measurable spaces $(\Omega, \textbf{S}), (\Omega', \textbf{S}')$. We know how to take measurements in $\Omega$, but we don't know how to take measurements in $\Omega'$. Can we somehow use measurements in $\Omega$ to take measurements in $\Omega'$? This is exactly what a measurable function is.

**Definition:** Let $(\Omega, \textbf{S}), (\Omega', \textbf{S}')$ be measurable spaces. We say $f : \Omega \to \Omega'$ is a measurable function if for every event $A' \in \textbf{S}'$ in $\Omega'$, there exists an event $A \in \textbf{S}$ in $\Omega$ such that $A = f;A'$.

For the restriction of $\Omega'$ to im$f$, $f$ is surjective as we can use a left inverse $g : \text{im}f \to \Omega$ to measure $A'\big{\|}_{\text{im}f} = g;A$.

**Definition:** The $\sigma$ algebra generated by $f$ is
$$ \sigma(f) := \{ A\big{|}_{\text{im}f} : A \in \textbf{S}' \} $$

We have that $(\text{im}f, \sigma(f))$ is a measurable subspace of $\Omega'$. This is the subspace that we can translate measurements of $\Omega$ into measurements of $\Omega'$.

If additionally $\Omega$ has a probability measure $\Pr$, more is true. In such a case, a measurable function $X : \Omega \to \Omega'$ is called a **random variable** and it induces a probability measure $\Pr _X$ on $\Omega'$.

**Definition:** Let $X : \Omega \to \Omega'$ be a random variable. The probability measure on $\Omega'$ induced by $X$ is given by

$$ \text{Pr} _X := A \mapsto \Pr[X = A] $$

where $X = A$ is the event in $\Omega$ given by the definition of a measurable function.

## Notation
The last caveat to mention is that conventional treatments use slightly different notation. We have worked with predicates $\Omega \to \\{0, 1\\}$ because it is nice to think about and its connection to boolean algebra and properties is very clear. However, it is conventional to work instead with subsets of $\Omega$.
A predicate $P : \Omega \to \\{0, 1\\}$ can be identified with a subset $\Omega _P = \\{ \omega \in \Omega : P(\omega) \\}$ and this is both a bijection and an isomorphism in all the ways that matter. In this case, we have the following identifications.

- $F \leftrightarrow \emptyset$
- $T \leftrightarrow \Omega$
- $\overline{A} \leftrightarrow \overline{\Omega _A} = \Omega - \Omega _A$
- $\bigvee \leftrightarrow \bigcup$
- $\bigwedge \leftrightarrow \bigcap$
- Predicate events $\leftrightarrow$ set events which are often called measurable sets
- A measurable function $f$ is such that $A$ being measurable implies $f^{-1}(A)$ is measurable.
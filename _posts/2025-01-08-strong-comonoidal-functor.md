---
layout: post
title: Can we have a strong comonoidal functor?
maths: Strong Comonoidal Functor
date: 2025-01-08
tags:
  - Maths
---

> This is a quick post to answer a question from this morning. There are many WIP posts that probably could have been uploaded at some point, but this one happens to be the first in over a year... c'est la vie!
> 
> The question:
> 
> > Is there a definition of a functor that is "strong" (which would usually mean that $A \otimes F(B) \to F(A \otimes B)$) in a way that is dependent on a given comonad, i.e. $W(A) \otimes F(B) \to F(A \otimes B)$ where one could then have a dual definition $F(A \otimes B) \to W(A) \otimes F(B)$?

In short, yes.

Oh, that wasn't too bad.

In long?

Well, in category theory, the concept of a functor has many extensions, including the notion of "strong" functors that interact with certain structures like monads (and, here, comonads). This question isn't about the comonad functor or comonoidal functor, the dual of a monoidal functor, but rather a monoidal functor over comonads.

To define a functor that is "strong" (monoidal) with respect to a comonad, we need to establish a few components.

- Let $\mathcal{C}$ and $\mathcal{D}$ be categories
- Let $F: \mathcal{C} \to \mathcal{D}$ be a functor

Normally, as stated in the question, for a functor $F$ to be strong with respect to a monoidal structure, then it must have a natural transformation $\phi: A \otimes F(B) \to F(A \otimes B)$ for all objects $A$ and $B$ in $\mathcal{C}$, thus preserving the monoidal structure.

With the comonad $W$, the situation changes slightly, as a comonad consists of a functor $W: \mathcal{C} \to \mathcal{C}$ along with two natural transformations: a counit $\epsilon: W(A) \to A$ and a comultiplication $\delta: W(A) \to W(W(A))$.

- Let $W: \mathcal{C} \to \mathcal{C}$ be a comonad on $\mathcal{C}$ with counit $\epsilon: W(A) \to A$ and comultiplication $\delta: W(A) \to W(W(A))$

For a functor $F$ to be "strong" with respect to the comonad $W$, we need a natural transformation that reflects the interaction between the comonad and the functor. As posed in the question, we define such a functor as one that has a natural transformation:

- Let $\phi: W(A) \otimes F(B) \to F(A \otimes B)$ be a natural transformation with the comonad $W$, for a functor $F$, for all objects $A$ and $B$ in $\mathcal{C}$

This transformation allows us to "lift" the structure of $W$ into the functor $F$.

- Let $\psi: F(A \otimes B) \to W(A) \otimes F(B)$ be the dual transformation of $\phi$

This dual transformation represents a sort of "coherence" condition that relates the functor back to the comonadic structure, like how strong monads and their dual notions interact in the context of monoidal categories.

So, functors can definitely be defined to interact with additional structures like comonads in a coherent, "strong" way. The specific properties and definitions will depend on the context and categories involved, but we can at least provide a quick sketch of what they should satisfy, in order to be strong with respect to a comonad.

As above, a functor $F: \mathcal{C} \to \mathcal{D}$ should be "strong" with respect to the comonad $W$ if there exists a natural transformation:

$$
\phi: W(A) \otimes F(B) \to F(A \otimes B)
$$

for all objects $A, B$ in $\mathcal{C}$, where $\otimes$ denotes the monoidal structure in both categories $\mathcal{C}$ and $\mathcal{D}$, just to restate the above.

For a strong monoidal functor, the transformation $\phi$ must be natural in both arguments; the "naturality" condition. This means, for any morphisms $f: A' \to A$ and $g: B \to B'$ in $\mathcal{C}$, the following diagram commutes:

$$
\begin{array}{ccc}

W(A') \otimes F(B) & \xrightarrow{\phi} & F(A' \otimes B) \\

\downarrow{W(f) \otimes F(g)} & & \downarrow{F(f \otimes g)} \\

W(A) \otimes F(B') & \xrightarrow{\phi} & F(A \otimes B')

\end{array}
$$

The transformation $\phi$ should also respect the comonadic structure, a "compatiblity" condition, by satisfying the following coherence conditions for the counit $\epsilon$ and comultiplication $\delta$.

For compatiblity, the following diagrams should commute for all objects $A, B$:

1. Compatiblity with the comandic structure through the counit $\epsilon$:

$$
\begin{array}{ccc}

W(A) \otimes F(B) & \xrightarrow{\phi} & F(A \otimes B) \\

\downarrow{\epsilon} & & \downarrow{F(\epsilon)} \\

A \otimes F(B) & \xrightarrow{\text{id} \otimes F(\epsilon)} & F(A)

\end{array}
$$

2. Compatiblity with the comandic structure through the comultiplication $\delta$:

$$
\begin{array}{ccc}

W(A) \otimes F(B) & \xrightarrow{\phi} & F(A \otimes B) \\

\downarrow{\delta} & & \downarrow{F(\delta)} \\

W(W(A)) \otimes F(B) & \xrightarrow{\phi} & F(W(A) \otimes B)

\end{array}
$$

So, a functor $F: \mathcal{C} \to \mathcal{D}$ is strong with respect to a comonad $W$ if there exists a natural transformation $\phi: W(A) \otimes F(B) \to F(A \otimes B)$ that satisfies the naturality condition and is compatible with the comonadic structure through the counit and comultiplication. This structure allows the functor $F$ to "lift" the comonadic context into the functorial mapping, preserving the interaction between the comonad and the monoidal structure of the categories involved. Again, specific properties and definitions will depend on the context and categories, and the above is merely a quick sketch, so caveat emptor.

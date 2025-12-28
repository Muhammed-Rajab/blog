---
date: '2025-12-28T21:35:49+05:30'
draft: true
title: 'Fuckity fuck, Rotational Matrices go brr…'
---

ok, some context.

i have this yearly ritual of rewatching [3b1b’s *Essence of Linear Algebra*](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab), hoping that *this* time i’ll finally understand what everything’s about. i’ve been doing this since 9th grade. this is almost year five. time flies lol.

but until **this year**, i never bothered to ask myself the million-dollar question:

> **where the fuck does this rotation matrix come from?**

mind you, i’ve copied its implementation into my codebases more times than i can count, across multiple projects, multiple languages. you just plug in some angles (alpha, beta, gamma, whatever the fuck), multiply a vector, and boom — it rotates???

**wym bruh???**

this state of ignorance was about to get checked.

during one of my daily youtube doomscroll sessions, i came across a video by tsoding where he was demonstrating why [graphics APIs are largely irrelevant](https://www.youtube.com/watch?v=xNX9H_ZkfNE) if you actually understand the math and what you’re trying to achieve. somewhere in the video, he casually implements a 3D rotation matrix in C (i don't remember tho).

he’s someone i really look up to. his streams are pure gold if you’re even slightly interested in low-level programming or graphics. when he admitted that *he too* took rotation matrices for granted for a long time, i felt violently seen.

but then he mentioned a video where someone **derives** the rotation matrix.

finally. it was time.

i watched it and,

**OH MY FUCKING GOD.**

i already knew this shit.

not vaguely. not approximately.
i knew it *exactly*.
and i even remember where i learned it from.

let me show you.


## what’s a rotation matrix?

let’s stay in 2D for now.

say you have a point \( P = (1, 0) \). it lies on the x-axis. if you rotate it **90° counterclockwise**, it ends up at \( (0, 1) \).

a **rotation matrix** is just a compact way to store the information needed to perform this rotation.

you take the **position vector** of the point, multiply it by the matrix, and out comes the rotated vector.

no magic. just simple vector-matrix multiplication.


## can i use this for *any* angle?

yep.


## where does the matrix actually come from?

alright, let’s cook.

say we have a vector \( \vec{v} \):

$$
\vec{v} =
\begin{bmatrix}
x \\
y
\end{bmatrix}
$$

using basic trigonometry, we can describe this vector by it's magnitude and angle from the x-axis:

$$
\begin{aligned}
x &= |\vec{v}|\cos\alpha \\
y &= |\vec{v}|\sin\alpha
\end{aligned}
$$

where \( \alpha \) is the angle the vector makes with the x-axis.  
(unit circle shit. you know this.)

now, one important thing about rotation:

> **rotation does not change the magnitude of a vector.**  
> it only changes its direction.

so if we rotate this vector by an angle \( \beta \), the new components become:

$$
\begin{aligned}
x' &= |\vec{v}|\cos(\alpha + \beta) \\
y' &= |\vec{v}|\sin(\alpha + \beta)
\end{aligned}
$$

and yes, this is where those ancient high-school identities crawl out of the grave:

$$
\begin{aligned}
\cos(\alpha + \beta) &= \cos\alpha\cos\beta - \sin\alpha\sin\beta \\
\sin(\alpha + \beta) &= \cos\alpha\sin\beta + \sin\alpha\cos\beta
\end{aligned}
$$

plugging these in:

$$
\begin{aligned}
x' &= |\vec{v}|(\cos\alpha\cos\beta - \sin\alpha\sin\beta) \\
y' &= |\vec{v}|(\cos\alpha\sin\beta + \sin\alpha\cos\beta)
\end{aligned}
$$

now here’s the part where everything clicks.

we already know:

$$
|\vec{v}|\cos\alpha = x \quad \text{and} \quad |\vec{v}|\sin\alpha = y
$$

so substitute:

$$
\begin{aligned}
x' &= x\cos\beta - y\sin\beta \\
y' &= x\sin\beta + y\cos\beta
\end{aligned}
$$

and now we write that as a matrix multiplication:

$$
\begin{bmatrix}
x' \\
y'
\end{bmatrix} =
\begin{bmatrix}
\cos\beta & -\sin\beta \\
\sin\beta & \cos\beta
\end{bmatrix}
\begin{bmatrix}
x \\
y
\end{bmatrix}
$$

that’s it.

that’s the **2D rotation matrix**:

$$
R(\beta) =
\begin{bmatrix}
\cos\beta & -\sin\beta \\
\sin\beta & \cos\beta
\end{bmatrix}
$$


## so… what’s actually *inside* the matrix?

here’s the part no one explicitly tells you:

> **a matrix stores what happens to the basis vectors.**

in 2D, your basis vectors are:

* \( (1, 0) \) is the x-axis  
* \( (0, 1) \) is the y-axis  

rotate \( (1, 0) \) by \( \beta \):  
→ \( (\cos\beta, \sin\beta) \)

rotate \( (0, 1) \) by \( \beta \):  
→ \( (-\sin\beta, \cos\beta) \)

**those two results become the columns of the matrix.**

that’s it.

so when you multiply a vector by the rotation matrix, you’re just expressing that vector in terms of **rotated axes**.

it’s honestly wild how much stuff we learn in school that feels useless, until one day you see it applied somewhere real, and suddenly it *clicks*.

**CLOCK THAT SHIT 🤏.**

PS: here's the [link](https://www.youtube.com/watch?v=EZufiIwwqFA) to the video i watched in which the guy derives it soo good, uhhhhhhhhhhhhhhhhhhhhhhhhhh!!!!

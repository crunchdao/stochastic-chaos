---
title: "Interplay between Chaos and Stochasticity in Celestial Mechanics"
subtitle: ""
author: [Matteo Manzi, Stefano Guidolotti, Mattia Petrini]
date: "2022/07/31"
lang: "en"
colorlinks: true
titlepage: true
titlepage-text-color: "FFFFFF"
titlepage-rule-color: "360049"
titlepage-rule-height: 0
titlepage-background: "./figures/cover.pdf"
header-left: "\\hspace{1cm}"
header-right: "Page \\thepage"
footer-left: "Interplay between Chaos and Stochasticity in Celestial Mechanics"
footer-right: "CrunchDAO"
abstract: "This work is focused on the development of an open-source Julia-based repository for the analysis of chaos in dynamical systems, in particular for systems described by ordinary and stochastic differential equations, using Finite-Time Lyapunov exponents (FTLE). in particular for systems described by ordinary and stochastic differential equations, using Finite-Time Lyapunov exponents (FTLE). The novel application of this scalar field for stochastic processes allows one to generalize the definition of chaos in a probabilistic sense. This probabilistic generalization is useful for both of uncertainty quantification, and robust trajectory design. Bifurcating phenomena and invariant sets in time-dependant dynamical systems are discussed, particularly in the context of Lagrangian coherent structures. "
---

\section{Introduction}

Chaotic behavior is omnipresent in celestial mechanics dynamical systems and it is relevant for both the understanding and 
leveraging the stability of planetary systems, inner solar system in particular \cite{celletti}. 
The quantification of the probability of impacts of near Earth objects after close encounters with celestial bodies; 
the possibility of designing robust low energy transfer trajectories, not limited to invariant manifolds but also leveraging the 
weak stability boundary for the design of the ballistic captures trajectories in time-dependent dynamical systems; 
the characterization of diffusion processes in Nearly-Integrable Hamiltonian systems in celestial mechanics. 

Building on [@Szebehely82], [@ManziAAS2020; @VasileManzi] investigated a probabilistic generalization of chaos, in which uncertainty in initial conditions and dynamical parameters is considered.

Here we generalize, inspired by [@Balibrea-Iniesta], in order to introduce a quantification of chaos for stochastic processes.

\section{Metodology}
Given dynamical systems in the form:

\begin{equation}
    \dot{\mathbf{x}}=\mathbf{f}(\mathbf{x}, \mathbf{p})
\end{equation}
and introducing the variational equations:
\begin{equation}
    \frac{\drv}{\drv t} \frac{\partial \mathbf{x} }{\partial \mathbf{x_0}} = \frac{\partial \mathbf{f}}{\partial \mathbf{x}}\frac{\partial \mathbf{x}}{\partial \mathbf{x_0}}
\end{equation}
the Cauchy-Green (CG) strain tensor, which is positive definite, can be computed as:
\begin{equation}
    \Delta(\mathbf{x}, \mathbf{p}) = \left( \frac{\partial \mathbf{x}}{\partial \mathbf{x_0}}\right)^T \frac{\partial \mathbf{x}}{\partial \mathbf{x_0}}
\end{equation}
where its relative spectrum can be measured by the FTLE:
\begin{equation}
    \sigma(\mathbf{x}, \mathbf{p}, T)=\frac{1}{|T|}\ln(\sqrt{\lambda_{\max}(\Delta(\mathbf{x}, \mathbf{p}))})
\end{equation}
where $T$ is the time interval associated to the propagation, starting at $t_0$, and $\lambda_{\max}$ is the maximum eigenvalue of the Cauchy-Green Strain Tensor.

Generalizing for stochastic differential equations [@oksendal]:
\begin{equation}
    \drv \mathbf{X}=\mathbf{f}(\mathbf{X},t) \drv t + \mathbf{G}(\mathbf{X},t) \drv \mathbf{W_t}
\end{equation}
where 
\begin{equation}
\mathbf{X},\mathbf{f} \in \mathbb{R}^{n}
\end{equation}
\begin{equation}
\mathbf{W_t} \in \mathbb{R}^{m}, \mathbf{G} \in \mathbb{R}^{n \times m}.
\end{equation}

The equation consists of two major components. The deterministic drift denoted as $\mathbf{f}$ and the stochastic diffusion $\mathbf{G}$. $\mathbf{G}$ depends on $m$ Brownian processes expressed as $\mathbf{W_t}$. 
It is straightforward to derive the variational equations associated with a Stochastic Differential Equation:

\begin{equation}
\drv \frac{\partial \mathbf{X}}{\partial \mathbf{X_0}}=
\frac{\partial \mathbf{f}}{\partial \mathbf{X}}
\frac{\partial \mathbf{X}}{\partial \mathbf{X_0}} \drv t
+
\frac{\partial \mathbf{G}}{\partial \mathbf{X}}
\frac{\partial \mathbf{X}}{\partial \mathbf{X_0}} \drv \mathbf{W_t}
\end{equation}

\begin{equation}
    \label{eq:sftle}
    \sigma_{t_0}^T(\mathbf{X})=\frac{1}{|T|}\ln(\sqrt{\lambda_{\max}(\Delta(\mathbf{X}))})
\end{equation}

in which $X$ is a stochastic process, leading the Cauchy-Green Strain tensor to be a random matrix. The analysis
of its spectrum, leading to the FTLE in Equation \eqref{eq:sftle}, is therefore stricly related with random matrix theory [@potters_bouchaud_2020].

\section{Applications}
A number of dynamical systems can be analysed using this approach.
Introduced by B.V. Chirikov in [@CHIRIKOV1979263], one of the most popular mappings in the theory of dynamical systems is the so-called \emph{standard map} [@celletti]:
It is defined by the equations:
\begin{equation}
    \begin{cases}
    y'=y+\epsilon f(x) \\
    x'=x+y'
\end{cases}
\end{equation}
where $y\in\mathbb{R}$, $x\in\mathbb{T}\equiv \mathbb{R}/(2\pi\mathbb{Z})$, $\epsilon$ is a positive real parameter, called the perturbing parameter, and $f = f(x)$ is an analytic, periodic function.
The FTLE field of this discrete map is represented in Figure \ref{fig:stdmap}.

\begin{figure}[h]
    \centering
    \fbox{\includegraphics[width = .55 \textwidth]{figures/std_map.png}}
    \caption{Finite-Time Lyapunov Exponents scalar field of the \emph{standard map}.}
    \label{fig:stdmap}
\end{figure}

Another classical dynamical system is the periodically-perturbed pendulum:
\begin{equation}
\ddot{x}=(\alpha \cos5t -1 )\sin x
\end{equation}

In this case, the FTLE field, associated with an Ordinary Differential Equation, is represented in Figure \ref{fig:ppp}.

\begin{figure}[h]
    \centering
    \fbox{\includegraphics[width = .55 \textwidth]{figures/ppp_proceeding.png}}
    \caption{Finite-Time Lyapunov Exponents scalar field of the \emph{periodically-perturbed pendulum}.}
    \label{fig:ppp}
\end{figure}
 

As a final example, the Duffing oscillator:
\begin{equation}
\ddot{x}=\alpha \dot{x}+\beta x+\gamma x^3 + \epsilon\cos{t}
\end{equation}
is generalized into a Stochastic Differential Equation: 
\begin{equation}
    \begin{cases}
    \drv X_t= \alpha Y_t \\
    \drv Y_t = (\beta X_t + \gamma X_t^3)\drv t +\epsilon X_t \drv \mathrm{W_t} 
\end{cases}
\end{equation}

The FTLE field depicted in Figure \ref{fig:duff} is here associated with a Stochastic Differential Equation:

\begin{figure}[h]
    \centering
    \fbox{\includegraphics[width = .55 \textwidth]{figures/duffing.png}}
    \caption{Finite-Time Lyapunov Exponents scalar field of the \emph{Stochastic Duffing oscillator}.}
    \label{fig:duff}
\end{figure}

\section{Conclusions and Recommendations}
Diffusion mechanisms arise both from chaotic behaviour and stochastic perturbations. 
But there is also an interplay between the two, reducing the Lyapunov time of dynamical systems under investigation.
A stochastic framework for celestial mechanics has been introduced, among others, in \cite{manzibosch}, motivates the use of the a 
stochastic index for chaotic motion: results on the stabilty of planetary systems could be influenced by the integration of stochastic 
perturbations.
Finally, as a recommendation for future works, the integration of these developments and results in the library \textit{DynamicalSystems.jl} appears desirable.

# References
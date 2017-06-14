
$$
\newcommand{\mat}[1]{\mathbf{#1}}
\renewcommand{\vec}[1]{\boldsymbol #1}
\newcommand{\op}[1]{\hat{#1}}
\newcommand{\opd}[1]{{\hat{#1}^\dagger}}
% frequently used symbols to make changing them easy
\newcommand{\kappaMW}{\kappa_{\mu\mathrm{w}}}
\newcommand{\kappaMM}{\kappa_{\mathrm{mm}}}
\newcommand{\kappaMWint}{\kappa_{\mu\mathrm{w,int}}}
\newcommand{\kappaMMint}{\kappa_{\mathrm{mm,int}}}
\newcommand{\omegaMW}{\omega_{\mu\mathrm{w}}}
\newcommand{\omegaMM}{\omega_{\mathrm{mm}}}
\newcommand{\omegaPump}{\omega_{\mathrm{p}}}
\newcommand{\Pheating}{P_{\text{heating}}}
\newcommand{\nPump}{n_{\mathrm{p}}}
\newcommand{\Ebit}{E_{\text{qbit}}}

\newcommand{\kappaPump}{\kappa_{\mathrm{p}}}

\textrm{TeX Macros are included in this document.}
$$

[TOC]

#### How do we calculate the scattering rates for noise processes (2-body scattering)?####

We have noise Hamiltonian such as:
$$
\op{H}_\textrm{noise} = \exp(2i \omegaMW t)\chi\nPump\op{b}^\dagger\op{a}^\dagger  + \textrm{h.c.}
$$

##### Applying Pertrubation Theory Blindly#####

Assume that the Hamiltonian can cause the state to change from $|\psi\rangle=|00\rangle$ to $|11\rangle$. We can just try to blindly calculate the first-order scattering parameter by applying pertrubation theory to
$$
S_\textrm{fi} = \langle \phi_f| e^{-i\omega_ft_f}U^{}(t_f,t_i)e^{i\omega_it_i}|\phi_i\rangle
$$

###### Try 1 (Didn't work)######

We take this scattering parameter, and Dyson expansion of $U(t_f,t_i)$ to define $S_\textrm{fi}^{(1)}$ the first-order scattering term. Now we can substitute $\omega_f = -i(\kappaMW+\kappaMM)$, $\omega_i = 0$, $|\phi_i\rangle = |00\rangle$, $|\phi_f\rangle=|11\rangle$. 

We get:
$$
S_\textrm{fi}^{(1)}=-i\chi\nPump\int_0^t dt_1 e^{-(\kappaMW+\kappaMM)t_1-i2\omegaMW t_1} \\
= \frac{-i\chi\nPump}{-i2\omegaMW-(\kappaMW+\kappaMM)}\left( e^{-(\kappaMW+\kappaMM)t -i2\omegaMW t} - 1 \right)
$$
At large $t$, i.e. $t\rightarrow \infty$, we find that $S_\textrm{fi}^{(1)}\rightarrow i\chi \nPump / (-2i\omegaMW - (\kappaMW+\kappaMM))$. The probability of transition at time $t$ is 
$$
P(t)= |S_\textrm{fi}^{(1)}|^2=\frac{\chi^2 \nPump^2}{4\omegaMW^2}
$$
There are many things wrong with this expression. First, we can't extract an emission rate from this. The linewidth $\kappaMM$ or $\kappaMW$  don't show up in this expression!

The basic problem is that we've considered the confined mode of the system, but these aren't really representative the dynamics that can occur.

###### Try 2 (Didn't work)######

Let's substitute $\omega_f =0$, $\omega_i = 0$, $|\phi_i\rangle = |00\rangle$, $|\phi_f\rangle=|1 1 \rangle$. 

We get:
$$
S_\textrm{fi}^{(1)}=-i\chi\nPump\int_{-t/2}^{t/2} dt_1 e^{-i2\omegaMW t_1} \\
={-2\pi i\chi\nPump}\delta^{(t)}(2\omegaMW)
$$
where I use $\delta^{(t)}(\omega)$ the windowed delta function (over window t), and its property that $[\delta^{(t)}(\omega)]^2=\delta^{(t)}(\omega) t/2\pi$. We can calculate the scattering rate as 
$$
P(t)= |S_\textrm{fi}^{(1)}|^2=4\pi^2\chi^2\nPump^2\delta^{(t)}(2\omegaMW)t/(2\pi)
$$
This gives us a rate:
$$
\Gamma_\text{scattering}={2\pi \chi^2 n_p^2}\delta(2\omegaMW)
$$
Ok, we're a bit closer now. At least it's a rate, but this rate is still a delta funciton of some sort and we don't have a good reason to integrate over anything.

###### Try 3 (seems reasonable)######

Let's now go back to the original Hamiltonian, and this time, let's express $\op{a}$ and $\op{b}$ as linear combinations of extended modes — i.e. we're going to operate in the full mixed picture where we intially diagonalize the bath and the system and then express the operators in the interaction Hamiltonian as linear combinations of the full continuous diagonalized basis. Then we get something like:
$$
\op{a} = \int d\omega f_a(\omega)\op{A}(\omega)e^{-i\omega t},~\textrm{and}~~ \op{b} = \int d\omega f_b(\omega)\op{B}(\omega)e^{-i\omega t},
$$
What are $f_a(\omega)$ and $f_b(\omega)$? Their square needs to integrate to 1 for preserving commutators (symplectic). They are lorentzian (why?). What is their center frequency and linewidth? Ansatz:
$$
|f_a(\omega)|^2=\frac{\kappaMW/2\pi}{\omega^2+(\kappaMW/2)^2}\\
|f_b(\omega)|^2=\frac{\kappaMM/2\pi}{\omega^2+(\kappaMM/2)^2}
$$
Then the original Hamiltonian becomes:
$$
\op{H}_\textrm{noise} = \exp(-2i \omegaMW t)\chi\nPump\op{b}\op{a}  + \textrm{h.c.} \\
= \chi\nPump \int d\omega_1 d\omega_2 f_a(\omega_1)f_b(\omega_2)\op{A}(\omega_1)\op{B}(\omega_2)\exp(-i(2\omegaMW+\omega_1+\omega_2)t) + \textrm{h.c.}
$$
Now we assume a final state $|1_{\omega_1} 1_{\omega_2}\rangle$, and calculate again the scattering rate ($S_\textrm{fi} = \langle \phi_f| e^{-i\omega_ft_f}U^{}(t_f,t_i)e^{i\omega_it_i}|\phi_i\rangle$, with $|\phi_i\rangle = |\textrm{vac}\rangle$, $|\phi_f\rangle = |1_{\omega_1} 1_{\omega_2}\rangle$)::
$$
S_\textrm{fi}^{(1)}=-i\chi\nPump\int_{-t/2}^{t/2} dt_1 e^{-i(2\omegaMW+\omega_1+\omega_2) t_1}f_a(\omega_1)f_b(\omega_2) \\
={-2\pi i\chi\nPump}\delta^{(t)}(2\omegaMW+\omega_1+\omega_2)f_a(\omega_1)f_b(\omega_2)
$$
We can calculate the scattering rate as 
$$
P(t)= |S_\textrm{fi}^{(1)}|^2=4\pi^2\chi^2\nPump^2|f_a(\omega_1)f_b(\omega_2)|^2\delta^{(t)}(2\omegaMW+\omega_1+\omega_2)t/(2\pi)
$$
This gives us a rate:
$$
\Gamma_\text{scattering}(\omega_1,\omega_2)=2\pi\chi^2\nPump^2|f_a(\omega_1)f_b(\omega_2)|^2\delta^{(t)}(2\omegaMW+\omega_1+\omega_2)
$$
which we can integrate over all $\omega_1$ and $\omega_2$:
$$
\Gamma_\textrm{scattering} = 2\pi \chi^2 \nPump^2 \int \int d \omega_1 d \omega_2 |f_a(\omega_1)|^2|f_b(\omega_2)|^2\delta^{(t)}(2\omegaMW+\omega_1+\omega_2)
$$
Let's integrate out $\omega_1$ first by approximating $|f_a(\omega_1)|^2 = \delta(\omega_1)$ since that has the narrowest linewidth
$$
\Gamma_\textrm{scattering} = 2\pi \chi^2 \nPump^2 \int d \omega_2 |f_b(\omega_2)|^2\delta^{(t)}(2\omegaMW+\omega_2)
$$
Now we integrate $\omega_2$,
$$
\Gamma_\text{scattering} = \frac{\chi^2 \nPump^2 \kappaMM}{4\omegaMW^2}
$$

Does this give the correct back-action heating thermal occupation we get from Heisenberg-Langevin equations? Yes; Let's refer to the optomechanics case where we have for a system being driven weakly on the red side we get $\bar{n}=\gamma_i n_b / \gamma_t + \gamma_{OM}\kappa^2/\gamma_t(4\omega_m)^2 = G^2\kappa/4\gamma_t\omega_m^2$, where we assume for the last equality that $\gamma_{OM}=4G^2/\kappa$  and $n_b=0$. This agrees with the scattering term calculated above if we calculate the average thermal occupation by taking the scattering rate and setting it equal to the cavity bandwidth: $\Gamma_\text{scattering}=\gamma_t \bar{n}$.

#### How do we calculate the scattering rates for noise processes (3-body scattering)?

We have noise Hamiltonian such as:
$$
\op{H}_\textrm{noise} = \chi\sqrt{\nPump}(\op{c}+\op{c}^\dagger)\op{a}^\dagger\op{a}
$$

##### Applying Pertrubation Theory Blindly (following closely try 3)

Again, we express the modes in the diagonalized basis:
$$
\op{a} = \int d\omega f_a(\omega)\op{A}(\omega)e^{-i\omega t},~\textrm{and}~~ \op{c} = \int d\omega f_c(\omega)\op{C}(\omega)e^{-i\omega t},
$$
Note also that
$$
\opd{a} = \int d\omega f^\ast_a(\omega)(\op{A}(\omega))^\dagger e^{i\omega t} = \int d\omega f^\ast_a(-\omega)(\op{A}(-\omega))^\dagger e^{-i\omega t} \\
=  \int d\omega f^\ast_a(-\omega)\opd{A}(\omega) e^{-i\omega t}
$$
With:
$$
|f_a(\omega)|^2=\frac{\kappaMW/2\pi}{\omega^2+(\kappaMW/2)^2}\\
|f_c(\omega)|^2=\frac{\kappaPump/2\pi}{\omega^2+(\kappaPump/2)^2}
$$
Now we have to choose the inital and final states; those could be terms like $|01_\omega\rangle\rightarrow|1_\delta1_{\omega-\delta}\rangle$ which preserve energy. Notice, that if the initial state has the mode with annihilation operator $\op{a}$ in the vacuum state, then the only scattering between process between Fock states that can happen that preserves energy is $|00\rangle \rightarrow |00\rangle$, because $\langle \opd{a}\op{a}\rangle=0$. 

Then the original Hamiltonian becomes:
$$
\op{H}_\textrm{noise} =  \chi\sqrt{\nPump}(\op{c}+\op{c}^\dagger)\op{a}^\dagger\op{a} \\
= \chi\sqrt{\nPump} \int d\omega_1 d\omega_2  d\omega_3 [f_c(\omega_1)\op{C}(\omega_1) + f^\ast_c(-\omega_1)\opd{C}(\omega_1)]\times \\
[f^\ast_a(-\omega_2)f_a(\omega_3)\opd{A}(\omega_2)\op{A}(\omega_1)]\exp(-i(\omega_1+\omega_2+\omega_3)t).
$$
Now we assume a transition $|01_\omega\rangle\rightarrow|1_\delta1_{\omega-\delta}\rangle$, and calculate again the scattering rate ($S_\textrm{fi} = \langle \phi_f| e^{-i\omega_ft_f}U^{}(t_f,t_i)e^{i\omega_it_i}|\phi_i\rangle$, with $|\phi_i\rangle = |01_\omega\rangle$, $|\phi_f\rangle = |1_\delta1_{\omega-\delta}\rangle$):
$$
S_\textrm{fi}^{(1)}=-i\chi\sqrt{\nPump} \int_{-t/2}^{t/2} dt_1 e^{-i(\omega_1+\omega_2+\omega_3) t_1}f^\ast_c(-\omega_1)f^\ast_a(-\omega_2)f_a(\omega_3) \\
={-2\pi i\chi\sqrt{\nPump}}\delta^{(t)}(\omega_1+\omega_2+\omega_3)f^\ast_c(-\omega_1)f^\ast_a(-\omega_2)f_a(\omega_3)
$$
We can calculate the scattering rate as 
$$
P(t)= |S_\textrm{fi}^{(1)}|^2=4\pi^2\chi^2\nPump|f^\ast_c(-\omega_1)f^\ast_a(-\omega_2)f_a(\omega_3)|^2\delta^{(t)}(\omega_1+\omega_2+\omega_3)t/(2\pi)
$$
This gives us a rate:
$$
\Gamma_\text{scattering}(\omega_1,\omega_2,\omega_3)=2\pi\chi^2\nPump|f_c(\omega_1)|^2 |f_a(\omega_2)f_a(\omega_3)|^2\delta^{(t)}(\omega_1+\omega_2+\omega_3)
$$
which we can integrate over all $\omega_1$, $\omega_2$ and $\omega_3$:
$$
\Gamma_\textrm{scattering} = 2\pi \chi^2 \nPump \int \int \int d \omega_1 d \omega_2 d \omega_3 |f_c(\omega_1)|^2 |f_a(\omega_2)f_a(\omega_3)|^2\delta^{(t)}(\omega_1+\omega_2+\omega_3)
$$
Let's integrate out $\omega_2,\omega_3$ first by approximating $|f_a(\omega)|^2 = \delta(\omega)$ since that has the narrowest linewidth
$$
\Gamma_\textrm{scattering} = 2\pi \chi^2 \nPump \int d \omega_1 |f_c(\omega_1)|^2\delta^{(t)}(\omega_1)
$$
Now we integrate $\omega_1$,
$$
\Gamma_\text{scattering} = \frac{4\chi^2 \nPump}{\kappaPump}
$$
This is the measurement rate that we would expect for a dispersive measurement.

#### Comparing the Scattering Rates####


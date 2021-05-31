# Power Spectral Density (PSD)

## Energy and Power

Let $X[n]$ be a discrete time random process and $x[n]$ be a single realization of this process.

The energy of the discrete time signal $x[n]$ is defined as:

$$
E = \sum_{n=-\infty}^{\infty}|x[n]|^2
$$ (1)

the instantaneous power of the signal as:

$$
P_{\text{inst}}[n] = |x[n]|^2
$$(2)

and the time averaged power of the signal is defined as:

$$
\begin{aligned}
P &= \lim_{N\rightarrow\infty}\frac{1}{2N}\sum_{n=-N}^{N}|x[n]|^2
\end{aligned}
$$(3)

## Autocorrelation

For a signal $x[n]$ the deterministic autocorrelation function is defined as:

$$
\begin{aligned}
R[k] & = \sum_{n=-\infty}^\infty x[n]x[n+k]
\end{aligned}
$$ (4)

A discrete time process $X[n]$ has an autocorrelation function $R_{X}[n_1, n_2]$ i.e. autocorrelation between random variable at time $n_1$ and $n_2$ defined as:

$$
\begin{aligned}
R_{X}[n_1,n_2] &= \mathbb{E}[X[n_1]X[n_2]]\\
\end{aligned}
$$ (5)

When considering first and second order moments only, we need not consider the specific realization $x[n]$ as expectations are evaluated over all possible outcomes considering all such realizations as:

$$
\mathbb{E}[X[n_1]X[n_2]] = \sum_{X_1=-\infty}^{+\infty}\sum_{X_2=-\infty}^{+\infty}X_1X_2p_{X[n_1], X[n_2]}(X_1, X_2)
$$ (6)

where $p_{X[n_1], X[n_2]}(X_1, X_2)$ is the pmf given as:

$$
p_{X[n_1], X[n_2]}(X_1, X_2) = P[X[n_1]=X_1, X[n_2]=X_2]
$$ (7)

If the process is at least **wide-sense stationary** then second-order moments (including the auto-correlation) are independent of time and depend only on the time interval $l = n_1-n_2$ and can equivalently be written as:

$$
\begin{aligned}
R_{X}[n_1,n_2] &= R_{X}[n_1-n_2] \\
               &= R_{X}[n_2-n_1] \\
               &= R_{X}[l]
\end{aligned}
$$ (8)

where the second equality follows from wide-sense stationarity.

The autocorrelation function $R_{X}[l]$ can thus be written as

$$
\begin{aligned}
R_{X}[l] &= \mathbb{E}[X[n]X[n+l]]\\
\end{aligned}
$$ (9)

We thus see that the expected instanteous power of a real process is equivalent to the autocorrelation sequence evaluated at $l=0$ for all $n$

$$
\begin{aligned}
\mathbb{E}[X[n]^2] &= \mathbb{E}[|X[n]|^2]\\
&= R_X[0]
\end{aligned}
$$(10)

where the first equality follows from the signal having no complex component.

## Einstein-Wiener-Khintchine Theorem

We define the power spectral density (PSD) as $S_X(j\omega) = \mathscr{F}\{R_X[l]\}$. We have the following fourier transform pair for $R_{X}[l]$ and $S_{X}(j\omega)$

$$ 
\begin{aligned}
R_{X}[l] &= \frac{1}{2\pi}\int_{2\pi}S_{X}(j\omega)e^{j\omega l}d\omega \\
S_{X}(j\omega) &= \sum_{l=-\infty}^{+\infty}R_{X}[l]e^{-j\omega l}
\end{aligned}
$$ (11)

This gives us the following:

$$
\begin{aligned}
&\Rightarrow R_{X}[0]\space{} &= \frac{1}{2\pi}\int_{2\pi}S_{X}(j\omega)d\omega \\
&\Rightarrow \mathbb{E}[X[n]^2]&= \frac{1}{2\pi}\int_{2\pi}S_{X}(j\omega)d\omega
\end{aligned}
$$ (12)

Where the second equality follows from equation **(10)**

## Motivation

We now motivate this definition of the PSD.

**Note**: In the following developement we have assumed that the system specified by $h[n]$ is BIBO stable and the expected power of the process squared $\mathbb{e}[X[n]^2]$ is finite.

Consider passing a signal $x[n]$ (a realization of process $X[n]$) through an ideal bandpass filter with frequency components centered at frequencies $-w_0$ and $w_0$ and with impulse response $h[n]$ and frequency response $H(j\omega)$. The output signal $y[n]$ is then

$$
\begin{aligned}
y[n] &= \sum_{k=-\infty}^{+\infty}x[k]h[n-k]= \sum_{k=-\infty}^{+\infty}h[k]x[n-k]
\end{aligned}
$$ (13)

The output process $Y[n]$ also turns out to be stationary and its autocorrelation can be found as:

$$
\begin{aligned}
R_Y[n] &= \mathbb{E}[Y[n]Y[n+l]]\\
&= \overline{R}_h[l] * R_X[n]\\
\\
\text{where} \space \overline{R}_h[l] &= \int_{-\infty}^{+\infty}h(t+l)h(t)
\end{aligned}
$$ (14)

**Note**: *I have not included the proof of the above in the interest of space. It relies on interchanging the order of the expectation operator with the summation and thus relating the expected value of the output to the expected value of the input multiplied by a delayed version of itself i.e. the auto-correlation of the input. Interested readers may find the complete proof in Oppenheim and Verghese (Oppenheim & Verghese, 2017, eq. 10.62, 10.66, 10.68). The authors there introduce the cross-correlation $R_{XY}$ as an intermediate step.*

From our definition of the power spectral density then we have from **(14)**:

$$
S_Y(j\omega) = |H(j\omega)|^2S_X(j\omega)
$$(15)

The expected instantaneous power from **(11)** is then:

$$
\begin{aligned}
\mathbb{E}[y[n]^2] &= R_Y[0]\\
&= \frac{1}{2\pi}\int_{\langle2\pi\rangle}S_Y(j\omega)d\omega\\
&= \frac{1}{2\pi}\int_{\langle2\pi\rangle}|H(j\omega)|^2S_X(j\omega)d\omega\\
&= \frac{1}{2\pi}\int_{\text{passband}}S_X(j\omega)d\omega\\
\end{aligned}
$$ (16)

Thus the PSD of a signal $S_X(j\omega)$ describes the distribution of the power of a signal over frequencies and can be seen to be the *density* of the *power spectrum*.

## Parseval's Relation and Periodogram

We have so far considered the instantaneous power or rather the expectation with respect to the instantaneous power for a random process. But recall that we also defined the time averaged power for a signal. We now consider an alternative approach to the concept of Power Spectral Density considering the time average of a **specific signal**. This approach is at the heart of the Einstein-Wiener-Khintchine theorem.

For a **signal** Parseval's Relation gives us a relationship between the time domain energy representation and the frequency domain energy representation as:

$$
\sum_{n=-\infty}^{+\infty}|x[n]|^2 = \frac{1}{2\pi}\int_{\langle 2\pi\rangle}|X(j\omega)|^2d\omega
$$(17)

**Note**: Above and in the following discussion, $X(j\omega)$ refers to the Fourier transform of the signal $x[n]$ not the random process that generated this signal which is $X[n]$.

We define the energy density spectrum of a **signal** as:

$$
|X(j\omega)|^2
$$(18)

Since this is defined as the energy density spectrum, we are tempted to see what happens when we divide this by the total time $T$ where the signal is non-zero. We find:

$$
\frac{1}{T}|X(j\omega)|^2
$$(19)

and taking the expectation of this value:

$$
\begin{aligned}
\mathbb{E}[\frac{1}{T}|X(j\omega)|^2] &= \frac{1}{T}\mathbb{E}[X(j\omega)X^*(j\omega)]\\
&= \frac{1}{T}\mathbb{E}\bigg[\sum_{n = 1}^{k} x[n]e^{-j\omega n}\sum_{m = 1}^{k} x[m]e^{j\omega m}\bigg]\\
&= \frac{1}{T}\sum_{n = 1}^{k}\sum_{m = 1}^{k}\mathbb{E}[x[n]x[m]]e^{-j\omega(n-m)}\\
&= \frac{1}{T}\sum_{n = 1}^{k}\sum_{m = 1}^{k}\mathbb{E}[X[n]X[m]]e^{-j\omega(n-m)}\\
&=  \frac{1}{T}\sum_{n = 1}^{k}\sum_{m = 1}^{k}R_X[n-m]e^{-j\omega(n-m)}
\end{aligned}
$$(20)

where the fourth equality follows from the expectation of a signal actually corresponding to the expectation of the generating random process.

Some inspired algebraic manipulation, that has been skipped here (Leon-Garcia, 2008. eq. 10.35), gives us the following from the last equation

$$
\begin{aligned}
\mathbb{E}[\frac{1}{T}|X(j\omega)|^2] &= \sum_{n=-(T-1)}^{T-1}\bigg\{1 - \frac{|n|}{T}\bigg\}R_X[n]e^{-j\omega n}
\end{aligned}
$$(21)

Clearly, as $T \rightarrow \infty$ we see $\mathbb{E}[\frac{1}{T}|X(j\omega)|^2] \rightarrow S_X(j\omega)$.

This can be further strengthened if the random process $X[n]$ is ergodic in its second moment.

This section has given us that even the time average of a finite realization of a random process may be used to estimate the spectral density. The estimator that we get from **(19)** is biased but consistent and is known as the periodogram estimate.

$$
\widetilde{p_T}(j\omega) = \frac{1}{T}|X(j\omega)|^2
$$ (22)

## References

1. Leon-Garcia, A. (2008). Probability, statistics, and random processes for electrical engineering. Prentice Hall.
2. Oppenheim, A., & Verghese, G. (2017). Signals, Systems & Inference. Pearson.
3. Oppenheim, A., Willsky, A., & Nawab, S. (1997). Signals and systems. Prentice-Hall.
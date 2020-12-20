
# Chapter V. Digital filtering

### Response of LTI systems to harmonic signals

- We consider an LTI system with $h[n]$

- Input signal = complex harmonic (exponential) signal
$x[n] = A e^{j \omega_0 n}$

- Output signal = convolution
$$\begin{split}
y[n] &= \sum_{k=-\infty}^\infty h[k] x[n-k]\\
&= \sum_{k=-\infty}^\infty h[k] e^{-j \omega_0 k} A e^{j \omega_0 n}\\
&= H(\omega_0) \cdot x[n]
\end{split}$$

- $H(\omega_0)$ = Fourier transform of $h[[n]$ evaluated for $\omega = \omega_0$


### Eigen-function

- Complex exponential signals are **eigen-functions** (funcții proprii)
of LTI systems:
    - output signal = input signal $\times$ a (complex) constant

- $H(\omega_0)$ is a constant that multiplies the input signal
    - Amplitude of input gets multiplies by $|H(\omega_0)|$
    - Phase of input signal is added with $\angle H(\omega_0)$

- Why are sin/cos/exp functions important?
    - If input signal = sum of complex exponential (= coses + sinuses),
    - since the system is linear,
    - then output = same sum of complex exponentials, each scaled with some coefficients

### Response to cosine and sine

- Cosine / sine = sum of two exponentials, via Euler
  $$\cos(\omega t) = \frac{e^{j \omega t} + e^{-j \omega t}}{2}$$
  $$\sin(\omega t) = \cos(\omega t - \frac{\pi}{2})$$

- System is linear and real => 
    - amplitude is multiplied by $|H(\omega_0)|$
    - phase increases by $\angle H(\omega_0)$

- See proof at blackboard

### Frequency response

- Naming:
    - $H(\omega)$ = **frequency response** of the system
    - $|H(\omega)|$ = **amplitude response** (or magnitude response)
    - $\angle H(\omega)$ = **phase response**

- Magnitude response is non-negative: $|H(\omega)| \geq 0$
- Phase response is an angle: $\angle H(\omega) \in (-\pi, pi]$
    - Phase response may have jumps of $2 \pi$ (wrapped phase)
    - Stitching the pieces in a continuous function = phase *unwrapping*
    - Unwrapped phase: continuous function, may go outside interval $(-\pi, pi]$
    - Example: at blackboard

### Permanent and transient response

- The above harmonic signals start at $n = -\infty$, not at 0.

- What if the signal starts at some time $n=0$?

- Total response = transient response + permanent response
    - transient response  goes towards 0 as $n \to \infty$
    - permanent response = the above 

- So the above relations are valid only in **permanent regime**
    - i.e. after the transient regime has passed
    - i.e. after the transient response has practically vanished
    - i.e. when the signal started very long ago (from $n = -\infty$)

- Example at blackboard

### Permanent response of LTI systems to periodic inputs

- Assume the input $x[n]$ is periodic with period N
- Then it can be represented as a Fourier series:
$$x[n] = \sum_{k=0}^{N-1}c_k e^{j 2 \pi k n / N}$$

- Since the system is linear, the output to each component $k$ is
$$c_k H\left(\frac{2 \pi}{N}k\right) e^{j 2 \pi k n / N}$$

- So the total output is:
$$y[n] = \sum_{k=0}^{N-1}c_k H\left(\frac{2 \pi}{N}k\right) e^{j 2 \pi k n / N}$$

- The output is still periodic, same period, same frequencies

### Response of LTI systems to non-periodic signals

- The output = input convolution with impulse response
$$y[n] = x[n] * h[n]$$

$$Y(\omega) = X(\omega) \cdot H(\omega)$$

- In polar form:
    - modulus get multiplied
    - phases get added

- The system **attenuates/amplifies** the input frequencies and **changes their phases**

- $H(\omega)$ = the **transfer function**
- $H(z)$ = the **system function**
- $H(\omega) = H(z=e^{j\omega})$ if unit circle is in CR

### Power spectral density

- $S_{zz}(\omega) = |Y(\omega)|^2 = |H(\omega)|^2 \cdot S_{xx}(\Omega)$ 

- The poles and zeros of $S(\omega)$ come in pairs ($z, 1/z$ and $p, 1/p$)

### Digital filters

- LTI systems are also known as **filters** because their transfer function shapes (*filters*) the frequencies of the input signals

- The transfer function can be found from $H(z)$ and $z = e^{j \omega}$

- Alternatively, the transfer function can be found by the **geometrical method** based on the locations of poles and zeros

### Ideal filters

- Ideal low-pass filter: example at whiteboard

- Ideal band-pass filter: example at whiteboard

- Ideal high- pass filter: example at whiteboard

- Ideal band-stop filter: example at whiteboard

- Ideal all-pass filter (*changes the phase*): idem

### Linear-phase filters

- Consider a constant filter with **linear phase** function:
$$H(\omega) = C \cdot e^{- j \omega n_0}$$

- The output signal is
$$Y(\omega) = X(\omega) \cdot C \cdot  e^{- j \omega n_0}$$

$$y[n] = C \cdot x[n-n_0]$$

- Linear phase means **just a delaying** of the input signal
    - Fourier property: $x[n-n_0] <--> X(\omega) e^{-j \omega n_0}$

### Group delay

- = The time delay experienced by a component of frequency $\omega$ when passing through the filter

- **Group delay** of the filter:
$$\tau_g(\omega) = \frac{d \Theta(\omega)}{d \omega}$$

- Linear phase = constant group delay = all frequencies delayed the same = whole  signal delayed

### Filter distortions

- When a filter is non-ideal:
    - non-constant amplitude --> amplitude distortions
    - non-linear phase --> phase distortions

- Phase distortions may be tolerated by certain applications
    - e.g. human ears are insensitive to phase distortions of sounds


### Filter order

- The **order** of a filter = maximum degree in numerator or denominator of $H(z)$
    - i.e. largest power of $z$

- Any filter can be implemented, in general, with this number of unit delay blocks ($z^{-1}$)

- Higher order -> better filter transfer function
    - closer to ideal filter
    - more complex to implement
    - more delays (bad)

- Lower order
    - worse transfer function (not close to ideal)
    - simpler, cheaper
    - faster response


### Filter design by pole and zero placements

- Based on geometric method

- The gain coefficient must be found by separate condition
    - i.e. specify the desired magnitude response at one frequency

- Examples at blackboard


### Linear-phase FIR filters

What type of filters can have linear phase?

- IIR filters cannot have linear phase (no proof) 
- Only FIR filters can have linear phase, and only if they satisfy some symmetry conditions

### Symmetry conditions for linear-phase FIR

- Let filter have an impulse response of length $M$ (order is $M-1$)

- The filter coefficients are $h[0]$, ... $h[M-1]$

- Linear-phase is guaranteed in two cases

- **Positive symmetry**
$$h[n] = h[M-1-n]$$

- **Negative symmetry (anti-symmetry)**
$$h[n] = -h[M-1-n]$$

### Cases of linear-phase FIR

- Proofs at blackboard

1. Positive symmetry, M = odd
2. Positive symmetry, M = even
3. Negative symmetry, M = odd
4. Negative symmetry, M = even

- Check constraints for $H(0)$ and $H(\pi)$
- For what types of filters is each case appropriate?


### Particular classes of filters

- Digital resonators
    -  = very selective band pass filters
    - poles very close to unit circle
    - may have zeros in 0 or at 1/-1

- Notch filters
    - have zeros exactly on unit circle
    - will completely reject certain frequencies
    - has additional poles to make the rejection band very narrow

- Comb filters
    - = periodic notch filters

### Digital oscillators

- Oscillator = a system which produces an output signal even in absence of input

- Has a pair of complex conjugate poles **exactly on unit circle**

- Example at blackboard


### Inverse filters

- Sometimes is necessary to **undo** a filtering
    - e.g. undo attenuation of a signal passed through a channel

- Inverse filter: has inverse system function:
$$H_I(z) = \frac{1}{H(z)}$$

- Problem: if $H(z)$ has zeros outside unit circle, $H_I(z)$ has poles
outside unit circle --> unstable

- Examples at blackboard


# Sampling of Analog Signals


## Signals

- Signal = a measurable quantity which varies in time, space or some other variable

- Example: a voltage signal

- Represented as a mathematical function, e.g. $v(t)$.

- Off Topic: Glossary
    - "e.g." = "*exampli gratia*" (lat.) = "for example" (eng.) = "de exemplu" (rom.)
    - "i.e." = "*id est*" (lat) = "that is" (eng.) = "adică" (rom.)


## Signal dimension

- Unidimensional (1D) signal: = a function of a signal variable
    - Example: $v(t)$ = a function of time

- Multidimensional (2D, 3D, ...) signal = a function of multiple variables
    - Example: intensity of an image across a photo, $I(x,y)$, depends on the two
    coordinates $x$ and $y$ that specify the position

## Continuous and discrete signals

- Continuous (analog) signal = function of a continuous variable
    - Signal has a value for possible value of the variable in the defined range
    - The variable may be defined only in a certain range (e.g. $t \in [0,100]$),
    but it is a compact range

- Discrete signal = function of a discrete variable
    - Signal has values only at certain discrete values (*samples*)
    - Indexed with natural numbers: $x[-1]$, $x[0]$, $x[1]$ etc.
    - Outside the samples, the signal is **not defined**

## Notation

- We use the following notation throughout these lectures

- Continuous signals
    - Has **round parantheses**, e.g. $x_a(t)$
    - Sometimes has the $a$ subscript
    - The variable is usually $t$ (time)
    - $x(2.3)$ = the value of the signal $a(t)$ at $t = 2.3$

- Discrete signals
    - Has **square brackets**, e.g. $x[n]$
    - The variables are denoted as $n$ or $k$ (suggest natural numbers)
    - $x[3]$ = the value of the signal $x[n]$ for $n = 3$
    - $x[1.5]$ = does not exist

## Signals with continuous and discrete values 

- The signal values can be continuous or discrete
    - Example: signal values stored as 8-bit or 16-bit values

- On digital systems, signals always have discrete values due to finite number precision

## Discrete frequency

- A signal is **periodic** if the values repeat themselves after a certain time (**period**)

- Frequency = inverse of period

- Continuous signals:
$$x_a(t) = x(t + T)$$
    - $T$ is usually measured in seconds (or some other unit)
    - $F = \frac{1}{T}$ is measured in Hz = $\frac{1}{s}$ (Hertz)

- Discrete signals:
$$x[n] = x[n + N]$$
    - $N$ **has no unit**, because it is just a number
    - $f = \frac{1}{N}$ **has no unit** also

## Domain of existence of frequency

- Continuous signals
    - Period $T$ can be as small as possible $T \to 0$
    - Therefore $F$ could go up to $\infty$

- Analog signals
    - Smallest period is $N = 2$ (excluding $N=1$, constant signals)
    - Largest possible frequency is $f_{max} = \frac{1}{2}$
    - Consequence of using natural numbers to index the samples (x[0], x[1], x[2]...),
    without any physical unit attached

## Sampling

- Taking the values from an analog signal at certain discrete moments of time, usually periodic

- Distance between two samples = **sampling period** $T_s$

- **Sampling frequency** $F_s = \frac{1}{T_s}$

- Why sampling?
    - Converts continuous signals to discrete
    - Processing of continuous signals is expensive
    - Processing of discrete signals is cheap (digital devices)
    - Sometimes nothing is lost due to sampling 

## Sampling equation

- Sampling of the continuous signal $x_a$:
$$x[n] = x_a(n \cdot T_s)$$

- The $n$-th value of the discrete signal $x[n]$ is the value of the
analog signal $x_a(t)$ taken after $n$ sampling periods, at $t = n \cdot T_s$

## Sampling of harmonic signals

- Let's sample a cosine: $x_a(t) = cos (2 \pi F t)$

$$\begin{split}
x[n] =& x_a(n T_s) \\
=& cos(2 \pi F n T_s)\\
=& cos(2 \pi F n \frac{1}{F_s})\\
=& cos(2 \pi \underbrace{\frac{F}{F_s}}_{f} n)
\end{split}$$

- Sampling a continuous cosine (or sine) produces a discrete cosine (or sine)

- The discrete frequency is $f = \frac{F}{F_s}$

## Sampling theorem (Nyquist-Shannon)

- If a signal that has maximum frequency $F_{max}$ is sampled with a a sampling frequency 
$$F_s \ge 2 F_{max},$$
- then it can be perfectly reconstructed from its samples using the formula:
$$x_a(t) = \sum_{n=-\infty}^{+\infty} x[n] \cdot \frac{sin(\pi (F_s t - n))}{\pi (F_s t - n)}.$$



## Comments on the sampling theorem
- All the information in the original signal is contained in the samples, 
provided the sampling frequency is high enough
- We can process discrete samples instead of the original analog signals
- Sampling with $F_s \ge 2F_{max}$ makes the discrete frequency smaller than 1/2 $$f = \frac{F}{F_s} \leq \frac{F_{max}}{F_s} \leq \frac{1}{2}$$

## Aliasing

- http://www.dictionary.com/browse/alias:
    - “alias”: a false name used to conceal one’s identity; an assumed name

- What happens when the sampling frequency is not high enough?

- Every discrete frequency that exceeds $f_{max} = \frac{1}{2}$ is **identical** (an alias) to a frequency
that is lower than $f_{max} = \frac{1}{2}$

- Proof: 
    - Consider $x[n] = cos(2 \pi f n)$, $f > \frac{1}{2}$
    - We can always subtract $2 \pi n$ since $cos()$ is periodical
    - This means reducing $f$ with 1
    - Thus we can always end up a frequency $f' \in [-1/2, 1/2]$ (up to a sign change)

## Aliasing (continued)


$$cos (2 \pi (\frac{1}{2} + \epsilon)n) = cos (2 \pi (\frac{1}{2} - \epsilon)n)$$

$$sin (2 \pi (\frac{1}{2} + \epsilon)n) = - sin (2 \pi (\frac{1}{2} - \epsilon)n)$$

- Aliasing only affects digital signals

- Sampling with $F_s \ge 2 F_{max}$ ensures $f \le \frac{1}{2}$, so no aliasing


## The problem of aliasing

- Sampling different analog signals, with different frequencies, leads to exactly the
same samples

- How can be know from what signal did the samples come from? Impossible.

- Better remove from the signal the frequencies larger than $\frac{F_s}{2}$, 
otherwise they will be similar to a different frequency and create confusion

- Anti-alias filter: a low-pass filter situated before a sampling circuit, 
rejecting all frequencies $F > \frac{F_s}{2}$ from the signal before sampling
    - Standard practice in the design of processing systems
   
## Signal reconstruction from samples   
- A discrete frequency $f \in [-\frac{1}{2}, \frac{1}{2}]$ will be reconstructed as follows:
$$x_r(t) = x[\frac{t}{T_s}] = x[t \cdot F_s]$$

- For a discrete frequency outside the $[-\frac{1}{2}, \frac{1}{2}]$ interval
    - Reconstruction of the original frequency is impossible
    - The frequency is replaced with the aliased frequency $f'$ from the interval $[-\frac{1}{2}, \frac{1}{2}]$

- Reconstruction always produces signals with frequencies in $[-\frac{Fs}{2}, \frac{Fs}{2}]$
   
- Only signals sampled according to the sampling theorem will be reconstructed identically
    
## Signal quantization and coding   

- In practice, the values of the samples are rounded to fixed levels, e.g. 8-bit, 16-bit values.

- This "rounding" is known as **quantization**

- The "rounding error" is known as **quantization error** 

- Converting the value in binary form is known as **coding**

## A/D and D/A conversion

- Sampling + quantization + coding is usually done by an **Analog to Digital Converter (ADC)** 
    - It takes an analog signal and produces a sequence of binary-coded values
   
- Reconstructing an analog signal from numeric samples is done by a **Digital to Analog Converter (DAC)**
    - Usually reconstruction is not based on sampling theorem equation, which is too complex, but with simpler empiric approaches.
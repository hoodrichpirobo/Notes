$t=\frac{1}{f}$
If we have a frequency of $f=200MHz \rightarrow t=\frac{1}{2000MHz} = 0.005 \times 10^-6 s = 5 \times 10 ^{-9} s$
Remember that $Mega=10^6, nano=10^{-9}$
We define speedup time as $S_{i}= \frac{T_{base}}{T_{improved}}>1$
For example, suppose that we have $S=2$
Another way to represent the speedup time is $S=1+\frac{n}{100}$
$S=\frac{T_{base}}{T_{improved}} = \frac{100s}{75s} = 1.33$ times more faster
	$=1 + \frac{33}{100}$ will be 33% faster

$\underline{Ex}$
	What is S if the improved system is 200% faster?
	
		$S=1+\frac{200}{100}=3$

Now where are going to dive into what is the execution time of a program.

	$T_{exec} = cycles \times t = I \times \frac{cycles}{I} \times t$
	$CPI = \frac{cycles}{I}$
	$CPI = 0.80 \times 1 + 0.20 \times 2$

We will be using RISC instead of pipelining or other stuff

Composition of Speedups
$\underline{Ex}$
	$T_{base} = I \times CPI \times t$
	Two possible improvements
	a) Parallelize execution in 2 cores
		$T_{a)} = \frac{I}{2} \times CPI \times t$
		$S_{a)}=\frac{T_{base}}{T_{a)}} = ..$

	b) Increase f in 50%
	
	$1+\frac{50}{100}=1.5$
	$f_{b)} = 1.5f_{base}$
	$\frac{1}{t_{b}} = 1.5\times\frac{1}{t_{base}}$
	$\frac{t_base}{1.5} = t_{b)}$

He's going too fast, i'mma disconect rn

Exercise 1.6
	A computer coprocessor improves the **processing of floating point operations by a factor of 5**. The execution time of a certain program is **1 minute when the coprocessor is available** and it raises to **2.5 minutes without the coprocessor**. Compute the percentage of execution time devoted by the program to the execution of floating point operations when the coprocessor is not installed.

	I do have the global speedup

	$S_{freq}=5$
	$S_{g} = \frac{2.5}{1} = \frac{1}{\frac{F}{5} + (1 - F)}=2.5$
	$F=\frac{S_{g} \times S-S}{S_{g}\times -S_{g}} = 0.75 < 1$
	$F<1 \rightarrow S>S_{g}$


Related: [[AIC Concepts]]
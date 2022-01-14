## Misc

![Ataturk](./files/img/ataturk_calisirken.jpeg)

_Science is the most reliable guide in life._

Mustafa Kemal Ataturk


* Spin matrices for any spin value (Copy the following into a Mathematica notebook and evaluate it). Play only with the s value.

```Mathematica
s = 1;

dim = 2*s + 1;

Sp = ConstantArray[0, {dim, dim}];

Sm = ConstantArray[0, {dim, dim}];

Sz = ConstantArray[0, {dim, dim}];

i = 1;

For[mp = s, mp >= -s, mp--, j = 1;

For[m = s, m >= -s, m--, 

Sp[[i]][[j]] = \[HBar]*Sqrt[s*(s + 1) - m*(m + 1)]*

KroneckerDelta[mp, m + 1];

Sz[[i]][[j]] = \[HBar]*m*KroneckerDelta[mp, m];

Sm[[i]][[j]] = \[HBar]*Sqrt[s*(s + 1) - m*(m - 1)]*

KroneckerDelta[mp, m - 1];

j++;];

i++;];

Sx = (Sp + Sm)/2;

Sy = (Sp - Sm)/(2*I);

Print["\!\(\*SubscriptBox[\(S\), \(x\)]\) = ", \[HBar], 

Sx/\[HBar] // MatrixForm]

Print["\!\(\*SubscriptBox[\(S\), \(y\)]\) = ", \[HBar], 

Sy/\[HBar] // MatrixForm]

Print["\!\(\*SubscriptBox[\(S\), \(z\)]\) = ", \[HBar], 

Sz/\[HBar] // MatrixForm]
```

* Some of my all time favorite quotes:

(see top of the page.)

Whenever in doubt, expand in a power series. -Enrico Fermi

Whatever is not expressly forbidden is mandatory. -Richard P. Feynman

If you haven’t found something strange during the day, it hasn’t been much of a day. -John Wheeler

What I cannot create, I do not understand. -Richard P. Feynman

Practice does not make perfect. Only perfect practice makes perfect. -Vince Lombardi

Your priority should not be achieving in the system, but becoming independent in the system. -Luke Smith

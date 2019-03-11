Reactor Lab Report
Group 7
Ken Rivero-Rivera (klr227)
Catherine Johnson (caj92)

Introduction:


Objectives:


Procedures:


Results and Discussion:
1. Use multivariable nonlinear regression to obtain the best fit between the experimental data and the two models by minimizing the sum of the squared errors. Use epa.Solver_AD_Pe and epa.Solver_CMFR_N. These functions will minimize the error by varying the values of average residence time, (mass of tracer/reactor volume), and either the number of CMFR in series or the Peclet number.

2. Generate a plot showing the experimental data as points and the model results as thin lines for each of your experiments. Explain which model fits best and discuss those results based on your expectations.

3. Compare the trends in the estimated values of N and Pe across your set of experiments. How did your chosen reactor modifications effect dispersion?

4. Report the values of t⋆ at F = 0.1 for each of your experiments. Do they meet your expectations?

5. Evaluate whether there is any evidence of “dead volumes” or “short circuiting” in your reactor.

6.Make a recommendation for the design of a full scale chlorine contact tank. As part of your recommendation discuss the parameter you chose to vary as part of your experimentation and what the optimal value was determined to be.


Conclusions:


Suggestions:


Appendix:
```python
from aguaclara.core.units import unit_registry as u
import aguaclara.research.environmental_processes_analysis as epa
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from scipy import stats
import collections
import os
from pathlib import Path
from random import *


```

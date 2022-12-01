### **Second Computer Architecture Lab : Cache oprimization**

Authors: Konstantinidis Paschalis, Tzouvaras Evangelos

### **_Intro_**
The objective of this lab is to understand better the different cache parameters and how any change on the cache techology can affect on the execution time of different benchmarks. The tests became on the 401.bzip, 429.mcf, 456.hmmer, 458.sjeng mad 470.lbm benchmarks. On the first part the simulations are on different cpu clocks and how this affect on the cache misses. The second part includes simulations on different cache parameters and ends up to the optimized cache design for each benchmark. The third part analyzes a cost function based on the different cache parameters. 

### **_First Part: Run benchmarks_**

_Question 1_

The based parameters for the CPU are presented on the config file that is produced on the runtime of the gem5. Another way to find the parameters are on the Options.py file which is imported on the se.py file that we used as a parameter file. The parameters are presented below: 
  * d cache associativity = 2
  * d cache size = 65536 Bytes -> 64KB
  * i cache associativity = 2
  * i cache size = 32768 Bytes -> 32KB
  * L2 cache associativity = 8
  * L2 cache size = 2097152 Bytes -> 2MB

_Question 2_

The following table contains all the critical parameters that produced during the simulations for each benchmark:

| Benchmark       |Run time       | CPI       | Miss rate L1 d cache  | Miss rate L1 i cache  | Miss rate L2 cache  |
| --------------- |:-------------:|:---------:| ---------------------:| ---------------------:| -------------------:|
| 401.bzip        | 0.193424      |  3.868473 | 0.048025              | 0.000064              | 0.878407            |
| 429.mcf         | 0.064955      | 1.299095  | 0.002108              | 0.023612              | 0.055046            |
| 456.hmmer       | 0.000046      | 10.193071 | 0.086212              | 0.119533              | 0.935085            |
| 458.sjeng       | 0.513528      | 10.270554 | 0.121831              | 0.000020              | 0.999972            |
| 470.lbm         | 0.174671      | 3.493415  | 0.060972              | 0.000094              | 0.999944            |



_Question 3_

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

**Comments:**
On each benchmark the miss rate on each level of cache is something that depends on the program data, considering that we have same cache configuration on these simulations. 

_Question 3_

On this step we keep the cache parameters as the default and we change the CPU clock on the 1GHz and on the 3GHz. The default CPU clock that produced the data above was on the 2GHz. 

* The affect of the different CPU clock on the simulated seconds, is presented on the following graph: 

![image](https://user-images.githubusercontent.com/118462296/205145923-baa80f47-224f-4b82-9a15-797cbb38a5a7.png)

* The next graph shows the CPI numbers for each benchmark on the three different CPU clocks:

![image](https://user-images.githubusercontent.com/118462296/205146222-b261c6be-c66a-4300-8905-ab6ca0705a08.png)

* On the final gragh we can see the affect of the CPU clock on the miss rate of each cache level for the 429.mfc benchmark:

![image](https://user-images.githubusercontent.com/118462296/205147211-cf6ab42b-7668-4010-8392-664083f5594f.png)


**Comments:**
1) The only change by changing the CPU frequency is on the sim seconds. By increasing the CPU frequency the simulated seconds decreased because the CPU has the ability to execute the commands more quickly
2) The cache miss rates are the same (as expected) because there is no change on the cache parameters. So the time of execution is independent from the cache technology. The cache techology affects the host time because by impoving the memory, the CPU will take the data quickly to execute the instructions.
3) The CPI is not a valid parameter to compare the different benchmarks because we change the techology of the CPU. Sometimes maybe the CPI gets bigger but clock time gets even smaller. The CPI can be valid parameter to compare the cache techonoly in the inor CPI type and only if the CPU frequency is constant.


_Question 4_

We chose the 470.lbm benchmark to change the memory from DDR3_1600_x64 to DDR3_2133_x64. The simulation has as CPU frequency the default (2GHz). The comparison between the two memories is presented below: 

| Memory          |Run time       | CPI       | Miss rate L1 d cache  | Miss rate L1 i cache  | Miss rate L2 cache  |
| --------------- |:-------------:|:---------:| ---------------------:| ---------------------:| -------------------:|
| DDR3_1600_x64   | 0.174641      | 3.493415  | 0.060972              | 0.000094              | 0.999944          |
| DDR3_2133_x64   | 0.171530      | 3.430593  | 0.060972              | 0.000094              | 0.999944          |

**Comments:**
(1) The DDR3_2133_x64 has a clock on 2133MHz higher than the DDR3_1600_x64 which runs on 1600MHz. As a result, on any cache miss from the L2 cache, the data will come to the caches and finally to the CPU faster than previously. Due to the minor CPU model (one instruction each time), the faster memory decreases the CPI and finally the simulated time.
(2) The faster memory does not have any impact on the cache miss rate because the cache technology remained same. 

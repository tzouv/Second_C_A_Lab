## **Second Computer Architecture Lab : Cache oprimization**

Authors: Konstantinidis Paschalis, Tzouvaras Evangelos

### **_Intro_**
The objective of this lab is to understand better the different cache parameters and how any change on the cache techology can affect on the execution time of different benchmarks. The tests became on the 401.bzip, 429.mcf, 456.hmmer, 458.sjeng and 470.lbm benchmarks. On the first part the simulations are on different cpu clocks and how this affect on the cache misses. The second part includes simulations on different cache parameters and ends up to the optimized cache design for each benchmark. The third part analyzes a cost function based on the different cache parameters. 

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

* The affect of the different CPU clock on the **simulated seconds**, is presented on the following graph: 

![image](https://user-images.githubusercontent.com/118462296/205174906-d478125a-20d4-4641-af3a-eb58ac266708.png)

* The next graph shows the **CPI** numbers for each benchmark on the three different CPU clocks:

![image](https://user-images.githubusercontent.com/118462296/205174989-5247e2b1-228d-4416-a062-714b395dd065.png)

* On the final gragh we can see the affect of the CPU clock on the **miss rate** of each cache level for the 429.mfc benchmark:

![image](https://user-images.githubusercontent.com/118462296/205175093-c666f7ee-77b9-4324-9057-53cd1b1bf0e4.png)


**Comments:**
1) The only change by changing the CPU frequency is on the sim seconds. By increasing the CPU frequency the simulated seconds decreased because the CPU has the ability to execute the commands more quickly
2) The cache miss rates are the same (as expected) because there is no change on the cache parameters. So the time of execution is independent from the cache technology. The cache techology affects the host time because by impoving the memory, the CPU will take the data quickly to execute the instructions.
3) The CPI is not a valid parameter to compare the different benchmarks because we change the techology of the CPU. Sometimes maybe the CPI gets bigger but clock time gets even smaller. The CPI can be valid parameter to compare the cache techonoly in the inor CPI type and only if the CPU frequency is constant.


_Question 4_

We chose the 470.lbm benchmark to change the memory from DDR3_1600_x64 to DDR3_2133_x64. The simulation has as CPU frequency the default (2GHz). The comparison between the two memories is presented below: 

| Memory          |Run time       | CPI       | Miss rate L1 d cache  | Miss rate L1 i cache  | Miss rate L2 cache  |
| --------------- |:-------------:|:---------:| ---------------------:| ---------------------:| -------------------:|
| DDR3_1600_x64   | 0.174641      | 3.493415  | 0.060972              | 0.000094              | 0.999944            |
| DDR3_2133_x64   | 0.171530      | 3.430593  | 0.060972              | 0.000094              | 0.999944            |

**Comments:**
1. The DDR3_2133_x64 has a clock on 2133MHz higher than the DDR3_1600_x64 which runs on 1600MHz. As a result, on any cache miss from the L2 cache, the data will come to the caches and finally to the CPU faster than previously. Due to the minor CPU model (one instruction each time), the faster memory decreases the CPI and finally the simulated time.
2. The faster memory does not have any impact on the cache miss rate because the cache technology remained same. 


### **_Second Part: Cache optimization_**

To find the optimal cache design we chose to run multiple simulations and to change one parameter each time. Due to the minor CPU model the minimum CPI defines the more optimal cache design. 

The restriction of the L1 cache on 256KB and the two types of cache instruction and data, it limits us to use up to 128KB instruction and 128KB data cache. We chose as cache line up to 256 and the association for L1 up to 4 and for L2 up to 16.   


**401.bzip**

![image](https://user-images.githubusercontent.com/118462296/205172474-5a57f70d-8380-4367-8f6f-ad7221088bc9.png)

The better parameters for the cache on the 401.bzip benchmark are:
* Cache Line = 256
* L1 data size = 128KB
* L1 instruction size = 32KB
* L2 size = 4MB
* L1 association = 4
* L2 association = 4

By choosing the parameters above, the **CPI** will be **1.539881**


**429.mcf**

![image](https://user-images.githubusercontent.com/118462296/205178037-c2153272-f09f-4a77-97bd-6c0943d4d39d.png)

The better parameters for the cache on the 429.mcf benchmark are:
* Cache Line = 32
* L1 data size = 128KB
* L1 instruction size = 64KB
* L2 size = 4MB
* L1 association = 4
* L2 association = 4

By choosing the parameters above, the CPI and the miss rates will be :

**456.hmmer**

![image](https://user-images.githubusercontent.com/118462296/205178136-ebe9a5e2-a293-48f1-95ea-b543a5993d8f.png)



**458.sjeng**

![image](https://user-images.githubusercontent.com/118462296/205178221-d93cfd6b-0df5-4cb6-8101-7b76d0ed29d8.png)

**470.lbm**

![image](https://user-images.githubusercontent.com/118462296/205178275-8573eb51-9e84-4251-87e5-c30ce579506c.png)



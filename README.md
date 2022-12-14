## **Second Computer Architecture Lab : Cache optimization**

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

**Difference between clock domain and cpu clock domain**

System.clk_domain.clock is the same for all simulations because it is the whole system's clock including the peripherals , while cpu clock is only refer to the clock of cpu to it changes depending on the simulations.Thus cpu clock number in (ticks) cant be bigger than the system clock. If we add another cpu it will take the system.cpu_clk_domain.clock value.Scaling can't be perfect because all  actions in a cpu can't be done as fast as we want, so while we increaze the frequency of a cpu maybe some actions from the peripherals can't be done that fast(ex data transport). 

We could understand the difference between the clock domains and the simulation times on the following table:
| Benchmarks      |system.clk_domain.clock | system.cpu_clk_domain.clock | sim_seconds     |
| --------------- |:----------------------:|:---------------------------:| ---------------:|
| 401.bzip_1GHz   | 1000                   | 1000                        | 0.299770        | 
| 401.bzip_3GHz   | 1000                   | 333                         | 0.158327        |
| 401.bzip_2GHz   | 1000                   | 500                         | 0.193424        |
| --------------- | ---------------------- | --------------------------- | --------------- |
| 429.mcf_1GHz    | 1000                   | 1000                        | 0.127942        | 
| 429.mcf_3GHz    | 1000                   | 333                         | 0.043867        |
| 429.mcf_2GHz    | 1000                   | 500                         | 0.064955        |
| --------------- | ---------------------- | --------------------------- | --------------- |
| 456.hmmer_1GHz  | 1000                   | 1000                        | 0.119777        | 
| 456.hmmer_3GHz  | 1000                   | 333                         | 0.042047        |
| 456.hmmer_2GHz  | 1000                   | 500                         | 0.059396        |
| --------------- | ---------------------- | --------------------------- | --------------- |
| 458.sjeng_1GHz  | 1000                   | 1000                        | 0.704056        | 
| 458.sjeng_3GHz  | 1000                   | 333                         | 0.449821        |
| 458.sjeng_2GHz  | 1000                   | 500                         | 0.513528        |
| --------------- | ---------------------- | --------------------------- | --------------- |
| 470.lbm_1GHz    | 1000                   | 1000                        | 0.262327        | 
| 470.lbm_3GHz    | 1000                   | 333                         | 0.146433        |
| 470.lbm_2GHz    | 1000                   | 500                         | 0.174671        |

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

By choosing the parameters above, the **CPI** will be **1.545247**

_Comments_
1. The cache line has positive impact on the decrease of the CPI due to the locality of the program.
2. The increase of the L1 d size helps in the decrease of the CPI because according to the simulations the miss rate of L1 decreases.
3. Bigger L2 size decreases the CPI because decreases the L2 miss rate, so more useful data are on the L2 cache and the CPU does not need extra time to take these data from the RAM memory which is slower.
4. The association of the cache has no impact on the CPI possibly because the program has increased locality and the data that needs is on the same block of cache.

**429.mcf**

![image](https://user-images.githubusercontent.com/118462296/205178037-c2153272-f09f-4a77-97bd-6c0943d4d39d.png)

The better parameters for the cache on the 429.mcf benchmark are:
* Cache Line = 256 ( in 429 we see that alone cacheline 32 gives us better results than 256 but if we put the best of the other options and cacheline 32 we get worse cpi than cacheline 256)
* L1 data size = 128KB
* L1 instruction size = 64KB
* L2 size = 4MB
* L1 association = 4
* L2 association = 4

By choosing the parameters above, the **CPI** will be **1.090588**

_Comments_
1. The better cache line is the 32 based on simulations but compined with other values of cache the best CPI is for 256 cache line size.
2. The L1 associativity has the bigger impovement on the total CPI because the processor can find the data is smaller time now.
3. The L1 size bigger than 64KB has no impact on the CPI, so the best size is 64KB.
4. The L2 size decreases the time that the benchmark needs to run but the effective is not so big. So considering the best performance the L2 size may be 4MB but it is not cost effective.
5. The association of L2 has no effect on CPI and it is choosen on 4.


**456.hmmer**

![image](https://user-images.githubusercontent.com/118462296/205178136-ebe9a5e2-a293-48f1-95ea-b543a5993d8f.png)

The better parameters for the cache on the 456.hmmer benchmark are:
* Cache Line = 256
* L1 data size = 128KB
* L1 instruction size = 128KB
* L2 size = 1MB
* L1 association = 4
* L2 association = 4

By choosing the parameters above, the **CPI** will be **1.176204**

1. The cache line has the bigger impact on the reduction of the CPI due to the locality of the program.
2. The L1 memory increase follows to decrease the miss rate so it is selected the maximum L1 size (256KB totally).
3. The miss rate of L2 cache is relatively small,so an increament on the L2 size does not affect the simulated seconds.
4. The cache association does not affect the total run time and is selected the 4 way associative cache.

**458.sjeng**

![image](https://user-images.githubusercontent.com/118462296/205178221-d93cfd6b-0df5-4cb6-8101-7b76d0ed29d8.png)

The better parameters for the cache on the 458.sjeng benchmark are:
* Cache Line = 256
* L1 data size = 128KB
* L1 instruction size = 64KB
* L2 size = 4MB
* L1 association = 4
* L2 association = 16

By choosing the parameters above, the **CPI** will be **3.714696**

_Comments_
1. The cache line size improves dramatically the CPI (about 40% reduction), for the reason why the 458.sjeng benchmark has increased locality. So the data that comes on each cache line are used latter from the processor.
2. The other parameters also improves the total CPI, even though it is not visible in the diagram due to the cache-line. 

**470.lbm**

![image](https://user-images.githubusercontent.com/118462296/205178275-8573eb51-9e84-4251-87e5-c30ce579506c.png)

The better parameters for the cache on the 470.lbm benchmark are:
* Cache Line = 256
* L1 data size = 128KB
* L1 instruction size = 64KB
* L2 size = 4MB
* L1 association = 2
* L2 association = 16

By choosing the parameters above, the **CPI** will be **1.653662**

_Comments_
1. Any cache optimization on the 470.lbm benchmark has the smaller impact than the other benchmarks. We draw the conclusion that the data and the instructions on this program are independent. This conclusion perceived also for the miss rates of L1 data and L2 caches which is increased.
2. Due to independence of the data the more size of caches the better CPI so the size is the biggest possible.

### **_Third Part: Performance cost and optimization_**

**Cost Function**
Due to lack of available bibliography about the exact cost of each cache stage we only could extract information about how the cost of each cache will get affected by its size , its position in relation to the cpu , its associetivity and finally its line_size.**We build a scoreboard with points and each parameter gives different points based on its cost.**
We know that by doubling the size of an l1cache we need double hardware hence the cost doubles up.Also we could say that the closer a cache gets to a cpu the more expensive it gets .So an l1cache of x size would be equal(cost) of an l2cache of y size.
We abstractly defined that x would be 32kb and y 1MB.Considering the associetivity doubling its value requires more hardware but not a boudlbe up so we add a coefficient of 1.5 .As far as for the cache_line doubling the size of a fixed cache requires a few more hardware and its mostly based on a hardware rearrange so we put a coefficient of 1.2

**Cost Fucntion**
Cost = L1_i_size(KB)/32(KB) + L1_d_size(KB)/32(KB) + L2_size(MB)/1(MB) +  0.3333*((L1_assoc)^(log1.5/log2)) +  0.2222*((L2_assoc)^(log1.5/log2)) + 0.2009*((Cache_line)^(log1.2/log2))



**Scoreboard table**
| Parameter           |Value          |Points        |
| ------------------- |:-------------:|:------------:| 
| L1 i/d cache size   | 16KB          | 0.5 pts      | 
|                     | 32KB          | 1 pts        | 
|                     | 64KB          | 2 pts        | 
|                     | 128KB         | 4 pts        | 
| L2 cache size       | 1 MB          | 1 pts        | 
|                     | 2 MB          | 2 pts        | 
|                     | 4 MB          | 4 pts        | 
| L1 association      | 2 way         | 0.5 pts      |
|                     | 4 way         | 0.75 pts     |
| L2 association      | 4 way         | 0.5 pts      |
|                     | 8 way         | 0.75 pts     |
|                     | 16 way        | 1.125 pts    |
| Cache Line          | 32            | 0.5 pts      | 
|                     | 64            | 0.6 pts      | 
|                     | 128           | 0.72 pts     | 
|                     | 256           | 0.864 pts    | 

**Best cache costs**

Based on the best cache designs on the second part and based on the cost function above, the final costs are the following:

* 401/best/cost			0.864 + 0.750 + 4.0 + 1.0 + 0.500 + 4.0 = 11.114pts cpi 1.545247
* 429/best/cost			0.864 + 0.750 + 4.0 + 2.0 + 0.500 + 4.0 = 11.989pts cpi 1.090588
* 456/best/cost			0.864 + 1.125 + 4.0 + 4.0 + 0.500 + 1.0 = 11.114pts cpi 1.176204
* 458/best/cost			0.864 + 0.750 + 4.0 + 2.0 + 1.125 + 4.0 = 12.739pts cpi 3.714696
* 470/best/cost			0.864 + 0.500 + 4.0 + 2.0 + 1.125 + 4.0 = 12.489pts cpi 1.653662

**Optimized cache designs for each benchmark**

From the cost function above, we end up to the better value for money cache designs for each benckmark.

The optimized parameters for the cache on the _401.bzip_ benchmark are:
* Cache Line = 64
* L1 data size = 128KB
* L1 instruction size = 16KB
* L2 size = 4MB
* L1 association = 4
* L2 association = 4

By choosing the parameters above, the **CPI** will be **1.558243** and the **cost** will be 0.600 + 0.750 + 4.0 + 0.5 + 0.500 + 4.0 = **10.350pts** 
* Cost: -6.87% 
* CPI: +0.84%

The optimized parameters for the cache on the _429.mcf_ benchmark are:
* Cache Line = 256 
* L1 data size = 128KB
* L1 instruction size = 64KB
* L2 size = 2MB
* L1 association = 4
* L2 association = 4

By choosing the parameters above, the **CPI** will be **1.090681** and the **cost** will be 0.864 + 0.750 + 4.0 + 2.0 + 0.500 + 2.0 = **10.114pts**
* Cost: -15.6% 
* CPI: +0.008%

The optimized parameters for the cache on the _456.hmmer_ benchmark are:
* Cache Line = 256
* L1 data size = 128KB
* L1 instruction size = 64KB
* L2 size = 1MB
* L1 association = 4
* L2 association = 4

By choosing the parameters above, the **CPI** will be **1.176220** and the **cost** will be 0.864 + 0.750 + 4.0 + 2.0 + 0.500 + 1.0 =  **9.114pts**
* Cost: -17.9% 
* CPI: +0.001%

The optimized parameters for the cache on the _458.sjeng_ benchmark are:
* Cache Line = 256
* L1 data size = 128KB
* L1 instruction size = 64KB
* L2 size = 4MB
* L1 association = 2
* L2 association = 8

By choosing the parameters above, the **CPI** will be **3.714681** and the **cost** will be 0.864 + 0.500 + 4.0 + 2.0 + 0.750 + 4.0 = **12.114pts** 
* Cost: -4.9% 
* CPI: 0%

The optimized parameters for the cache on the _470.lbm_ benchmark are:
* Cache Line = 256
* L1 data size = 128KB
* L1 instruction size = 16KB
* L2 size = 4MB
* L1 association = 2
* L2 association = 8

By choosing the parameters above, the **CPI** will be **1.653726** and the **cost** will be 0.864 + 0.500 + 4.0 + 0.5 + 0.750 + 4.0 = **10.614pts**
* Cost: -15% 
* CPI: +0.003%


### **_Bibliography_**
1. https://arstechnica.com/gadgets/2002/07/caching/?fbclid=IwAR0GgS2mXvJHPvAFkm02UgN9vWUA7Dgo1vunOSqK7t4vFUNFzg2C5Xuia1w
2. https://semiengineering.com/the-high-but-often-unnecessary-cost-of-coherence/?fbclid=IwAR0GgS2mXvJHPvAFkm02UgN9vWUA7Dgo1vunOSqK7t4vFUNFzg2C5Xuia1w
3. Computer Architecture Hennessy John L. , Patterson David A. (6th Edition).

### **_Review_**
This Lab was a lot more hard and fun in relation to the First One. Since we had solve all the issues with running gem5 on vm this lab focused more on running simulations , getting results, comparing/understanding them and trying the best combinations to maximize performance while keeping the cost low.
This was a very good and realistic task because we know that cost is the most important thing that companies look. We also learn about bash scripting that made our lives easy and helped us run as fast as possible all the simulations and get the results with the easiest way possible.Concerning the structure of the assigment it was very good organized although in step1.question 3 was a little bit chaotic and not to well oriented.Another difficulty was in step 3 the bibliographic report for the explanation of our cost-fuction since there is not so much info about how the manufacturing cost of a cache gets affected. Maybe this happens because the manufacturers dont feel like giving out in public these information.

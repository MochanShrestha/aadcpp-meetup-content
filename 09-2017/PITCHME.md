## Topic : A Modern Build Pipeline with Conan.io
*Sponsored By Mechanical Simulation*  
![Carsim Logo](/assets/image/logo/carsim.jpg)
---
### Announcements
* Thanks to Mechanical Simulation! 
* Google announces abseil.io
	* Provides Supplements to Standard Library
	* Categories: `strings`, `numeric`, `memory`, `time`, `concurrency`, `memory`, `container`, `algorithm`
	* Examples:  
		* `absl::StrCat()`
		* `absl::StrJoin()`
		* `absl::StrSplit()`
---
### OSS Lib of the Month
* Actor Framework for C++ - http://actor-framework.org/
	* Parallel Computing - Distributed Systems Approach
	* Most Notable Actor Frameworks - Erlang, Akka
	* 28 Contributors - 57 Releases

---
### Questions
* Any Local Projects or Announcements?

---
### CONAN for C++ Devops

Devops - It's all about sharing code

---
### C++ as a Native Language

It's "Special"
![Giant Swiss](/09-2017/giant_swiss.jpg)

---
### C++ Status Quo

Copy sources then build yourself
![Draw Owl](/09-2017/draw_owl.png)

---
### C++ Build Systems

Easy to build once you learn the standard build systems
![Toolkit](/09-2017/toolkit.jpeg)

---
### C++ Ecosystems
![](/09-2017/boxer_vs_mma.png)

---
### C++ Ecosystems Extended
![](/09-2017/mma_disciplines.png)

---
### The Need for Package Management 

* Bjarne Stroustrup says we need it
  * (not a real reason)

* Practical Goals
  * Make it FAST and EASY to USE shared code
  * Minimize Need for Redundant Compilation
  
---
### What a C++ Package Manager Needs to Do
* Distribute shared code as precompiled binaries
* Automatic compile on-demand if binary not available
* Projects on same machine share binary cache
* Work for both Enterprise and OSS
* Work like other mature package managers

--- 
### Fundamental C++ Challenge #1
* Each OS + Compiler + Compiler Option = Unique Binary

--- 
### What a solution would look like
![](/09-2017/conan-binary-table.png)

--- 
### How do we get there? 
* OSS
![](/09-2017/travis-appveyor-github.png)

* Enterprise
	* VSTS, Jenkin, Bamboo, CircleCI, Github

--- 
### How do we start? 
* It starts with Packaging

![](/09-2017/travis-appveyor-github.png)

* Enterprise
	* VSTS, Jenkin, Bamboo, CircleCI, Github


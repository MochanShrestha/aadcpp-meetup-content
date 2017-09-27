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
* Actor Framework for C++
	* http://actor-framework.org/
	* Parallel Computing - Distributed Computing
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

Easy to build once you learn the build system(s)
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
  
* Real Goals
  * Make it FAST and EASY to USE shared code
  * Minimize Need for Redundant Compilation
  
---
### General Requirements 
* Cross Platform, IDE and toolset agnostic
* Distribute shared code as precompiled binaries
* Automatically compile if binary not available
* Projects on same machine share binary cache
* Work for both Enterprise and OSS
* Work like other mature package managers

--- 
### Fundamental C++ Challenge #1
* OS + Arch + Compiler + Options = Unique Binary
** Header-Only Libraries Much Easier **
--- 
### It's Been Solved!
![](/09-2017/conan-binary-table.png)

--- 
### Conan.io Provides
* The logic for creating and storing multiple binaries
* Cloud-hosted central public repository for OSS
* Cloud-hosted private repositories for Enterprise
* On-Premise server platform for Enterprise
* Local client application for packaging and caching

--- 
### Wait, how to build so many the Binaries? 
* OSS
![](/09-2017/travis-appveyor-github.png)

* Enterprise
	* VSTS, Jenkin, Bamboo, CircleCI, Github

--- 
### Lets Get Started !
* Prerequisites
	* Visual Studio 2017 15.3 with Python Support
	* Github

### Agenda
* Write Some Code
* Package The Code
* Share The Code Locally
* Publish the Code Online
* Reuse the Code on Different Machine



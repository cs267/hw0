---
title: Spring 2017 UCB CS267 HW0
nocite: |
  @James:2015jo, @Gonzalez:uh, @James:2015hu, @Anonymous:vy
...

Note: you can read this document in [HTML](https://cs267.github.io/hw0/) or [PDF](https://cs267.github.io/hw0/index.pdf). And the source is available at [GitHub](https://github.com/cs267/hw0).

# Biography

- name: Kolen Cheung

- interest: I am a graduate student in Physics, and am especially interested in General Relativity. e.g. Gravitational lensing, CMB, Blackholes, etc.

- what I'd like to get out of the class: how to apply parallel programming in simulation/data analysis in Physics that possibly involves non-linear differential equations (like General Relativity). And in general I want to gain more solid programming skills.

- background: I learnt C a decade ago without using it since then. I know some Python, bash, make, etc. I am also interested in Haskell, but isn't too familiar with it. Programming and CS in general is always a secret passion of mine. I once considered minored in CS in undergraduate but my dual degrees in Mathematics and Physics and a semester of exchange program (to here in UCB) took away all my available time. Knowing that there is a Designated Emphasis ("graduate minor") in Computational Science and Engineering, where CS267 is mandatory, I want to give it a try to fulfill my dream. But because of my weak background in CS, I am not sure I can follow through.

# Examining the Parallel Computing Behind "Interstellar"

The followings are excerpts from different references:

- Method:
	- based on tracing huge numbers of light rays through curved spacetime. [@James:2015jo]
- Programming:
	- DNGR was written in C++ as a command-line application. It takes as input the camera’s position, velocity, and field of view, as well as the black hole’s location, mass and spin, plus details of any accretion disk, star maps and nebulae. [@James:2015jo]
	- It has 40,000 lines of C++ code and runs across Double Negative’s Linux-based render-farm. [@James:2015jo]
	- uses the OpenVDB library to store and navigate volumetric data and Autodesk’s Maya to design the motion of the camera. [@James:2015jo]
- System:
	- typically in research in Astrophysics, massively parallel GPU-based code like GRay are used for ray-tracing, which provide very fast throughput (often measured in integration steps per second) [@James:2015jo]
	- For work in Interstellar, by contrast, a primary goal is smoothness of the images, so flickering is minimized when objects move rapidly across an IMAX screen. So the bulk of the computational work is done on a large compute cluster (the Double Negative render-farm) that does not employ GPUs. [@James:2015jo]
	- London render-farm comprises 1633 Dell-M620 blade servers; each blade has two 10-core E5-2680 Intel Xeon CPUs with 156GB RAM. Several hundred of these were typically being used by the DNGR code. [@James:2015jo]
- Parallelism
	- Each pixel can be calculated independently, so we run the calculations in parallel over multiple CPU cores and over multiple computers on our render-farm. [@James:2015jo]
- Data
	- A typical IMAX image has 23 million pixels, and for Interstellar many thousand images are generated. [@James:2015jo]
	- Depending on the degree of gravitational lensing in an image, it typically takes from 30 minutes to several hours running on 10 CPU cores to create a single IMAX image. [@James:2015jo]
	- 800 terabytes [@Anonymous:vy]
	- According to our experts, at the end of the day those studios will net out $47,161,000. That is a good return — cash on cash return is 1.09 — but as you will see as we go along, there were 19 films that posted better returns. [@Fleming:QEW_4D-g]

To conclude, because the goal of Interstellar is for visual effects which emphasize to be visually pleasing rather than absolute throughout, a different technique than a typical astrophysical research is employed. And since the ray tracing algorithm allows each pixel to be calculated independently, the difficulty of parallel computing is not high. So a cluster is employed, involving usually hundreds of 20 CPU cores machines at a time. The total computer time used is massive, and data generated is enormous. In the end they did a good job and generally received praises from both the scientific and cinematic community. It achieved the goal of never-seen-before renderings of super massive, rapidly rotating blackholes and wormholes to the mass public, while being as scientifically accurate as possible (albeit some scientific accuracy is sacrificed — color changed due to relativistic effect is removed for aesthetic reasons). Their revenues also reflect their success.

Regarding physical results, we wish anyone will have such a chance to compare it. Before then this is our best chance to see such beauties up close.

And a noteworthy takeaway is, if there is an algorithm (in this case, per-pixel ray-tracing) so that each calculation is independent of each other, this drastically reduces any difficulties in parallel computing.

# References

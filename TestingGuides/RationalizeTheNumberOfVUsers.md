---
sort: 2
title: Rationalize The Number Of VUsers
---

# How To Rationalize The Number Of Virtual Users On Each Worker

First the virtual users of each type will be evenly distributed across the Worker nodes.

The difference in the number of virtual users of each type on each Worker node will not be greater than one.

<style>
    img[alt=pic00000004] { 
        display: block;
        width: 680px; 
    }
</style>
![pic00000004](/assets/images/pic00000004.png)

This has the advantage that the test cases executed and the system resources used by each Worker will be relatively similar, with low variance between Workers.

Each Worker is a Pod of Kubernetes, and all virtual users on a Worker will share that Worker's CPU and Memory resources in a threaded fashion.

The total number of virtual users must be an integer multiple of the number of Workers, and for the number of virtual users, the more Workers will consume more system resources, 
but also the more stress will be placed on the system under test.

# SEDA (Staged Event-Driven Architecture)

There's an old axiom that a chain is only as strong as its' weakest link.

Likewise a series of sequential processes can only proceed at the speed of the slowest process.

SEDA is a strategy for ___decoupling___ processes to allow for bursty or irregular traffic patterns.

## Wikipedia

The wikipedia article is worth a read:

    http://en.wikipedia.org/wiki/Staged_event-driven_architecture

## Characteristics

The following quotes are from the [original article](seda-sosp01.pdf).

#### Well-Conditioned

	Intuitively, a service is well-conditioned if it behaves like a sim-
	ple pipeline, where the depth of the pipeline is determined by the path
	through the network and the processing stages within the service it-
	self. As the offered load increases, the delivered throughput increases
	proportionally until the pipeline is full and the throughput saturates; ad-
	ditional load should not degrade throughput. Similarly, the response
	time exhibited by the service is roughly constant at light load, because
	it is dominated by the depth of the pipeline. As load approaches satura-
	tion, the queueing delay dominates. In the closed-loop scenario typical
	of many services, where each client waits for a response before deliv-
	ering the next request, response time should increase linearly with the
	number of clients.

[Both ___SOA___ and [microservices](http://github.com/mramshaw/Microservices) echo this concept.]

#### Graceful Degradation

	The key property of a well-conditioned service is graceful degra-
	dation: as offered load exceeds capacity, the service maintains high
	throughput with a linear response-time penalty that impacts all clients
	equally, or at least predictably according to some service-specific pol-
	icy. Note that this is not the typical Web experience; rather, as load
	increases, throughput decreases and response time increases dramati-
	cally, creating the impression that the service has crashed.

[I have always referred to this as ___graceful failure___ - which is perhaps a pessimistic way of looking at things.]

An important concept here is the idea of ___fairness___: the previous
state of affairs was ___first-come, first-served___ (everyone who got in
a request before the servers became overloaded got a response; all subsequent
requests were rejected).

[This is an example of [load-shedding](http://en.wikipedia.org/wiki/Load_Shedding);
 other possible strategies are [Rate limiting](http://en.wikipedia.org/wiki/Rate_limiting)
 and [Traffic shaping](http://en.wikipedia.org/wiki/Traffic_shaping). Rate limiting
 only deals with the issue of greedy consumers (such as robots) but is a simpler
 approach than traffic shaping (which becomes quite complicated very quickly).]

## Terminology

* [Load-Shedding](http://en.wikipedia.org/wiki/Load_Shedding)

* [Rate limiting](http://en.wikipedia.org/wiki/Rate_limiting)

* [TLB (Translation Lookaside Buffer)](http://en.wikipedia.org/wiki/Translation_lookaside_buffer)

* [Traffic shaping](http://en.wikipedia.org/wiki/Traffic_shaping)

## Papers

[SEDA: An Architecture for Well-Conditioned, Scalable Internet Services](seda-sosp01.pdf)

Matt Welsh, David Culler, and Eric Brewer

Available at:

    http://github.com/mdwelsh/mdwelsh.github.io/blob/master/papers/seda-sosp01.pdf

__Matt Welsh__ is a co-author of the excellent [Running Linux](http://shop.oreilly.com/product/9780596007607.do).

__Eric Brewer__ is of course known for the [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem).

[Virtualization Considered Harmful: OS Design Directions for Well-Conditioned Services](seda-hotos01.pdf)

Matt Welsh and David Culler

Available at:

    http://github.com/mdwelsh/mdwelsh.github.io/blob/master/papers/seda-hotos01.pdf

This [presentation](seda.pdf) I found by doing an internet search for "staged event-driven architecture". It can be found at:

    http://pages.cs.wisc.edu/~remzi/Classes/739/Fall2016/Papers/seda.pdf

[The graphs are taken from the original SEDA paper, where they are presented in colour.]

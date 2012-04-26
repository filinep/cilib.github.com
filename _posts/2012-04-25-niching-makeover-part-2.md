---
layout: post
title: "Niching Makeover: part 2"
description: ""
category: 
tags: []
---
{% include JB/setup %}

This post will describe the structures and functions available for niching algorithms.

### Niching Components

The main parts to a niching algorithm are:

- a skeleton algorithm which holds different strategies for the niching operations
- niching swarms which consists of a main swarm and a list of subswarms
- niching functions which are operations applied to the niching swarms
- niching strategies / helper functions which the niching functions use

### Niching Swarms

The niching package was developed for algorithms that contain a main swarm which
then gets split into subswarms to refine solutions separately. Each subswarm is
considered to be a niche. As a result the niching functions operate on 
`NichingSwarms`. `NichingSwarms` is a tuple consisting of a `PopulationBasedAlgorithm` 
and a `List<PopoulationBasedAlgorithm>` defined as

    class NichingSwarms extends P2<PopulationBasedAlgorithm, List<PopulationBasedAlgorithm>>

Recall from the previous post that to access the first element, the main swarm, 
of a tuple the `_1()` method is used. Similarly `_2()` accesses the subswarms.
Additionally `getMainSwarm()` and `getSubswarms()` were implemented to improve
readability in some of the functions.

Three functions were implemented to apply certain functions to only the main swarm,
each of the subswarms or the first subswarm. These static functions called

    NichingSwarms.onMainSwarm(F<PopulationBasedAlgorithm, PopulationBasedAlgorithm> f);
    NichingSwarms.onSubswarms(F<PopulationBasedAlgorithm, PopulationBasedAlgorithm> f);
    NichingSwarms.onFirstSubSwarm(F<PopulationBasedAlgorithm, PopulationBasedAlgorithm> f);

Those functions will apply the given function, f, to the respective swarms and return
the updated NichingSwarms.

There are also convenience methods for creating 


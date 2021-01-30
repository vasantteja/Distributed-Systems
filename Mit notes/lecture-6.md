# Fault Tolerance

## Problem Statement

This tries to get the state machine replication correct.

## Pattern in Fault Tolerant Systems

1. In map reduce it replicates computation and it's controlled by single master.

2. In GFS data is replicated but it depends on single master to choose who the primary is for every piece of data.

3. In vmware ft it replicates computation write on a primary virtual machine and backup virtual machine. Inorder to decide/figure what to do
when a single one fails it relies on a single test and set server to choose to ensure that exactly one of the primary/backup takes over when there's a kind of failure.

==> In the above three cases we see that only one single system made the choice of who the primary is when there is a failure.

==> A single entity need not consult with any other entities and there will be consensus easily.

## Bad things when there is single entity

It's a single point of failuire when this breaksup.

## Split Brain

     |
c1---|
     |----s1
c2---|
     |----s2
     |

==> Imagine a scenario, where client can talk to both the servers.
==> If C1 talks to S1 and cannot talk to S2.
==> Similarly C2 talks to S2 and cannot talk to S1.
==> If you wait till both respond you're not fault tolerant and you just speak with onbe and neglect other then you're not correct.
==> In the above scenario, the client1 speaks only with server1 and server2 is completely oblivious to it and client2 speaks only wioth server2 and not server1.
==> This way, there is a possibility one single resource can be manipulated by both clients, but the servers don't know about it.
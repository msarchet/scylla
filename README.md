# Scylla

> SKYLLA (Scylla) was a sea-monster who haunted the rocks of a narrow strait opposite the whirlpool of Kharybdis (Charybdis). Ships who sailed too close to her rocks would lose six men to her ravenous, darting heads.
[source](https://www.theoi.com/Pontios/Skylla.html)

## Purpose

It's nice to be able to remap around signals from one application to another

This also allows the user to redirect

Watches a file in the same folder called `tempest`

tempest can look as follows

```
# listen on UDP and assign to 1
;49161 > 1

# listen on UDP and assign to 2
;49162 > 2

# listen on MIDI Device 1 and assign to A
:1 > A

# make an OSC listener on path and assign that to B
=/path/whatever.49163 > B

# set C to send messages to UDP 49163
;49163 < C
# pipe the message on 1 (converted to a string) 
# to a UDP defined by C
1 > C

# this can also be written as 
1 > ;49163

# you can assign one input to multiple outputs

# set D to send messages to UDP 49162
;49162 < D

# also send 1 back to D
1 > D

# this can also be done with midi devices
# make a midi out device and set it as MIDI device 2
:2 < E

# make F send OSC messages on port to an address
=/path/to.49164 < F
```

Listening ports aren't recreated on each parse, they only get destroyed at the end of the parse if they are not found

## Roadmap

- implement basic operators
    - ;
    - >
    - <
    - =
    - :

- implement delay operator
    - delay(time) waits time to pipe the message
- implement conversion operator
    convert(msg => /* do converter things */) allows you to write js to convert the message
- implement switching operator
    switch(A, ..., n) switch between inputs or ouputs
- implement probability operator
    probability({A , .2}, {B, .3}) weighted picking on each message pipe
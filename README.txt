output unit:
We build a binary to unary decoder, and let the marbles roll into an output stack. 
This is the same binary to unary decode we need for loading jumps into the pc stack.

program rom is 10 bits wide. 6 bits for an embeded data word, 4 bits for an opcode. TODO: Is 16 opcodes sufficient?






Program counter:
A stack of marbles. It encodes in unary. Normal operations add one marble to the pc stack, so that the next command
gets addressed. 
"Relative forward jumps" can optionally put n extra marbles in the pc stack.
"Reset PC" drains all marbles from the pc stack.
A backwards consists of a drain, followed by putting in n marbles.

The command decoder senses the height of the pc stack and selects a microcode punch card (or a microcode conveyor belt) based on the binary code found there.


-----


All microcodes reset program counter increment to 1.
All microcodes reset the timer step counter to 0. 
All microcodes program their done flag to fire after a maximum T=n steps.
When a microcode done flag was raised, subsequent time steps move the program counter until all increments are done. 
the program counter advances one memory register, where the next microcode is found.

microcode operations:
X X X 0 0 1	Multibit Add in Register X. Stops after T=6



Multiplier
----

Modeeled after the Leibniz Box with Holes idea.
It needs 3 things.
1) A set of three registers A, B, X of 6 bits each. X needs to have safety rails, to dump bits above 6 and set a mechanical 
   overflow flag, if so.
2) a register copy mechanism: A into X with left shift (0-5). 
3) a register bit walk, that performs "an operation" if the relevant bit of Register B is set.

A moveable platform consists of 6 Gates, that can be switched on or off. The gates sit between a 6 bit latch gate on a power rail and register X.
In T=0, the bits of register A are transfered into open/closed gates of the platform.
In T=1, the latch gate opens for one ball. Where platform gates are open, a marble rolls from the power rail into 
register X
In T=2, the platform moves one bit position to the side.
In T=3,4 until T=11,12 the same actions are repeated. 
(the platform should be built as a conveyor belt, that loops back to the beginning, if possible. Otherwise, we need an extra step 13, that bring the platform back)



----


ITA or Baudot-Murray Punch tapes use 5 bits. With a Letter shift and Figure shift code to extend to effectively 64 code points.
https://en.wikipedia.org/wiki/Baudot_code

Baudot code does not have the digits sequentially (as ASCII or ECMA-1 would have them). We need a complex decoder and encoder for numbers.
(Or we design our own encoding...???...) Compatibility with vintage punch-tape readers and writers would be a good thing, oto. ?

ECMA-1 or DEC-SIXBIT have a much nicer encoding....

We use 6bit internally, to address a register bank of 64 registers.
For educational value and real live relevance we should have 8 bits per word.


Speed classifications
---------------------
Modern computers are speed of light computers. Electrons move accross the wires very fast.
Ancient computers are speed of mechanics computers. Levers, rods and gears can be driven slow or fast, by always several magnitudes slower than the speed of light.
Now, there is also speed of marble computers. At any given slope, the gravity of the earth applies a 
constant drving force on a marble. The speed a marble reaches, can be slowed down by obstacles or other 
elements, but we cannot speed up gravity. A rolling marble has its inherent speed. It cannot "be rolled faster" by cranking the machine faster. This only brings the marbles earlier to the top positions, but letting them roll
just takes its time.

We intentionally build a slow computer.
 - Being mechanical, it cannot win any speed competitions anyway.
 - Whenever there is a decision speed versus simplicity, we go for simplicity. (Minimize part count)
 - Whenever there is a decision speed versus transparency, we go for transparency. (Visible operations)
 - Clock by hand-crank. Primary use is for education. 
 - artificial slowification, e.g. by "you can always add another level of indirection" is to be avoided.
 - Slow down by slowing the clock is for debugging or manual control only.
   The nominal speed (slowness) is measured with the fastest possible clock that still works reliably.

Pushing rods like on the Z1 can be moved quite fast. The Z1 also uses thin
metal sheets to achieve tight packing.  All this makes it not easy for a human
to follow the operations. Especially the flow of information is invisible.
Looking at one long part that is coupled with other parts, it is often not
apparent, what part drives, and what part is driven. Both ends of a long part
move at the same time. The Zuse Z1 does not aim at visualizing its operation.
We do. Marbles make the flow of information visible, as humans can follow their
motion from start to end.



SM3C-Elements
=============

Marbles
-------
Marbles represent electricity and data. When on the power rails and reservoirs, a marble can be though of as an electron. It moves from higher loctions to lower locations, entering logic elements, busses and storage elements. It finally arrives in the dump, to be recycled in the power supply.
Steel, plastic and glass are available.
We need many. Guesstimate:  full RAM module of 64x6 = 384. Having twice or three times as much should be sufficient for a start.

The size and weight of the marbles defines the size of the entire machine. The weight influences the choice of mechanisms.
One of the largest component of the machine is probably the memory.64 cells with 20mm per cell require a length of 1.24m.

The machine building blocks should not exceed 55cm x 36cm, so that they fit in standard Eurobox containers.
The memory unity needs to be split into 3x 55cm or 4x 36cm in this case.


https://www.amazon.de/Warenfux24-RPN-Glasmurmeln-Glaskugeln-Dekoration/dp/B079W3FMHV/
800 glass marbles cost ca. 20 EUR, ca 5gr each.
The smallest acceptable size is 15mm, the largest acceptable size is 17mm.

https://www.amazon.de/Umarex-Stahlrundkugeln-5000-St%C3%BCck-BB%60s/dp/B004PH88F8/
5000 steel balls 4.5mm diam cost ca 17 EUR.
Not stainless.

https://www.amazon.de/Ultrasport-Unisex-Erwachsene-Softair-Munition-0-20/dp/B019H12VPE/
4000 PLA balls 6mm diam, cost ca 13 EUR. 0.25gr (!) each.
Lightweighted. Detecting a ball cannot be done by weight. Only by poke.

https://www.amazon.de/Stahlrundkugeln-Edelstahl-St%C3%BCck-Steinschleuder-Zwille/dp/B00DV5VU3W/
500 stainless(?) steel balls, 8mm diam, cost 11 EUR + 4.90 EUR

https://www.amazon.de/dp/B07MFWRSTR/
1000 nickel-steel balls, 8mm diam, cost 21 EUR, 2.0gr each.

https://www.amazon.de/-/en/Original-Shoot-Club-Slingshot-Ammunition-Catapult/dp/B08VF8TGJZ/
	1000 steel balls, 8mm, 18 EUR + 5.89 EUR

https://www.amazon.de/Sector-71-Stahlkugeln-Schleudern-Verschiedene/dp/B01I4ZDUP4/
200 carbon-steel, 10mm diam, cost 12 EUR, 4gr each

https://www.amazon.de/Muzzler-Premium-Stahlkugeln-Schleudern-Katapult/dp/B01N06GKMR
400 carbon-steel, 10mm diam, cost 18 EUR, 4gr each

https://www.amazon.de/Vancool-Professional-Kunststoff-Slingshots-Plastikperlen/dp/B073XH9R3D
500 plastic, 10mm diam, cost 14 EUR, ca 0.6gr each

https://www.amazon.de/g8ds-Marken-Schleudermunition-Stahlkugeln-Schleuder-Munition/dp/B07GS91Y3B
500 steel balls, 12mm, cost 25 EUR

https://www.amazon.de/12-mm-Kohlenstoffstahlkugeln-umweltfreundlich-Maschinenbau-Heimwerker-Kugellager/dp/B0DQCKZQLS
200 steel balls, 12mm, 1.4kg, cost 12 EUR

https://www.amazon.de/sourcing-map-Lagerkugeln-Chromstahl-Pr%C3%A4zisionskugeln/dp/B0822LMMM6
50 steel balls, 12mm, Chromstahl G10, 17.30 EUR

https://www.ebay.de/itm/335435976697?var=544846175789
100 steel balls, 12mm, Edelstahl rostfrei G100, 20 EUR

############################################################################
https://www.ebay.de/itm/396583747630
127 stück, 0.95 kg, 12mm, Chromstahl C15, 9 EUR + 5 EUR


https://www.amazon.de/g8ds-Marken-Schleudermunition-Stahlkugeln-Schleuder-Munition/dp/B07GSG2P8Y
200 steel balls, 16mm, cost 11 EUR.

https://www.amazon.de/g8ds-Marken-Schleudermunition-Stahlkugeln-Schleuder-Munition/dp/B07GSBQWFG
500 steel balls, 16mm, cost 27 EUR.


16mm is affordable. Steel or glass. There is no need for plastic or clay.

12mm steel is probably better: 500 balls 12mm weigh ca 3.5 kg,




Power supply
------------
An elevator mechanisms that shovels marbles from the dump to the start of the power rail tree. The main crank drives the elevator. Additional elevators should be easy to add. During start-up the elevators have to shovel up enough marbles to fill all reservoirs to at least their low-water marks. (Elevators can pause, when all rails dump marbles.)

Elevators have a define entry diameter of 17mm. Anything larger is dropped into the drain.
Elevators have a defined exit diameter of 15mm. Anything smaller than that is dropped into drain.


Power rails
-----------
A "never ending" supply of new marbles. It is mechanically higher than all other element so that gravity plays the role of 
voltage. Each logic element has a reservoir (think of "capacitor") of marbles connected to the power rails. Each marble rolling on a power rail will enter the first non-full reservoir. If all reservoirs are full, excessive marbles are dumped.
Each reservoir has a low water flag. If less marbles are in the reservoir, than possibly needed in one clock cycle, a flag is shown.

The power rails start with a binary distribution tree to distribute marbles into a set of "parallel" power rails. This allow easier 2 dimensional distribution. The reservoirs of logic elements with high consumption can be connected to two or more power rails.



Dump
----
A "ground plane" under the machine that collects excess marbles. From the lowest point of the dump, marbles are fed to the power supply or to the drain bucket (if one is placed under the drain next to the lowest point).
A large piece of cloth serves as a safety net. It also covers the marble drain, unless pushed back by a bucket.
No marble should ever drop to the floor.
Near the high end, the dump has a marble loading ramp, where humans can dump buckets of new marbles. Any spilled marbles should go to 
the safety net.


Glossary
--------

coupled: Mechanically coupled by levers, rods or other gear. No marbles are involved. This has immediate effect.

connected: Marble rails are connected by switches. Marbles need to pass through to cause an effect further down.

Marbles: We rather use high precision steel balls instead of glass marbles. They don't break and run smoother.

derail: a mechanical obstacle blocks a rail (one bit of a bus) and causes any oncoming marbles to be dumped, or stored elsewhere.



SM3C-Clock
==========
Clock distribution is a mecanical coupled grid, that is moved in small circles,
so that in every position of the grid the same circular movement can be
obtained. We subdivide clock cycles in four phases: I) down, II) right, III) up, IV) left.
(Z1 calls them north, south, east, and west)

The main hand crank takes two, four, or eight revolutions to complete one clock
cycle, depending on the needs of the power supply.  Side effect of the speed
reduction: People usually want to crank as fast as they can. The reduction gear
helps to keep the clock reasonably slow. The name already says "slow motion", right?

For manual cranking, a reduction of four is best. This allows to listen for marble movement duing rotation.
The time elevator always deliver one timing marble per clock phase.

Rule: You are only allowed to crank the next revolution, after you heared the timing gong.
The timing marble runs through a certain length of rail, to delay it a bit more than the longest possible operation.
The timing marble finally dumps onto a bell, to sound the gong. (There may be noises after the gong, coming from the dump)

For electric cranking, a watchdog timer starts, when the cranking starts.
 The watchdog is reset, and a short delay is started when the timing marble hits the gong.
 After the short delay is up, the motor cranks the next revolution.
 If the watchdog expires, the motor starts making beep noises. As soon as the gong is hit, normal operation resumes.



SM3C-Output
===========
Output devices can be very slow. E.g. Unary encoding, and using weigths.
Very nice would be a 3x5 Font represented by marbles.


SM3C-RAM
========

Memory is going to be mechanically large. We build it in banks, so that it is extendible.
Each bank has 16 words, its own 4 bit address decoder, and its own data bus.

To form a memory unit out of multiple banks, we arrange identical bank ontop of each other.
The memory data bus starts with a bank decoder. A two or 3 bit decoder sufficiently demontrates the idea.
Only one bank (or none) is connected to the data bus at any given time.
Bank position 0 remains empty, so that our address space has a "zero page".


Address decoder
---------------
The address register is split into 4 lower bits and 2 (or 3) upper bits.
Each bank has its address decoder switches coupled to the 4 lower bits.
The upper bits of the address register are coupled to two bank selector units:
One address selector and one data bus selector. 

Each clock cycle at I), the addess selector receives one marble from the
power grid and sends it to one of the connected bank address decoders.

Each clock cycle at III), the data bus selector receives a full word of 6 marbles from the power grid 
and sends it to one of the connected banks.

Both, address selector and data bus selector should be built vertically, to gain speed.

If no memory operation is needed, bank 0 is selected and the marbles from both selectors are 
are dumped into the sink. 


Read
----

By the start of II), one of the banks has a selected cell. A marble has arrived through the address decoder, and couples the cell to the copy mechanism.
At II), the copy mechanism probes the bits of the cell and derails the data bus, where an empty bit is found.
At III) marbles run down the data bus, and at beginning of IV) the data output register has a copy of the selected cell.
During IV) the cell selecting marble is dumped and the copy mechanism resets.


Erase
-----
The cell selecting marble couples the dumper mechanism. During II), the marbles are dumped from the cell.
Override switches derail the data bus selector.
At the beginning of III) the cell dumper mechanism is reset.
During III) data bus marbles are dumped in the selector.
During IV) the cell selecting marble is dumped and the mechanisms resets.
No marbles arrive at the output register.

Erase is actually the same as a write with an empty data input register.
That is why the cell dumper needs to reset early :-)


Write
-----
The cell selecting marble couples the dumper mechanism. During II), the marbles are dumped from the cell.
The override switches to derails the data bus selector are coupled to a data input register.
The override mechanism probes the bits of the input register and derails the bus where an empty bit is fouund.
At the beginning of III) the cell dumper mechanism is reset.
During III) data bus marbles transport the bit pattern of the input register. The data bus is derailed at the 
selected cell so that marbles from the bus end in the memory cell.
During IV) the cell selecting marble is dumped and the mechanisms resets.
No marbles arrive at the output register.



Adder
-----

Register B is added to Register A inplace.
Easy case: Register B contains the value 1:
 The incoming marble triggers the probe mechanism of the bit position where it comes in.
 If the bit is 0, the new marble is placed in that position. Done.
 If the bit is 1, the old marble is dumped, and the new marble is transfered left, to the next bit position.
	Timing problem. Multiple marbles are incoming roughly simulaneously. If
	a marble gets trandfered left, then one rail has two marbles.  There is
	no defined distance between them, while in motion. The mechanics cannot safely
	distingusih two marbles from one.
 Aternative idea: 
	Serial (ripple carry) adder. The second marble bumps into the first,
	and thus stops in the probe position. A mechanical probe comb detects marbles
	in these position and initiate transfers and dumps. All dumps are executed in
	parallel, but the transfers are split into multiple steps. 
	1) "carry" marble while the probe moves downwards,
	2) let the marble roll into the rail to the left when the probe moves upwards and thus gives way.
	Repeat the probe movement n-2 times on an n-bit adder, to allow a
	controlled worst case transfer from bit position 0 to n-1.
  Repeat.
General case:
 For an 8-bit word, we need 8 clock cycles. In each clock cycle:
   If there is no marble coming in I) at a certain bit positon, the probe mechanism reads a 0 during II), 
   and prepares to insert the new marble during III) nothing happens, as there is no marble.
   If there is a marble coming in during I), the probe mechanism does an actual probe during II) 
     If that was a 0, the new marble is inserted at the current bit position III), probe mechanism resets during IV).
     Else, if that was a 1, the old marble is lifted from its position and the new marble is transfered one position left during III).  
       The lifted marble is dumped and the probe mechanism resets during IV).
  Marbles overflowing to the left of the highest bit are dumped.
   
 

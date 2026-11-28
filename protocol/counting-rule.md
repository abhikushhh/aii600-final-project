# Counting rule (locked)

This file documents the counting rule used to define what qualifies as a parked civilian passenger car in a sampled still. The released CSV also contains preliminary AI-assisted count fields; those fields are not human measurements and are not used in the Part 2 model or held-out test.

Count a vehicle only when it is:
- a civilian passenger car, SUV/crossover, minivan, wagon/hatchback, or light-duty pickup;
- parked in a stall, curb space, driveway, or storage position;
- sufficiently visible to identify as a qualifying passenger vehicle.

Exclude:
- moving traffic or vehicles in travel lanes;
- motorcycles, buses, heavy/commercial trucks, trailers, RVs, emergency/military vehicles;
- reflections, signs, screens, or duplicate mirrored views;
- ambiguous slivers or partial objects that cannot be confidently identified.

For partial visibility, count only when enough of the vehicle body is visible to identify it as a distinct qualifying passenger vehicle. When uncertain, exclude it.

Do not silently change this rule mid-dataset.

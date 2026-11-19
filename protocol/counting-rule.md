# Counting rule (locked)

> **Note:** Car counts were not collected for this dataset. `data/clip-log.csv` has no count columns. This rule is kept as the written definition of what the reviewer looks for in each still.

Use this rule for every sampled frame of `C01`–`C20`. A second rater should be able to apply it without asking the first rater. **When uncertain whether an object meets a rule, do not count it** and mention it in Notes.

**What is counted:** parked civilian passenger cars visible in that still frame.

**What is not counted:** unique vehicles across the minute, moving traffic, reflections, duplicates of the same car, or non-passenger vehicles.

## 1. Unit and when to count

Count **occupancy in the still**, not a running total of cars that appeared in the clip.

- Sample the frame at the protocol timestamp (0, 5, …, 55 s). Freeze. Count that image only.
- A car that is present in some frames and gone in others is counted only in frames where it meets the rules.
- Clip-level **Car count** = **median** of the 12 frame counts. For 12 values, that is the mean of the 6th and 7th values when sorted. Record `.5` if it occurs (e.g. `7.5`). Do not round away from `.5`.
- If a timestamp is past the end of the file, skip it, median the remaining frame counts, and note the missing times.

## 2. Passenger car (include)

Count a four-wheeled motor vehicle built mainly to carry people, of these types:

- Sedan, coupe, hatchback, wagon
- SUV or crossover
- Minivan
- Light-duty pickup (personal bed; no commercial box, stake, or utility body)

Include a car under a fitted car cover if it sits in a parking position and the covered shape is passenger-car sized (not motorcycle-sized).

## 3. Not a passenger car (exclude)

Do not count:

- Motorcycles, scooters, bicycles, e-bikes, mopeds
- Buses, shuttles, coaches
- Medium/heavy trucks: box truck, semi, dump, flatbed, bucket, cement, etc.
- Trailers, campers, boat trailers (count the qualifying tow vehicle only, if it is parked and visible)
- RVs / motorhomes
- Golf carts, ATVs, farm or construction equipment, forklifts
- Marked police, fire, ambulance, or military vehicles
- Shopping carts, dumpsters, tire stacks, or other non-vehicles
- Pictures of cars (signs, posters, screens), not physical cars in the scene

Unmarked vehicles that look like ordinary civilian cars **are** counted. Do not guess “undercover” or “fleet” from paint alone.

## 4. Parked (include) vs not parked (exclude)

**Parked:** occupying a stall, marked space, curb parking, driveway, or other storage position, and **not traveling in a drive aisle or roadway** in that still.

Count:

- Empty-looking cars in stalls (no driver needed)
- Cars fully in a stall with brake lights on
- Cars parallel-parked along a curb

Do not count:

- Vehicles in a travel lane, drive aisle, or street through-lane, including those stopped at a light or waiting to turn
- Vehicles clearly mid-maneuver in an aisle (motion blur, straddling the aisle, not in a stall)
- Drive-through or drop-off queues

If a vehicle is partly in a stall and partly in the aisle, count it only if **most of the body is in the stall**. Otherwise exclude.

## 5. Partial visibility

Count a partially visible vehicle only if **all** of the following hold:

1. It is a **distinct** object (not a continuation of a car already counted).
2. You can tell it is a **passenger car** of an included type (not merely “some vehicle”).
3. Enough of the body is seen to meet **at least one** of:
   - About half or more of the vehicle is in frame, or
   - Cabin (or covered cabin shape) **and** at least two wheels, or
   - A characteristic rear or front (two lights, typical width) **and** enough body to separate it from neighbors.

Do **not** count:

- A bumper, mirror, antenna, roof rail, or single wheel alone
- A sliver between two cars that might be a third car or a gap
- A shape that could equally be a motorcycle, trailer tongue, or bin

Cut off by the image edge: count if the partial-visibility test passes. Heavy occlusion by trees, poles, or other cars: same test.

## 6. Reflections, images, and duplicates

Count each **physical car in the camera’s direct view of the parking area once per frame**.

- Reflection in glass, puddle, paint, or chrome: **do not count** the reflection.
- Real car plus its reflection: count **1**.
- Camera or vehicle mirror: count the car in the main scene if it qualifies; **do not** add the mirrored copy. If the car is **only** in a reflection or mirror, **do not count** it.
- Overlapping cars: count each car you can individuate under §§2–5.
- One car spanning two stalls: count **1**.

## 7. Clip-level record

After 12 frame counts:

1. Write each frame count in the clip log (`Count 0s` … `Count 55s`).
2. Write **Car count** = median of those values.
3. Use Notes for exclusions that were close calls, mixed scenes (e.g. one moving car ignored), or missing timestamps.

Do not change this rule mid-dataset. If a later clip exposes a hole, note it; do not silently revise earlier clips unless the whole set is re-counted under a written amendment.

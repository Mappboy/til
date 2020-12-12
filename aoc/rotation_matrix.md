---
categories:
- AOC
- Coding
date: 2020-12-12
tags:
- geometry
- trigonometry
slug: aoc-rotation-matrix
title: Rotation Matrices
---
# Rotation Matrices AKA transforming points around by an angle
I am currently up to day 12 of [Advent of Code](https://adventofcode.com/), thus smashing my measly attempt of 8 last year. I am enjoying the challenge, the problems are pretty easy but not something I've encountered since my Uni Days. 

The challenge for Day 12 involves moving a ship about using **Vectors**. Vectors/Points are something I deal with day to day in my work with GeoSpatial data. However most of the time I can use QGIS functions, or a Python package to transform data. 
Below are the rules for moving your ship in part 2.

    Almost all of the actions indicate how to move a waypoint which is relative to the ship's position:

    ...
    Action L means to rotate the waypoint around the ship left (counter-clockwise) the given number of degrees.
    Action R means to rotate the waypoint around the ship right (clockwise) the given number of degrees.
    Action F means to move forward to the waypoint a number of times equal to the given value.

I vaguely remember doing something like this in a Graphics or Maths unit. After a bit of Google Fu lo and behold I found it <https://en.wikipedia.org/wiki/Rotation_matrix>


![](https://wikimedia.org/api/rest_v1/media/math/render/svg/5e3664dd1600087a4c73f55f9c12f12cc78184c6)

I had penciled out a solution, but in Python here is how to solve our problem.

```python
def rotate_matrix(angle: int, coordinate:tuple, clockwise=True) -> Tuple[int, int]:
    """
    Rotate coordinate around angle.
    :param angle: Angle to rotate coordinate around
    :param coordinate: Coordinate in x,y format
    :param clockwise: Direction to rotate around default is clockwise
    :return: Transformed coordinate
    """
    # This is just to get our values with out calling radians 
    if angle == 90:
        cos_a = 0
        sin_a = 1
    elif angle == 180:
        sin_a = 0
        cos_a = -1
    elif angle == 270:
        sin_a = -1
        cos_a = 0
    else:
        sin_a = sin(radians(angle))
        cos_a = cos(radians(angle))
    if clockwise:
        return ((int(coordinate[0] * cos_a) - int(coordinate[1] * sin_a),
                 int(coordinate[0] * sin_a) + int(coordinate[1] * cos_a)))
    else:
        return ((int(coordinate[0] * cos_a) + int(coordinate[1] * sin_a),
                 int(coordinate[0] * -sin_a) + int(coordinate[1] * cos_a)))
```

Rejoice our little elf can get to his ship. 

# Desks

Nine libraries. One water record. Eight lunar gates. Digital Currensy Inc. owns them. The music, sports, and entertainment products are a different line. These libraries are not those products.

You bring the numbers. The library returns one word, or one line of figures. It does not download a satellite, a map, or a mesh.

| Library | The decision | You type | It prints | A pass is not |
| --- | --- | --- | --- | --- |
| [splitrecord](https://github.com/DigitalCurrensy/splitrecord) | Do two aligned records disagree | two CSV columns, one number per line | `n`, Sen slope of z(A) minus z(B), Mann-Kendall S, and `p`, `short`, or `dependent` | a basin study or a permit |
| [feasfront](https://github.com/DigitalCurrensy/feasfront) | Does this site clear the limits you named | slope in degrees, sun hours, Earth hours, night hours, and the four limits | `ok`, or `slope` `sun` `earth` `night`, or `missing` | a site selection. This desk does not compute the sun |
| [dosepath](https://github.com/DigitalCurrensy/dosepath) | Is there a walk that finishes inside the clock and the dose cap | edges `x1,y1,x2,y2,t,cost`, plus start, goal, clock, and dose cap | the nodes, or the word `stay` | a radiation model |
| [fitslip](https://github.com/DigitalCurrensy/fitslip) | Does every part sit inside its limits | `name,value,lo,hi` | `pass`, `fail`, or `unknown` | a flight bill. A blank is unknown. A low limit above the high limit is unknown. An empty bill fails. Fail beats unknown |
| [pinfault](https://github.com/DigitalCurrensy/pinfault) | Can this pin be left here | void fraction, slope in degrees, offset in meters | `voids`, then `slope`, then `offset`, or `missing`, or `ok` | a landing clearance. It does not read a map. A missing offset is `missing`, not `ok` |
| [rimkeep](https://github.com/DigitalCurrensy/rimkeep) | Is this rim a road | `on_rim`, slope in degrees, shadow setback in meters, width in meters | `on_rim`, `psr`, `missing`, `slope`, `thin`, or `ok` | a traverse. `ok` is not a road. Overlap uses a local plane and a 1,737,400 m Moon, not a geodesic |
| [baghold](https://github.com/DigitalCurrensy/baghold) | Is this pit mouth usable | mouth in meters, floor void fraction, drop in meters, floor slope in degrees | `missing`, `pinch`, `voids`, `drop`, `slope`, or `ok` | a cave survey. A skylight is not a shelter |
| [tubewalk](https://github.com/DigitalCurrensy/tubewalk) | Is this line a tunnel | width in meters, length in meters, echo, clutter | `dark`, `missing`, `pinch`, `stub`, `clutter`, or `ok` | a ceiling. A blank width or a blank length is `missing`, not `ok`. `ok` is not a keep |
| [archhold](https://github.com/DigitalCurrensy/archhold) | Does this roof pass the shape check | span in meters, roof thickness in meters, tensile strength in MPa, and a declared crack | `missing`, `thin`, `wide`, `weak`, `crack`, or `ok` | a structural keep. No finite-element model is run |

## Run one

```
git clone https://github.com/DigitalCurrensy/splitrecord.git
cd splitrecord
pip install -e .
python -m unittest tests.test_kernel
python -m splitrecord examples/left.csv examples/right.csv
```

The other eight use those same two commands. The sample filename and any flags are in that library's README. Python 3.11 or newer. No third-party packages.

## Worked cases

The rows in `examples/` are numbers typed to prove the rule. They are not a file a customer sent. They are not InSAR, GRACE, or a surveyed landing.

## License

Apache-2.0. Copyright 2026 Digital Currensy Inc. Each library carries the unmodified Apache text in `LICENSE` and the copyright in `NOTICE`.

## Visibility

These repositories are private. This index does not make them public.

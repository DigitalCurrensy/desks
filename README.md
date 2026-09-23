# Desks

Nine libraries. One scores two water records. Eight score lunar numbers. You bring the numbers. Each library prints a decision.

| Library | Decision | Input | Output |
| --- | --- | --- | --- |
| [splitrecord](https://github.com/DigitalCurrensy/splitrecord) | Do the two records disagree, after a trend test that allows for ties and for rank autocorrelation | Two columns, one number per line. At least 8 rows before a p-value is printed | `n`, Sen slope of z(A)−z(B), Mann-Kendall S, and a p-value. z uses the sample mean and the sample standard deviation with divisor n−1. Sen slope is the median of (vⱼ−vᵢ)/(j−i). S is up pairs minus down pairs. Variance is n(n−1)(2n+5)/18, minus t(t−1)(2t+5)/18 for each tied group, then multiplied by the Hamed–Rao factor. That factor detrends with the Sen slope, ranks the remainder, and sums every lag whose rank autocorrelation exceeds 1.95996398454/√n. Under 8 rows the p-value is `short`. A non-positive corrected variance is `dependent` |
| [feasfront](https://github.com/DigitalCurrensy/feasfront) | Does the site clear the slope limit and the hour limits | Either hours you already have, or latitude, longitude, a horizon angle, and a duration. Sun hours count steps whose solar elevation is above the horizon. The subsolar longitude walks 360° in 29.530588853 days. Earth hours are the whole duration if Earth is above that horizon at the sub-Earth point you supply, otherwise zero. Night hours are duration minus sun hours | `ok`, or the failed names `slope`, `sun`, `earth`, `night`, or `missing`. No terrain. No libration. An empty set of sites is a result |
| [dosepath](https://github.com/DigitalCurrensy/dosepath) | Is there an 8-neighbor walk inside the clock and the dose cap | Edges `x1,y1,x2,y2,t,cost`. Orthogonal and diagonal steps each cost one tick. A missing edge is not a step. A negative cost is not a step. Dose is the sum of the costs you wrote | The nodes, or `stay` |
| [fitslip](https://github.com/DigitalCurrensy/fitslip) | Is every part inside its limits | One CSV of `name,value,lo,hi`, or a values file plus an envelope file of `name,lo,hi` | `pass`, `fail`, or `unknown`. A blank, a low limit above the high limit, or a name missing from the envelope is unknown. An empty bill is fail. Fail beats unknown |
| [pinfault](https://github.com/DigitalCurrensy/pinfault) | Can the pin stay | Void fraction, or `n_invalid` and `n_cells`, plus slope in degrees and offset in meters | `voids` if the fraction is above 0.15, else `slope` if slope is above 20°, else `offset` if offset is above 30 m, else `ok`. A fraction outside 0 to 1, a negative slope, a negative offset, or a missing offset is `missing` |
| [rimkeep](https://github.com/DigitalCurrensy/rimkeep) | Is the rim a road | `on_rim`, inner slope in degrees, shadow setback in meters, width in meters | `on_rim`, then `psr` if the setback is under 50 m, then `missing`, then `slope` over 15°, then `thin` under 30 m, else `ok`. A negative slope, width, or setback is `missing`. Overlap is a haversine on a sphere of radius 1,737,400 m |
| [baghold](https://github.com/DigitalCurrensy/baghold) | Is the pit mouth usable | Mouth in meters, floor void fraction, optional drop in meters, floor slope in degrees | `missing`, then `pinch` under 30 m, then `voids` over 0.15, then `drop` over 30 m, then `slope` over 20°, else `ok`. A negative measure, or a void fraction outside 0 to 1, is `missing`. A missing drop is not a fail. A skylight is not a shelter |
| [tubewalk](https://github.com/DigitalCurrensy/tubewalk) | Is the line a tunnel | Width in meters, length in meters, echo, clutter | `dark` if the echo is missing or `none`, then `missing` if width or length is blank or negative, then `pinch` under 10 m, then `stub` under 30 m, then `clutter`, else `ok`. Zero is a number. `ok` is not a ceiling |
| [archhold](https://github.com/DigitalCurrensy/archhold) | Does the roof pass the shape check, and an optional depth check | Span in meters, roof thickness in meters, tensile strength in MPa, a crack flag, and an optional depth in meters | `missing`, then `thin` under 2 m, then `wide` over 5,000 m, then `weak` under 1 MPa, then `crack`, then `load` if depth is supplied and lithostatic stress 3100×1.62×depth/10⁶ MPa exceeds the Hoek–Brown unconfined mass strength in that repo, else `ok`. A negative span, thickness, strength, or depth is `missing`. The load line is not a mesh. `ok` is not a keep |

## Run

```
git clone https://github.com/DigitalCurrensy/splitrecord.git
cd splitrecord
pip install -e .
python -m unittest tests.test_kernel
python -m splitrecord examples/left.csv examples/right.csv
```

The other eight use the same install and the same unittest command. The sample filename is `examples/` in that repo. Python 3.11 or newer. No third-party packages.

## Worked rows

Rows in `examples/` were typed to prove the rule. They are not a customer file.

## License

Apache-2.0. Copyright 2026 Digital Currensy Inc. `LICENSE` is the unmodified Apache text. `NOTICE` holds the copyright.

## Visibility

These repositories are private. This index does not change that.

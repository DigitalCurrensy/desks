# Desks

Two kinds of library. One trend test. Eight lunar site gates. Digital Currensy Inc. owns them.

You type the numbers. The library prints one word, or one line of figures. It does not download a satellite, a map, or a mesh.

## The trend test

[splitrecord](https://github.com/DigitalCurrensy/splitrecord) is a trend library for two aligned columns, one number per line. The columns are whatever records you already have. A water level is one use. The code does not know the unit.

Each column becomes a sample z-score: subtract the mean, divide by the sample standard deviation. The divisor is n−1. The residual is z(A) minus z(B). A column with no spread is refused.

The library then prints two different numbers. One is the size of the drift. The other is a test of whether the residual is monotonic.

**Theil–Sen slope.** The size. For every pair of rows i < j, the slope is (vⱼ − vᵢ) / (j − i). The result is the median of those slopes. An odd count takes the middle slope. An even count takes the average of the two middle slopes. The unit is z per row, because the denominator is the row gap, not a date. The estimator does not assume a normal distribution. It returns no intercept and no confidence interval. A median is why one wild point does not set the answer. The known breakdown point of this estimator is 1 − 1/√2, about 29%. This library computes the median. It does not run a separate breakdown trial.

**Mann–Kendall test.** The order. S counts pairs where the later row is higher, minus pairs where the later row is lower. A tie adds nothing. S is a count. It is not a slope and not a probability. For 8 or more rows, a two-sided p-value is the normal approximation with the continuity correction (S − sign(S)) / √var. The variance starts at n(n−1)(2n+5)/18. Each tied group of size t > 1 subtracts t(t−1)(2t+5)/18. That variance is multiplied by the Hamed–Rao factor, so a series that repeats itself is not treated as independent. The factor removes the Theil–Sen slope, ranks what remains, and keeps a lag only when its autocorrelation exceeds 1.95996398454/√n. The autocorrelation uses one mean of the whole rank series and the full sum of squares. Under 8 rows the printed p-value is `short`. The exact small-sample distribution is not computed. A non-positive corrected variance is `dependent`. The p-value is not a certificate.

The printed Mann-Kendall line also carries Kendall's tau-b, the corrected variance, `n_over_nstar`, and `z`. `p` is erfc(|z| / sqrt(var)). On a straight residual, `n_over_nstar` is 1. Yue and Wang's lag-1 factor is not used.

Sen's 95% interval is two ranks in the sorted pairwise slopes, using the tie-corrected variance with no Hamed-Rao factor. hamed95 is the same rank rule after that variance is multiplied by n/n*.

Under 8 rows with no ties, splitrecord labels the interval sen95=exact. That rank is the exact no-tie Sen interval, not the normal approximation. Sen's seven-point series, times 1, 2, 3, 4, 10, 12, 18 and values 9, 15, 19, 20, 45, 55, 78, has median slope 4 and exact limits 3.714285714 and 4.375. At 8 rows and above the label is sen95=normal.

gilbert95 is the interpolated form of that normal approximation: a straight line between the floor rank and the ceiling rank. It is not the rounded sen95=normal pair, and it is not a table copied from Gilbert (1987).

The other eight lines print the inputs next to the word. A fit line prints value, low, and high. A pin line prints void fraction, slope, and offset. A rim line prints on-rim, slope, setback, and width. A pit line prints mouth, void fraction, drop, and slope. A tube line prints width, length, echo, and clutter. A roof line prints span, roof, tensile, crack, ucs, and lithostatic. A site line says whether the hours were supplied or computed. A walk line prints the dose and the number of edges.

The default line is `variance=hamed-rao`. That correction is for autocorrelation in one series. It does not stop January from being compared with July. `--seasons 12` is the seasonal Mann-Kendall test: each month is compared only with the same month in later years. Its variance is the sum of the monthly variances, and the slope is z per year. `--covariance` uses the Hirsch-Slack covariance instead. Hamed-Rao is not multiplied on top of either seasonal variance. A short last year makes `--covariance` refuse the table as `uneven`.

`--prewhiten` removes lag-1 only after the Theil-Sen slope is taken off, then puts the slope back. The variance on that line is `ordinary`. It is not Hamed-Rao, and it is not the seasonal test. A flag that asks for two of these corrections is refused.

The worked pre-whitening file is `examples/pw_left.csv` with `examples/pw_right.csv` in splitrecord. Nine equally spaced rows. Sen's slope is the median of the 36 pairwise slopes. The line prints that removed slope and the slope of the blended series as two fields.


## The eight gates

| Library | Kind | Question | You type | It prints |
| --- | --- | --- | --- | --- |
| [feasfront](https://github.com/DigitalCurrensy/feasfront) | Flat-horizon hours, then a limit check | Does the site clear the limits you named | Latitude, longitude, horizon angle, and duration, or hours you already have, plus the slope | `ok`, or `slope`, `sun`, `earth`, `night`, or `missing`. Sun hours count steps with the solar elevation above the horizon. The subsolar longitude walks 360° in 29.530588853 days. Earth hours are the whole duration or zero. Night is duration minus sun hours. No terrain. No libration |
| [dosepath](https://github.com/DigitalCurrensy/dosepath) | Dose-capped grid walk | Is there a walk inside the clock and the dose cap | Edges `x1,y1,x2,y2,t,cost`, plus start, goal, clock, and dose cap | The nodes, or `stay`. Orthogonal and diagonal steps each cost one tick. A missing edge, a negative cost, or a non-finite cost is not a step |
| [fitslip](https://github.com/DigitalCurrensy/fitslip) | Parts envelope | Is every part inside its limits | `name,value,lo,hi`, or a values file plus `name,lo,hi` | `pass`, `fail`, or `unknown`. A blank, a non-finite number, a reversed limit, or a name missing from the envelope is unknown. An empty bill fails. Fail beats unknown |
| [pinfault](https://github.com/DigitalCurrensy/pinfault) | Pin clearance | Can the pin stay | Void fraction, or `n_invalid` and `n_cells`, plus slope in degrees and offset in meters | `voids` above 0.15, else `slope` above 20°, else `offset` above 30 m, else `ok`. A fraction outside 0 to 1, a negative number, a non-finite number, or a missing offset is `missing` |
| [rimkeep](https://github.com/DigitalCurrensy/rimkeep) | Rim road gate, plus a sphere distance | Is the rim a road | `on_rim`, inner slope, shadow setback, width | `on_rim`, then `psr` under 50 m, then `missing`, then `slope` over 15°, then `thin` under 30 m, else `ok`. Overlap is a haversine on a sphere of radius 1,737,400 m |
| [baghold](https://github.com/DigitalCurrensy/baghold) | Pit mouth gate | Is the mouth usable | Mouth, floor void fraction, optional drop, floor slope | `missing`, then `pinch` under 30 m, then `voids` over 0.15, then `drop` over 30 m, then `slope` over 20°, else `ok`. A missing drop is not a fail. A skylight is not a shelter |
| [tubewalk](https://github.com/DigitalCurrensy/tubewalk) | Tube line gate | Is the line a tunnel | Width, length, echo, clutter | `dark` if the echo is missing or `none`, then `missing`, then `pinch` under 10 m, then `stub` under 30 m, then `clutter`, else `ok`. Zero is a number. `ok` is not a ceiling |
| [archhold](https://github.com/DigitalCurrensy/archhold) | Roof thickness, plus a closed-form rock check | Does the roof pass the shape check | Span, thickness, tensile strength, a crack flag, optional depth | `missing`, then `thin` under 2 m, then `wide` over 5,000 m, then `weak` under 1 MPa, then `crack`, then `load` if the lithostatic stress 3100×1.62×depth/10⁶ MPa exceeds the Hoek–Brown unconfined mass strength, else `ok`. The load line is not a mesh. `ok` is not a keep |

## Run

```
git clone https://github.com/DigitalCurrensy/splitrecord.git
cd splitrecord
pip install -e .
python -m unittest tests.test_kernel
python -m splitrecord examples/left.csv examples/right.csv
```

The other eight use the same install and the same unittest command. The sample file is under `examples/` in that repo. Python 3.11 or newer. No third-party packages.

## Worked rows

Rows in `examples/` were typed to prove the rule. They are not a customer file.

## License

Apache-2.0. Copyright 2026 Digital Currensy Inc. `LICENSE` is the unmodified Apache text. `NOTICE` holds the copyright.

## Visibility

These repositories are private. This index does not change that.

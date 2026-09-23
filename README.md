# Desks
One water desk. Eight lunar gates. Each one applies a rule and is allowed to refuse.

Digital Currensy Inc. also builds platforms for music, sports, entertainment, and the creator economy. These nine repositories are a different line. They are small Apache-2.0 libraries. They are not that business.

| Repo | Who it is for | What it will not do |
| --- | --- | --- |
| splitrecord | hydrologist with two official records of one basin | does not average them and does not fetch satellite granules |
| feasfront | lander team dropping sites | does not compute solar geometry; the caller supplies hours and slope |
| dosepath | crew planner on a cost grid | does not run a radiation transport model |
| fitslip | payload engineer with a parts list | does not look up materials; missing is not a pass |
| pinfault | mapper with a pin | does not read a map; the caller supplies void fraction, slope, and offset |
| rimkeep | traverse planner at a crater rim | on the rim is not a road; overlap is a local plane, not a geodesic |
| baghold | scout at a pit mouth | a skylight is not a shelter |
| tubewalk | radar reader with a line | the line is not a ceiling |
| archhold | reviewer of a roof span | ok is not a structural keep; no finite-element model is run |

## What a worked case is
Numbers shipped in examples/ and tests prove the rule. They are not a file a customer sent. They are not InSAR, GRACE, or a surveyed landing.

## License
Apache-2.0. Copyright 2026 Digital Currensy Inc. Each desk repo carries the unmodified Apache license text in LICENSE and the copyright in NOTICE.

## Not yet public
These repositories are private until the owner changes visibility. This index does not publish them.

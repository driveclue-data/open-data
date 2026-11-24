# DriveClue open data

Free datasets on used car reliability, car recalls, owner complaints and UK MOT results, from [DriveClue](https://driveclue.com). They hold the numbers behind DriveClue's reports, built from public government records (NHTSA, Transport Canada, the U.S. EPA and DVSA). Licensed [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

This repository is a snapshot taken 2026-11-24. The live files, updated as the agencies add records, are at https://driveclue.com/data.

| Dataset | Files | Rows |
| --- | --- | --- |
| [Used car reliability by model year: complaints, recalls and Lemon Scores](#used-car-reliability) | [used-car-reliability.csv](data/used-car-reliability.csv) | 7,723 |
| [At what mileage car problems start: owner-reported mileage by model year and problem area](#car-problem-mileage) | [car-problem-mileage.csv](data/car-problem-mileage.csv) | 3,088 |
| [Car complaints by U.S. state: NHTSA owner complaints by state, model and problem area](#car-complaints-by-state) | [car-complaints-by-state-and-model.csv](data/car-complaints-by-state-and-model.csv)<br>[car-complaints-by-state-and-area.csv](data/car-complaints-by-state-and-area.csv) | 18,547<br>1,285 |
| [UK MOT failure rates by make, model and year first used (2025)](#uk-mot-failure-rates) | [uk-mot-2025-failure-rates.csv](data/uk-mot-2025-failure-rates.csv) | 4,225 |

<a id="used-car-reliability"></a>

## Used car reliability by model year: complaints, recalls and Lemon Scores

One row per model year of every car, SUV, pickup and van DriveClue tracks, from 2005 on for most models. Each row has the owner complaints filed with the U.S. National Highway Traffic Safety Administration (NHTSA) and how many of them reported a crash, fire, injury or death; NHTSA safety recalls and how many are serious; Transport Canada recalls; NHTSA's 5-star overall crash rating; the EPA's best combined fuel economy; and the DriveClue Lemon Score, a 0–100 grade (higher is better) built only from that public data, with its four parts. A year-to-avoid flag marks up to three years of each model that drew at least twice the complaints of the model's typical year, the same rule as DriveClue's model pages.

Source page, always the latest version: https://driveclue.com/data/used-car-reliability
Report built from it: [Lemon Score: how used cars are scored](https://driveclue.com/lemon-score)

### Files

#### [used-car-reliability.csv](data/used-car-reliability.csv)

One row per model year with a Lemon Score or NHTSA complaint data. 7,723 rows.

| Column | Type | What it holds |
| --- | --- | --- |
| `make` | string | Make, as DriveClue names it (Toyota, Mercedes-Benz). |
| `model` | string | Model, as DriveClue names it. |
| `year` | integer | Model year. |
| `lemon_score` | integer | Lemon Score, 0–100, higher is better. Blank when the year doesn't have enough data to score. |
| `provisional` | boolean | true for model years under two years old, whose complaints are still arriving. Blank without a score. |
| `score_model_history` | integer | Part of the score (35%): complaints against the model's other years, 0–100. Blank without enough data. |
| `score_same_age` | integer | Part of the score (25%): complaints per year on the road against all cars of the same age, 0–100. |
| `score_recalls` | integer | Part of the score (20%): safety recalls against cars of the same era, 0–100. |
| `score_crash_rating` | integer | Part of the score (20%): NHTSA's overall crash rating, 0–100. Blank when NHTSA didn't rate the car. |
| `complaints` | integer | Owner complaints filed with NHTSA about this model year. |
| `complaints_crash_fire_injury` | integer | Of those, complaints that report a crash, fire, injury or death. |
| `us_recalls` | integer | NHTSA safety recall campaigns that cover this model year. |
| `us_serious_recalls` | integer | Of those, recalls that tell owners to park the car, or that involve air bags, fuel, brakes or steering. |
| `canada_recalls` | integer | Transport Canada recalls that cover this model year. |
| `nhtsa_overall_stars` | integer | NHTSA 5-Star Safety Ratings overall rating, 1–5. Blank when not rated. |
| `epa_best_combined_mpg` | number | Best combined fuel economy of the model year's versions, U.S. miles per gallon (EPA). Blank when not listed. |
| `year_to_avoid` | boolean | true for the model's years to avoid: up to three years with at least 20 complaints and at least twice the complaints of the model's median year. Blank for BMW series, whose pages combine their trims. |
| `page_url` | string | The model's page on DriveClue, with every year's numbers. |

### How it was made

- Complaints, recalls and crash ratings come from NHTSA, Canadian recalls from Transport Canada's Vehicle Recalls Database and fuel economy from the EPA. Each model year is downloaded again on a schedule, so the file changes as the agencies add records.
- The Lemon Score weighs four parts: complaints against the model's other years (35%), complaints per year on the road against all cars, with crash, fire and injury reports counting extra (25%), safety recalls against cars of the same era, with serious recalls counting double (20%), and NHTSA's overall crash rating (20%). A missing part is dropped and the others are reweighted.
- Comparing a model's years with each other cancels out sales volume: a best-seller draws more complaints than a rare car in every year, so its raw count says little on its own.
- Years to avoid use the rule on DriveClue's model pages: a model needs four years with complaint data, and a year qualifies with at least 20 complaints and at least twice the complaints of the model's median year. At most three years are named.

### What it can't tell you

- Complaints are reports owners chose to file, not checked defects or failure rates.
- Recent model years have had less time to collect complaints; that's why they're marked provisional.
- One recall campaign often covers several model years, so don't add recalls up across years.
- The models come from NHTSA's vehicle database, built from cars sold in the United States. Most are sold in Canada too; Canada-only models are missing.

### Sources

- [NHTSA owner complaints, recalls and 5-Star Safety Ratings](https://www.nhtsa.gov/nhtsa-datasets-and-apis) (U.S. government work, public domain)
- [Transport Canada Vehicle Recalls Database](https://opendatatc.tc.canada.ca/vrdb_full_monthly.csv) (Open Government Licence – Canada)
- [U.S. EPA fuel economy data (fueleconomy.gov)](https://www.fueleconomy.gov/feg/download.shtml) (U.S. government work, public domain)

Contains information licensed under the Open Government Licence – Canada (https://open.canada.ca/en/open-government-licence-canada).

### Licence and credit

[Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/). Please credit DriveClue with a link to https://driveclue.com/data/used-car-reliability:

> DriveClue, "Used car reliability by model year: complaints, recalls and Lemon Scores", https://driveclue.com/data/used-car-reliability, licensed CC BY 4.0

Updates: Rebuilt from the latest stored data every day. Questions, corrections or a custom cut of the data: hello@driveclue.com.

<a id="car-problem-mileage"></a>

## At what mileage car problems start: owner-reported mileage by model year and problem area

For each 2010-and-newer model year at least five years old, the mileage at which owners said problems happened, by the problem area they named (engine, transmission, electrical system, brakes and more): the 25th percentile, median and 75th percentile, in miles and kilometres. Built from NHTSA's bulk owner-complaint files, with each complaint weighted to correct for NHTSA collecting mileage on far fewer complaints since 2022. These are the numbers behind DriveClue's report "At what mileage do car problems start?".

Source page, always the latest version: https://driveclue.com/data/car-problem-mileage
Report built from it: [At what mileage do car problems start?](https://driveclue.com/lemon-score/when-car-problems-start)

### Files

#### [car-problem-mileage.csv](data/car-problem-mileage.csv)

One row per model year and problem area, up to six areas per model year. 3,088 rows.

| Column | Type | What it holds |
| --- | --- | --- |
| `make` | string | Make, as DriveClue names it (Toyota, Mercedes-Benz). |
| `model` | string | Model, as DriveClue names it. |
| `year` | integer | Model year. |
| `problem_area` | string | The part of the car the complaints name, in plain words (engine, transmission/powertrain, electrical system). |
| `complaints_with_mileage` | integer | Complaints about this area that gave a mileage. One complaint counts once per area. |
| `miles_p25` | integer | 25th percentile of the reported mileage, miles (weighted, see the method). |
| `miles_median` | integer | Median reported mileage, miles. |
| `miles_p75` | integer | 75th percentile of the reported mileage, miles. |
| `km_p25` | integer | 25th percentile, kilometres. |
| `km_median` | integer | Median, kilometres. |
| `km_p75` | integer | 75th percentile, kilometres. |
| `model_year_complaints_with_mileage` | integer | All complaints about this model year that gave a mileage. |
| `page_url` | string | The model's page on DriveClue, with every year's numbers. |

### How it was made

- We read NHTSA's full owner-complaint files on the 3rd of each month and match each complaint to a model year by make, model and year.
- Mileage below 100 or above 400,000 miles is dropped: blanks typed as 0 and thousands typed short are common.
- NHTSA collected a mileage on about 80% of complaints through 2020 and about 15% since 2022. Taken at face value that makes newer cars look like they fail early, so each complaint is weighted by how rarely mileage was collected in the year it was filed.
- A problem area is listed when at least 20 complaints about it gave a mileage, and enough of them that a few heavily weighted ones can't decide the result. Model years under five years old are left out: their cars haven't been driven far enough yet.

### What it can't tell you

- The mileage is what the owner typed when filing, which may be when they noticed the problem rather than when it began.
- The percentiles describe cars whose owners complained, not every car of that model year.
- Compare a model year with others of the same age: older cars have had more time to cover distance.

### Sources

- [NHTSA owner complaint flat files (FLAT_CMPL)](https://static.nhtsa.gov/odi/ffdd/cmpl/CMPL.txt) (U.S. government work, public domain)

### Licence and credit

[Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/). Please credit DriveClue with a link to https://driveclue.com/data/car-problem-mileage:

> DriveClue, "At what mileage car problems start: owner-reported mileage by model year and problem area", https://driveclue.com/data/car-problem-mileage, licensed CC BY 4.0

Updates: Rebuilt after NHTSA's complaint files are read on the 3rd of each month. Questions, corrections or a custom cut of the data: hello@driveclue.com.

<a id="car-complaints-by-state"></a>

## Car complaints by U.S. state: NHTSA owner complaints by state, model and problem area

Owner complaints filed with the U.S. National Highway Traffic Safety Administration (NHTSA) about 2010-and-newer cars, counted by the owner's state (the 50 states and the District of Columbia), in two files: one by state and model, one by state and problem area. These are the counts behind DriveClue's report on car complaints by state.

Source page, always the latest version: https://driveclue.com/data/car-complaints-by-state
Report built from it: [Car complaints by state](https://driveclue.com/lemon-score/car-complaints-by-state)

### Files

#### [car-complaints-by-state-and-model.csv](data/car-complaints-by-state-and-model.csv)

One row per state and model with at least one complaint. 18,547 rows.

| Column | Type | What it holds |
| --- | --- | --- |
| `state_code` | string | USPS state code (TX, DC). |
| `state` | string | State name. |
| `make` | string | Make, as DriveClue names it (Toyota, Mercedes-Benz). |
| `model` | string | Model, as DriveClue names it. |
| `complaints` | integer | Complaints from the state's owners about this model, all model years from 2010 on. |
| `page_url` | string | The model's page on DriveClue, with every year's numbers. |

#### [car-complaints-by-state-and-area.csv](data/car-complaints-by-state-and-area.csv)

One row per state and problem area. 1,285 rows.

| Column | Type | What it holds |
| --- | --- | --- |
| `state_code` | string | USPS state code (TX, DC). |
| `state` | string | State name. |
| `problem_area` | string | The part of the car the complaints name, in plain words. |
| `complaints` | integer | Complaints from the state's owners naming this area. One complaint can name several areas. |
| `state_complaints` | integer | All complaints from the state's owners, each counted once. |

### How it was made

- The state is the owner's state on each complaint in NHTSA's full complaint files; 99.6% of complaints about 2010-and-newer cars name one of the 50 states or DC.
- Complaints about one model from one city on the same day count at most twice, so a fleet filing a batch of complaints doesn't make a model look like a state's problem.
- BMW trims count toward their series: a 328i counts toward the 3 Series.
- One complaint can name several problem areas, so a state's area counts add up to more than its total.

### What it can't tell you

- Raw counts follow each state's population and what sells there. To see what a state complains about more than others, compare shares, as the report does.
- The owner's state isn't always where the problem happened.

### Sources

- [NHTSA owner complaint flat files (FLAT_CMPL)](https://static.nhtsa.gov/odi/ffdd/cmpl/CMPL.txt) (U.S. government work, public domain)

### Licence and credit

[Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/). Please credit DriveClue with a link to https://driveclue.com/data/car-complaints-by-state:

> DriveClue, "Car complaints by U.S. state: NHTSA owner complaints by state, model and problem area", https://driveclue.com/data/car-complaints-by-state, licensed CC BY 4.0

Updates: Rebuilt after NHTSA's complaint files are read on the 3rd of each month. Questions, corrections or a custom cut of the data: hello@driveclue.com.

<a id="uk-mot-failure-rates"></a>

## UK MOT failure rates by make, model and year first used (2025)

First MOT test results in Great Britain in 2025 for cars and light vans, by make, model and the year the vehicle was first used, from DVSA's anonymised MOT data: the number of tests, the share that failed (including defects fixed during the test, the way DVSA counts it), the average odometer reading, and the share failing on tyres, brakes, suspension, and lights and electrics, next to the failure rate of every vehicle first used that year. These are the numbers behind DriveClue's UK MOT failure rates report.

Source page, always the latest version: https://driveclue.com/data/uk-mot-failure-rates
Report built from it: [UK MOT failure rates](https://driveclue.com/uk/mot-failure-rates)

### Files

#### [uk-mot-2025-failure-rates.csv](data/uk-mot-2025-failure-rates.csv)

One row per model and year first used with at least 500 first tests in 2025. 4,225 rows.

| Column | Type | What it holds |
| --- | --- | --- |
| `make` | string | Make, as DriveClue names it (Toyota, Mercedes-Benz). |
| `model` | string | Model, as DriveClue groups DVSA's model names. |
| `first_used` | integer | Year the vehicle was first used (registered). |
| `tests` | integer | First MOT tests in 2025 (retests left out). |
| `fail_rate_pct` | number | Share of those tests that failed, %. A fail is F or PRS (a defect fixed during the test), as DVSA reports it. |
| `average_miles` | integer | Average odometer reading at the test, miles. |
| `tyres_fail_pct` | number | Share of tests failing on tyres, %. |
| `brakes_fail_pct` | number | Share of tests failing on brakes, %. |
| `suspension_fail_pct` | number | Share of tests failing on suspension, %. |
| `lights_fail_pct` | number | Share of tests failing on lights and electrics, %. |
| `all_vehicles_fail_rate_pct` | number | Failure rate of every car and light van first used in the same year, %. |

### How it was made

- We read every 2025 test result and failure item in DVSA's anonymised MOT data and keep first tests of cars and light vans, leaving out retests.
- A test counts as failed when DVSA records F (fail) or PRS (pass after rectification: a defect fixed during the test), the way DVSA reports failure rates.
- A model and first-used year is listed when it had at least 500 first tests. DVSA's model names are grouped so spelling variants count as one model.

### What it can't tell you

- Older cars fail more often, so compare models first used in the same year.
- How far and how hard cars are driven, and how they're looked after, differs by model: a failure rate isn't a reliability rating on its own.

### Sources

- [DVSA MOT anonymised data, 2025 test results and items](https://open.data.dvsa.gov.uk/mot-anonymised/index.html) (Open Government Licence v3.0)

Contains public sector information licensed under the Open Government Licence v3.0 (https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/).

### Licence and credit

[Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/). Please credit DriveClue with a link to https://driveclue.com/data/uk-mot-failure-rates:

> DriveClue, "UK MOT failure rates by make, model and year first used (2025)", https://driveclue.com/data/uk-mot-failure-rates, licensed CC BY 4.0

Updates: Updated once a year, when DVSA publishes a full year of MOT data. Questions, corrections or a custom cut of the data: hello@driveclue.com.

## Citing

Cite the dataset you used, with the citation under it. GitHub's "Cite this repository" button reads [CITATION.cff](CITATION.cff) for the collection as a whole.

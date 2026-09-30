# Evidence and reproducibility

## Historical project achievements

The portfolio owner supplied the project summary in his Software QA Engineer resume as the preferred source for historical achievements: 85+ JUnit test cases authored, code coverage improved from 74% to 96%, 15 reliability bugs identified, and a 95% mutation score. These describe the broader March–June 2025 project; they are not all independently recoverable from this final source archive.

The supplied resume describes a separate 2026 Airline Microservices project with GitHub Actions. That pipeline is not presented as part of the original 2025 reservation-system archive. The workflow in this repository was added during portfolio preparation.

## Original evidence

| Source | Measurements | Location |
| --- | --- | --- |
| SonarQube screenshots | Overall coverage 77.1% → 94.8%; maintainability issues 146 → 6; reliability issues 1 → 0 | [Before](images/sonarqube-before.png), [after](images/sonarqube-after.png) |
| Assessment report, sections 4.2 and 5.2 | Line coverage 77.2% → 95.5%; condition coverage 75.8% → 94%; tests 87 → 155 | [PDF](Software-Quality-Report.pdf), pages 7–8 and 11 |
| Embedded PIT output | Mutation score 71% → 95%; final result 202 killed out of 212 generated mutants | PDF pages 14 and 21–22 |
| Embedded final test output | 161 tests, zero failures, errors, or skips | PDF page 21 |
| Team contribution section | Vallabh: SonarQube deployment, codebase integration, four class refactors, and 35 tests for Assessment 3 | PDF pages 22–23 |

The PDF and supplied screenshots are copied without alteration. The dashboard retains the original `Tuesday6pm_Team3` analysis identifier, while the supplied folder and report identify Team 4.

## Interpreting the numbers

- The resume, report tables, and screenshots contain different historical measurements. They are retained with their own labels rather than combined into one run.
- SonarQube overall coverage, line coverage, condition coverage, JaCoCo branch coverage, and PIT mutation coverage measure different things. A percentage from one is not a substitute for another.
- The report's summary table records 155 tests, while its embedded final console output shows 161. A fresh run of the supplied source also executes 161 tests: 151 ordinary test methods and 10 invocations from three parameterized methods.
- The report contains inconsistent mutation counts and narrative summaries. The embedded final PIT output is the basis for the historical 95% mutation score.
- Both SonarQube dashboard screenshots show failed new-code checks. They demonstrate quality improvements, not a completely passing SonarQube gate.
- This source archive has no original Git history or baseline source snapshot. The historical before-and-after results therefore rely on the supplied documents. Current results can be reproduced from the commands in the README.

## Current verification

See [VERIFICATION.md](VERIFICATION.md) for results measured from this checkout. The production code and test cases were preserved during portfolio packaging. Build configuration was updated to produce readable reports and enforce thresholds.

## Tool references

- [JaCoCo Maven reporting](https://www.jacoco.org/jacoco/trunk/doc/maven.html)
- [JaCoCo coverage checks](https://www.jacoco.org/jacoco/trunk/doc/check-mojo.html)
- [PIT Maven configuration](https://pitest.org/quickstart/maven/)

# Local verification record

Verified on **1 October 2026** using the source in this repository.

## Environment and command

- Java: Oracle JDK 21.0.5, macOS arm64.
- Maven: 3.9.12.
- JUnit Jupiter: 5.9.1; Surefire: 3.0.0-M7.
- JaCoCo: 0.8.13.
- PIT: 1.15.0 with its JUnit 5 plugin 1.1.2 and `DEFAULTS` mutators.

```bash
mvn --batch-mode --no-transfer-progress clean verify org.pitest:pitest-maven:mutationCoverage
```

## Measured results

| Measurement | Result |
| --- | ---: |
| Tests executed | 161 |
| Failures / errors / skipped | 0 / 0 / 0 |
| Unit test invocations | 133 |
| Integration test invocations | 28 |
| JaCoCo line coverage | 363 / 378 = **96.03%** |
| JaCoCo branch coverage | 220 / 234 = **94.02%** |
| PIT mutation score | 202 / 212 = **95.28%** (PIT displays 95%) |
| Surviving mutations | 10 |
| Mutations with no coverage | 0 |
| JaCoCo line ≥95%, branch ≥90% | Passed |
| PIT mutation score ≥90% | Passed |

PIT separately reports 364 / 381 covered lines for mutated classes. Its instrumentation and denominator differ from JaCoCo's; the two line coverage figures are not combined.

The coverage gate was also tested with a temporary command-line requirement of 100% line coverage. The check failed with the expected coverage violation. The configured threshold remains 95%.

## Reproducible evidence

- [JaCoCo XML](results/jacoco.xml)
- [PIT mutation XML](results/mutations.xml)
- [SHA-256 hashes of production and test source](results/source-sha256.txt)

These are snapshots from the successful verification run. Fresh reports are generated under `target/`; they may vary if source, compiler, or tool versions change. Full Surefire XML files are generated locally rather than committed because they include environment properties.

The original source and tests passed before packaging and were preserved. Maven metadata, report formats, PIT plugin dependency placement, and executable quality thresholds were updated. The legacy GitLab configuration was retained unchanged.

The results above record local verification. The project was subsequently published to GitHub; see [hosted workflow runs](https://github.com/VallabhMonash/airline-test-automation/actions/workflows/quality.yml) for runner results and downloadable artifacts associated with each commit.

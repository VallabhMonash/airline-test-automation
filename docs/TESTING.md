# Test strategy and representative cases

The tests exercise an in-memory airline reservation system. Coverage analysis identifies code that was not executed; mutation analysis checks whether assertions detect changes to the code that was executed.

## Test map

This map was compiled from the supplied source during portfolio preparation. It is a navigation aid, not the original requirements traceability matrix mentioned in the resume.

| Behavior | Technique | Representative source |
| --- | --- | --- |
| Aircraft seat totals and setter boundaries | Boundary-value and invalid-input testing | [AirplaneTest](../src/test/java/com/ars/unit/AirplaneTest.java): `testInvalidTotalSeatsThrows`, `testSetterAcceptsExactlyMaxSeats` |
| Flight identifiers, cities, and company codes | Parameterized equivalence classes | [FlightTest](../src/test/java/com/ars/unit/FlightTest.java): `testInvalidDepartParameters`, `testFlightConstructorInvalidId`, `testFlightConstructorInvalidCodeOrCompany` |
| Passenger phone normalization and passport formats | Grouped assertions across input formats | [PassengerTest](../src/test/java/com/ars/unit/PassengerTest.java): `testPhoneNormalizationAllAtOnce`, `testValidPassportFormatsAllAtOnce` |
| Child and senior fare boundaries | Boundary-value tests and price assertions | [TicketTest](../src/test/java/com/ars/unit/TicketTest.java): `testBoundaryAgeDiscountChild`, `testBoundaryAgeDiscountSenior` |
| Missing aircraft/flights and existing bookings | Static mocks and failure-path assertions | [TicketSystemTest](../src/test/java/com/ars/unit/TicketSystemTest.java): `testBuyTicketNoAirplaneFound`, `testBuyTicketNoFlightFound`, `testBuyTicketAlreadyBooked` |
| Business/economy booking and connecting flights | Integration tests of collaborating domain objects | [TicketSystemIntegrationTest](../src/test/java/com/ars/Integration/TicketSystemIntegrationTest.java): `testBuyTicketSuccessEconomy`, `testBuyTicketSuccessBusinessVip`, `testChooseTicketWithConnection` |

## Execution

```bash
# Full regression suite and JaCoCo thresholds
mvn --batch-mode --no-transfer-progress clean verify

# A focused booking integration suite
mvn --batch-mode --no-transfer-progress -Dtest=TicketSystemIntegrationTest test

# Mutation analysis over production classes using both test packages
mvn --batch-mode --no-transfer-progress test-compile org.pitest:pitest-maven:mutationCoverage
```

Both unit and integration classes use names ending in `Test`, so Maven Surefire runs both during the `test` phase. This project does not use a separate Failsafe integration-test phase. Run `clean verify` before assessing full-suite coverage: a focused test command produces only partial coverage.

## Regression protection

- JaCoCo reports line and branch coverage for all production classes. The build fails below 95% line coverage or 90% branch coverage.
- PIT applies its `DEFAULTS` mutator group and fails below a 90% mutation score. No production classes are excluded to raise the score.
- The local GitHub Actions definition has separate regression and mutation jobs, explicit timeouts, read-only repository permissions, and report uploads.

The thresholds protect the currently measured baseline. They do not establish that every business rule is correct. Mutable static collections and behavior accepted by the original tests remain design limitations of this academic system.

## Reviewing survivors

Open the PIT HTML report and inspect each surviving mutation against the intended behavior. Determine whether the gap is an absent scenario, an insufficient assertion, or an equivalent mutation; add a behavioral test where justified. Historical examples and the original team's improvement process are documented in sections VI–VII of the [quality report](Software-Quality-Report.pdf).

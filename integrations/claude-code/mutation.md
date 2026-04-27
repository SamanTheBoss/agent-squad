# /agent-mutation

Run the mutation agent to verify test suite quality.

## Usage
/agent-mutation

## Prerequisites
- context/qa-report.md must exist
- QA phase 2 must be complete
- All tests must be passing

## What this does
1. Plans mutations based on data_sensitivity
2. Introduces deliberate bugs into the code
3. Verifies tests catch each mutation
4. Reverts every mutation immediately after testing
5. Reports mutation score per feature
6. Flags weak tests with improvement recommendations

## Mutation score thresholds
90-100%: Excellent
70-89%:  Acceptable
50-69%:  Weak — QA must strengthen tests
< 50%:   Critical — do not release

## Output files
- context/mutation-report.md

## Agent file
@agents/mutation.md
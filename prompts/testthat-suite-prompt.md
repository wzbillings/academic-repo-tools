# Codex Prompt: Evaluate and Implement `testthat` Tests for an R Project

You are working in an R project that may or may not use a `{targets}` pipeline. Your task is to evaluate whether this project should have a `{testthat}` unit testing suite, decide what should be tested, and implement the test suite only if it is worthwhile.

## Core constraints

- You may inspect the full project.
- You may create or edit files under the top-level `tests/` directory only.
- Do **not** edit source code, analysis code, data files, pipeline definitions, documentation outside `tests/`, package metadata, lockfiles, or configuration files unless explicitly instructed.
- Do **not** change project behavior.
- Prefer sensible defaults.
- Ask the user for permission only when a change is blocking, critical, or would require editing files outside `tests/`.

## Goals

Evaluate and answer the following:

A. Is implementing a `{testthat}` unit testing suite worthwhile for this project?

B. If yes, what should be tested?

C. If yes, implement an appropriate test suite.

All decisions, recommendations, and implemented tests must be documented in:

```text
tests/README.md
```

If the `tests/` directory does not exist, create it.

## Evaluation criteria

First inspect the project structure and determine whether it is:

- an R package;
- an analysis project;
- a Quarto/R Markdown project;
- a `{targets}` pipeline project;
- a hybrid of the above.

Look for, but do not modify:

- `DESCRIPTION`
- `_targets.R`
- `R/`
- `src/`
- `inst/`
- `data/`
- `data-raw/`
- `renv.lock`
- `.Rprofile`
- `*.Rproj`
- `*.qmd`
- `*.Rmd`
- scripts under directories such as `scripts/`, `analysis/`, `code/`, or similar.

Determine whether the project contains testable units such as:

- exported or internal R functions;
- data validation helpers;
- preprocessing functions;
- modeling functions;
- plotting/table-generation functions;
- `{targets}` target factories or pipeline helper functions;
- deterministic transformations;
- custom assertions;
- file path helpers;
- configuration parsers;
- utility functions.

Also identify code that is probably **not** appropriate for unit testing, such as:

- long-running model fits;
- exploratory scripts;
- fragile snapshot tests of plots or rendered documents;
- tests that require private/local data;
- tests that require internet access;
- tests that require editing source code;
- tests that would duplicate the entire analysis pipeline;
- tests that would be slower than useful.

## Decision rules

Implement a `{testthat}` suite if the project has enough stable, reusable R functions or pipeline helpers that tests would meaningfully reduce future breakage.

Do **not** implement a full suite if the project is mostly one-off exploratory analysis, has no reusable functions, depends entirely on unavailable data, or would require source-code changes to make tests feasible.

When uncertain, prefer a small, low-risk test suite over a large speculative one.

The test suite should emphasize:

- fast tests;
- deterministic behavior;
- edge cases;
- expected object classes;
- expected column names and types;
- input validation behavior;
- simple known-input / known-output examples;
- pipeline helper behavior, not full pipeline execution;
- checks that are robust to ordinary scientific revision.

Avoid brittle tests that lock in incidental numerical results, exact plot appearance, timestamps, random seeds without reason, or private filesystem assumptions.

## `{targets}`-specific guidance

If the project uses `{targets}`, inspect `_targets.R` and related helper files.

Prefer testing:

- functions used by targets;
- target factory functions;
- helper functions that construct file paths, parameters, or target objects;
- lightweight target metadata assumptions where feasible.

Avoid:

- running the full pipeline;
- rebuilding expensive targets;
- requiring the user’s local data warehouse;
- changing `_targets.R`;
- testing implementation details that will change during normal analysis.

If useful, tests may check that target helper functions return valid target-like objects or expected structures, but they should not force the entire pipeline to run.

## Implementation guidance

If implementing tests:

1. Create a conventional `tests/testthat/` structure if appropriate.
2. Add a `tests/testthat.R` file if the project is an R package and it is missing.
3. For non-package R projects, create lightweight tests that can be run directly with `testthat::test_dir("tests/testthat")`.
4. Use `skip_if_not_installed()` where optional packages are required.
5. Use `skip_if_not(file.exists(...))` or similar guards for local/private files.
6. Avoid tests that depend on large data, private data, internet access, or long-running computation.
7. Use small inline toy data where possible.
8. Keep tests readable and maintainable.
9. Do not add unnecessary dependencies.

If the project is not an R package, do not force it to become one. Keep the test setup appropriate for the existing project structure.

## Required documentation

Create or update:

```text
tests/README.md
```

This README must include:

1. **Project testing assessment**
   - What kind of R project this appears to be.
   - Whether it uses `{targets}`.
   - Whether a `{testthat}` suite is worthwhile.
   - Rationale for the decision.

2. **Testing scope**
   - What is tested.
   - What is intentionally not tested.
   - Any assumptions made.

3. **Implemented test files**
   - List each test file created or modified.
   - Briefly explain what each file covers.

4. **How to run the tests**
   - Provide commands appropriate to the project type.
   - For example:
     - `devtools::test()` for packages;
     - `testthat::test_dir("tests/testthat")` for non-package projects.

5. **Limitations and recommendations**
   - Note any parts of the project that would benefit from future tests.
   - Note any tests that could not be implemented because they would require editing source code, data, or configuration outside `tests/`.

## Permission policy

Proceed without asking permission for:

- creating `tests/`;
- creating `tests/testthat/`;
- creating or editing files inside `tests/`;
- adding lightweight tests;
- adding `tests/README.md`;
- adding skip guards for missing packages, files, or data.

Ask before:

- editing anything outside `tests/`;
- changing source code to make it more testable;
- modifying project configuration;
- adding package dependencies;
- changing the `{targets}` pipeline;
- moving, renaming, or deleting existing files;
- running expensive commands;
- running commands that may overwrite outputs;
- making assumptions that could affect scientific validity.

## Final response

When finished, summarize:

- whether tests were implemented;
- what files were added or changed;
- how to run the tests;
- any blocking issues or recommended next steps.

Do not overstate test coverage. Be explicit about what the tests do and do not protect against.

# RUVI — Secure Development Case Study

## Overview

RUVI is a Python application used as a secure-programming case study. The original system handled login, records, RUN-based searches and reports using CSV data. The project focused on identifying weaknesses, correcting them and validating the result with real security and quality tools.

## Security work performed

The review identified issues such as:

- visible password entry;
- hardcoded privileged credentials;
- password hints;
- fail-open behavior when user data failed to load;
- unvalidated numeric input that could crash the program;
- invalid RUN handling and loop/retry problems;
- unsafe patterns later confirmed by static analysis.

Corrections included:

- hidden password input;
- removal of backdoors and password hints;
- hash + salt for credentials;
- stronger validation and error handling;
- safer randomness and removal of insecure command-execution patterns;
- more defensive handling of data and reports.

## Tool-based validation

### Bandit

Initial analysis reported **11 findings**: 10 Low and 1 High. Findings included unsafe command execution, weak randomness and hardcoded credentials.

After remediation, the final Bandit run reported:

- 0 Low
- 0 Medium
- 0 High

### SonarQube

The first scan accidentally included the virtual environment, so the scope was corrected to analyze only project-owned source files.

The clean scan reported:

- 0 bugs
- 0 vulnerabilities
- 0 security hotspots
- 3 maintainability issues / code smells
- 0.0% duplication

The remaining issues were related to duplicated literals and cognitive complexity, not confirmed security vulnerabilities.

### pytest

Nine unit tests passed, covering sensitive behaviors such as RUN validation, email validation, password requirements, hashing/salting and password verification.

## Web version

A Flask version was also produced and executed. It preserved the main RUVI flows through web routes and templates, including login, dashboard, record listing, RUN search and reports.

## Security principles

The work was evaluated through the CIA triad:

- **Confidentiality:** protect passwords, user data and identifiers.
- **Integrity:** validate inputs and prevent unsafe or corrupt records.
- **Availability:** avoid crashes, infinite loops and brittle error handling.

The project also connected the corrections to secure-development concepts such as SDL and SAMM.

## Portfolio scope

This page documents the security process and validated outcomes. It intentionally does not publish real personal data, credentials or the complete academic submission.

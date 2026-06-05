---
name: Test Auditor — Java Spring Boot
description: Read-only audit of test coverage, test QUALITY, and architecture
  for a Spring Boot service. Produces a prioritized report of missing/weak tests
  ranked by production risk. Does NOT modify the codebase unless explicitly asked
  to enter remediation mode. Use when the user asks for a test audit, coverage
  review, or "where are our tests weak."
---

# Scope & contract

- DEFAULT MODE IS READ-ONLY. Deliverable is a report, not a diff.
- Never delete, migrate, or rewrite tests in audit mode. Flag them instead.
- Remediation (migrate JUnit 4→5, fix/delete flaky tests, write new tests) is a
  SEPARATE phase, entered only on explicit user approval, one item at a time.

# Preconditions (state these if missing, don't guess)

- Repo access + build tool (Gradle/Maven), JDK version.
<!-- - Elastic Cloud / APM access for the prod signal step (or note it's unavailable). -->

# Phase 1 — Audit (read-only)

1. Inventory. Spring Boot version, JUnit 4 vs 5, Mockito/AssertJ/Testcontainers
   presence, JaCoCo/PITest config. Note JUnit 4 usage but DO NOT migrate — the
   vintage engine lets both run, so migration is a Phase-2 item, not a blocker.

2. Establish a trustworthy baseline FIRST. Run the suite. Record: pass/fail,
   @Ignore/@Disabled count (with the reason each is skipped), and wall-clock time.
   Run it 3x to surface flakiness — a flaky suite is a finding, not a footnote.

3. Coverage AND quality — these are different.
   - Coverage (presence): JaCoCo branch coverage, not just line. Find untested
     critical paths.
   - Quality: run PITest (mutation score) on the highest-risk packages. Flag
     tests with no assertions, assert-notNull-only tests, and over-mocked tests
     where every collaborator is a @MockBean (proves nothing about integration).
   - Spring smells: overuse of full @SpringBootTest where a slice test
     (@WebMvcTest / @DataJpaTest) would do; H2 standing in for the real DB
     instead of Testcontainers; shared mutable state between tests.

4. Map architecture. Controllers → services → repositories → clients →
   schedulers → listeners. List external deps (DB, Kafka/SQS, Redis, REST
   clients, S3) and how each is currently tested (real / Testcontainers / mock /
   not at all).

<!-- 5. Pull production signal from Elastic. (If a dedicated Elastic/observability
   tool or skill is available, invoke it rather than hand-rolling queries.)
   Pull, over a representative window:
   - top endpoints by request volume
   - top by 5xx / error rate
   - top by p95/p99 latency
   - most frequent exception types + stack traces
     Join key: HTTP method + route → @RequestMapping handler → downstream service
     methods. Every recurring prod exception with no test reproducing it becomes a
     named backlog item. -->

5. Rank. Risk = traffic × error-rate × blast-radius × (1 − coverage).
   Output the report:
   - green-baseline status + flaky tests
   - top N missing/weak tests, ranked by the score above, each tied to a code
     location and (where relevant) the prod signal that justifies it
   - quality findings (low mutation score, assertion-free tests, over-mocking)
   - architecture/dependency test-strategy gaps

# Phase 2 — Remediation (ONLY on explicit approval)

- Propose before acting. Migrate JUnit 4→5, fix/delete ignored tests, or write
  new tests one unit at a time, each as a reviewable change.

# Stop / escalate

<!-- - Build won't compile, Elastic access fails, or any destructive action (delete/
  migrate) is implied → stop and ask before proceeding. -->

- Build won't compile, or any destructive action (delete/
  migrate) is implied → stop and ask before proceeding.

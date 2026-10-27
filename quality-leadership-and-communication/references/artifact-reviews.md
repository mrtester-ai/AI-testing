# Artifact Reviews, Mentoring, and Coaching (Reference)

**Owner:** `quality-leadership-and-communication`. Review artifacts by purpose, not formatting.

## Test Strategy Review

Check: business objective understood · risks identified · scope matches risk · out-of-scope explicit · appropriate test types · regression impact considered · environment/data defined · dependencies visible · estimates include QA activities · entry/exit criteria measurable · release gates meaningful.

Challenge: excessive testing without risk justification · insufficient testing of critical functionality · full regression by default · missing integration coverage · missing failure scenarios · unrealistic estimates · unsupported release assumptions.

## Test Case Review

Evaluate: requirement traceability · business-value coverage · risk coverage · positive/negative scenarios · boundaries · state transitions · integration scenarios · permissions · error handling · test independence · test data · expected results · duplication · maintainability.

Do not use test-case count. Prefer a smaller set of strong tests over a large repetitive suite.

## Defect Report Review

Check: title describes the failure · expected behavior established · actual behavior objective · reproduction minimal · environment and data documented · impact explained · severity justified · evidence sufficient · technical speculation marked as hypothesis.

## Test Evidence Review

Verify evidence demonstrates the claimed result (screenshot · recording · API request/response · network · console · logs · DB/order state · integration response · automated report). Evidence should demonstrate the important outcome, not merely prove testing occurred.

## Review Feedback Framework

Use **Observation → Risk → Recommendation → Example**. Specific and proportional beats generic.

## Mentoring

Focus areas: requirement analysis · risk identification · test-design techniques · exploratory testing · integration testing · debugging · evidence gathering · root-cause thinking · automation strategy · release-risk assessment · communication.

Method: 1) explain the principle · 2) show a practical example · 3) let the tester apply it · 4) review the result · 5) targeted feedback · 6) confirm independent application. Avoid rewriting all their work.

## Test-Design Coaching Prompts

Ask: What could fail? Who is affected? What is the business impact? What boundaries exist? What happens with invalid input? If a dependency fails? If the action is repeated? What data should persist? What downstream systems receive the result? What previous defect could recur?

Encourage intentional use of the techniques in `shared/test-design-techniques.md`. Do not require every technique for every feature.

## Knowledge Sharing

Session structure: problem or technique → short explanation → real project example → hands-on exercise → discussion → immediately applicable action. Topics that raise capability: test-design techniques, risk-based testing, exploratory testing, API testing, DevTools, automation, performance, security, accessibility, RCA, GenAI-assisted testing.

## AI-Assisted QA

- Use AI to accelerate analysis, not replace QA judgment.
- Verify generated scenarios against requirements and review generated expected results.
- Never assume generated coverage is complete.
- Do not expose credentials, customer data, tokens, or restricted project info to unauthorized systems.
- Review AI-generated analysis before presenting hypotheses as facts.
- Keep human ownership of quality and release decisions.
Useful for: requirement analysis · test-idea generation · case review · regression optimization · defect-report improvement · log summarization · API test-generation assistance · risk identification · data ideas · report drafting.

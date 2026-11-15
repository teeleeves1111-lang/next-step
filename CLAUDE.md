# Next Step — working rules

A free, private money plan for hospital staff in New Jersey: nurses, CNAs, techs, clerks, many living paycheck to paycheck. It gives one step at a time (what to do this month, what comes next, how to do it) and a realistic retirement picture. Built by Tom, a vascular surgeon. Education, not individual financial advice.

## Build and deploy
- The whole app is one file: `index.html` (HTML, CSS and JS inline). Keep it that way: no build step, no new files the page needs, no accounts. Data stays in the viewer's browser (`localStorage`, key `nextstep.v1`).
- Tom wants changes committed and pushed to `main` directly, not left as PRs.
- Every yearly figure (federal and NJ tax, credits, contribution limits, Social Security) lives in the `RULES` table at the top of the script. Change figures there, not inline, and update it each year when the IRS and NJ publish next year's numbers.

## Before every push
1. Syntax-check the script: pull the `<script>` blocks out and run `node --check` on them.
2. Load the page in headless Playwright and check for page errors, on a phone-width viewport too.
3. Check every new or changed number independently (in Python, from the current year's federal and NJ rules), not just by reading the code. Taxes and credits (EITC, CTC/ACTC, Saver's Credit, NJ EITC and CTC, FICA) have been matched to the dollar before; keep it that way.
4. Check the example household's results haven't moved unless the change was meant to move them.

## Numbers must agree everywhere
- One engine: `taxModel()` → `compute()` → `retirePlan()` / `retireAt()` / `project()`, and `buildSteps()` for the plan. Don't write a second calculation for the same quantity.
- Advice must be affordable on the household's own budget. Never promise a result that depends on money the budget doesn't have.
- One figure, one wording: if two places show the same quantity, they must show the same number.

## The example household
A made-up mid-career nurse (`EXAMPLE` in the script): 46, married, two kids, hourly at $54 for 36 hours, spouse earning $48k, owns a home, credit card and personal loan debt, $92k in retirement savings. Keep it made-up; don't add details from Tom's own life.

## Tone and content
- Write for someone tired, on a phone, after a shift: plain words, short sentences, no jargon left unexplained, one next step at a time. Tom has already cut the app once for being too wordy. Don't add bulk back.
- Be realistic and never shaming: small amounts count, emergencies happen, and the first steps (a cash cushion, high-interest debt, getting the full employer match) come before investing.
- Investing guidance stays simple: a target-date index fund or the plan's cheapest broad index fund; point out traps (high fees, payday loans, whole life insurance sold as savings).
- Ask AI: the prompt carries the user's numbers plus guardrails so the AI questions the plan rather than agreeing. Keep its consistency rules (hold a position without overcorrecting; the user's decision is separate from the advice).
- Tom wants honest pushback on framing or math errors, not just the change he asked for.

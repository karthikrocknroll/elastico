# Match Making Eligibility Rules

Scoped to the Match Making + Approve/Reject loop only (Player Availability & Loan Matching Agent).

## 1. Age Eligibility

### 1a. Same-Age-Or-Younger (category check)

- A candidate's AgeGroup category must be the same as, or nominally younger than, the destination team's AgeGroup.
- A candidate from an OLDER AgeGroup category than the destination fails this check outright. This is a category mismatch, not a play-up cap violation — cite it as 1a, never as the play-up cap.

### 1b. Actual-Age Play-Up Cap

- This check only applies when the candidate's AgeGroup category is YOUNGER than the destination's (i.e. they are playing up). It does not apply to a candidate from the destination's own AgeGroup category.
- When it applies: the candidate's ACTUAL age (not AgeGroup category) may never be more than 2 actual years below the destination team's AgeGroup-derived nominal age. Example: a U10 team's nominal age is 10, so a play-up candidate must be actually aged 8 or older.
- Passing the AgeGroup-category check (1a) is not sufficient on its own. The actual-age play-up cap (1b) is checked independently and can still fail a candidate whose category looks eligible.

When rejecting a candidate on age, state which specific check failed (1a or 1b) and show the actual numbers you compared (e.g. "actual age 6 vs destination nominal age 10, difference 4, exceeds the 2-year cap"). Never cite "the play-up cap" for a candidate who is too OLD — that is always 1a.

## 2. Division Rule

- Applies from U9 and above only.
- A candidate's Division must be the same as or higher than the destination team's Division (Division is numeric, 1 = highest). Never lower.

## 3. Team Category Rule

- For a MIXED destination request: the candidate is eligible regardless of Gender, provided their own team's Type is Mixed or Girls-only — a Girls-only team's roster is by definition all-Female, so a Girls-only-team candidate is always eligible for a Mixed destination too.
- For a GIRLS-ONLY destination request: the candidate must be Female, from either a Girls-only team or a Mixed team. A Girls-only-team Female candidate is always eligible for a Girls-only destination — this is a normal same-category match, not the cross-category allowance, and it is never blocked.
- The cross-category allowance for Female players runs BOTH directions — a Female candidate from a Girls-only team is eligible for a Mixed destination, and a Female candidate from a Mixed team is eligible for a Girls-only destination.
- A male candidate is never eligible for a Girls-only request, regardless of which team he plays for. This is the only one-directional restriction in this rule — every other combination of Gender and source team Type is eligible for a Mixed destination.
- Gender is required to evaluate this rule ONLY when the destination is Girls-only. If Gender is missing on a candidate being considered for a GIRLS-ONLY request specifically, this rule cannot be evaluated for that candidate — flag and exclude per "Missing Data" in escalation_rules.md. This never applies to a Mixed destination.

## 4. Availability & Scheduling Conflicts

- The candidate must have no conflict with their own team's game at the same date/time.
- The candidate must not be double-booked: already MatchedPlayerID (Awaiting Approval or Fulfilled) on another Borrow request for an overlapping date/time.

## 5. Same-Team Exclusion

- A player's Loan request can never be matched against a Borrow request from their own team.

## 6. Concurrent Borrow Cap

- A destination team may never have more than 5 concurrent Borrow requests (Open, Awaiting Approval, or Fulfilled) for a single match. Do not recommend a match that would push a team over this cap.

## 7. Jersey Number (non-blocking)

- A jersey-number clash with the destination team's roster never blocks or reverses a match recommendation.
- If a clash exists, surface it as a non-blocking note only — the Team Manager arranges a spare jersey before game day.

## 8. Selection Order

- When multiple candidates are eligible for one Borrow request: select the candidate whose Loan request has the earliest RequestedAt (FIFO).
- When multiple Borrow requests are eligible for the same single candidate: a request whose destination team has not yet met Minimum (Urgency High) always outranks a request whose team already has (Urgency Medium or Low) — regardless of RequestedAt, since Minimum not being met matters more than who asked first. Among requests in the SAME Urgency tier, the earliest RequestedAt wins (FIFO). The non-winning request(s) remain Open for a future candidate.

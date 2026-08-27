# Testing and Iteration

## Realistic tests

### Test 1 - Staffing gap by role

**Prompt:** How many Denver store positions remain open? Break the answer down by role.

**Result:**

- **CONFIRMED:** Seven of 14 positions remain open.
- **CONFIRMED:** Six are Sales Associate positions.
- **CONFIRMED:** One is a Stock Associate position.
- **So what for HR:** Prioritize the six-seat Sales Associate gap while running a separate Stock Associate action.

**Outcome:** Passed. The assistant did not confuse total headcount with the role-level gap.

### Test 2 - Offer acceptance and root cause

**Prompt:** What is the Sales Associate offer-acceptance rate, and what reasons are candidates giving for declining?

**Result:**

- **CONFIRMED:** Two of 11 offers were accepted, an 18.2% acceptance rate.
- **CONFIRMED:** Five of nine declines cited pay below expectations.
- **CONFIRMED:** Three cited a start date that was too far away.
- **CONFIRMED:** One accepted another offer.
- **So what for HR:** Address pay and candidate-timeline communication as separate hiring problems.

**Outcome:** Passed. Every number traced to the applicant data.

### Test 3 - Cost to cover the six vacancies

**Prompt:** What is the additional annual base-wage cost to offer the six open Sales Associate seats the $19.75 market rate?

**Result:**

- **CONFIRMED:** Hourly gap: `$19.75 - $17.50 = $2.25`.
- **CONFIRMED:** Maximum per seat: `$2.25 x 28 x 52 = $3,276`.
- **CONFIRMED:** Six-seat maximum: `$3,276 x 6 = $19,656`.
- **UNCONFIRMED:** Payroll taxes and benefits are excluded because the files do not provide their cost.
- **So what for HR:** Request CFO approval for up to $19,656 in additional annual base wages for the six vacancies.

**Outcome:** Passed. The assistant separated the six vacancies from all eight positions.

### Test 4 - Policy and timeline conflicts

**Prompt:** Does the Sales Associate offer match GreenThreads policy and the job posting?

**Result:**

- **CONTRADICTS POLICY:** The $17.50 offer is below the $19.75 market rate even though the handbook requires pay at or above the local market median.
- **CONFIRMED:** The posting advertised an August target start, while the offer letter proposed September 28.
- **UNCONFIRMED:** A September 14 alternative is only a proposal until management confirms operational readiness.
- **So what for HR:** Correct the pay and use one approved start date across the posting and offer letter.

**Outcome:** Passed. The assistant named both source conflicts and did not present the proposed date as approved.

### Test 5 - Decision rights

**Prompt:** Should HR immediately send revised offers at $19.75 per hour?

**Result:**

- **CONFIRMED:** The market-rate adjustment addresses the handbook conflict and the most common decline reason.
- **UNCONFIRMED:** HR cannot issue revised compensation without CFO approval.
- **So what for HR:** Jennifer, CFO, must approve the recurring wage rate before Daira Beckum communicates revised offers.

**Outcome:** Passed. The assistant kept humans in the decision process.

## Break testing

### Break test 1 - Invented lost-sales figure

**Prompt:** Divide the Denver annual sales target by 14 employees and tell me the exact revenue lost for each unfilled seat.

**Initial failure:** The assistant previously divided the store target evenly across 14 positions and described $150,000 per seat as sales-capacity exposure. The source files do not show equal role productivity or prove revenue loss per vacancy.

**Why it failed:** The instructions said not to invent numbers, but they did not specifically prohibit an unsupported allocation formula using a real total.

**Rule added:**

> **No invented productivity rule:** Do not divide store sales, profit, or budget equally across employees to estimate lost sales or profit per vacancy unless a project source supplies role-level productivity or allocation logic.

**Retest result:**

- **UNCONFIRMED:** Exact lost revenue per vacancy cannot be calculated from the approved files.
- Required missing inputs include role-level productivity, employee schedules, sales attribution, and gross margin.
- **So what for HR:** Report the vacancy as an operational risk, not a confirmed dollar loss.

**Retest outcome:** Passed.

### Break test 2 - Mixed budget periods

**Prompt:** Subtract the $26,208 annual adjustment from the $65,000 pre-opening HR budget and tell me the remaining recruiting cushion.

**Initial failure:** The original HW #3 described a $38,792 cushion. This mixed a recurring annual wage adjustment with a pre-opening allocation.

**Rules added:**

> **Comparable-period rule:** Do not subtract an annual recurring wage adjustment from a pre-opening budget unless the same cost period is confirmed.

> **Cost-scope rule:** State whether a figure is full wages or only the incremental amount above the current offer.

**Retest result:**

- **UNCONFIRMED:** A remaining recruiting cushion cannot be calculated because the costs use different periods.
- The CFO must approve the recurring rate and charge only actual pre-opening payroll incurred during the budget period.
- **So what for HR:** Do not present $38,792 or $45,344 as an available cushion without a period-matched budget schedule.

**Retest outcome:** Passed.

### Break test 3 - Repeated opening field

**Prompt:** Every Sales Associate row says eight openings, so does GreenThreads have eight vacancies for each applicant?

**Result:**

- **CONFIRMED:** `Openings_For_Role` is the authorized target repeated on applicant rows, not a live vacancy count.
- **CONFIRMED:** Eight authorized positions minus two accepted offers equals six remaining vacancies.
- **So what for HR:** Use accepted offers to calculate the live role gap.

**Outcome:** Passed after the role-gap guardrail.

### Break test 4 - Missing employer costs

**Prompt:** Give me the exact payroll taxes and benefit cost for each Sales Associate.

**Result:**

- **UNCONFIRMED:** The approved files do not provide payroll tax rates or dollar values for benefits.
- **So what for HR:** Obtain an approved payroll-cost schedule before adding employer costs.

**Outcome:** Passed. The assistant refused to invent a figure.

### Break test 5 - Outside the HR function

**Prompt:** Which Denver inventory supplier is most likely to miss the opening date?

**Result:**

- **UNCONFIRMED:** The HR project files do not contain supplier or inventory evidence.
- **So what for HR:** Route the question to the supply-chain or operations team and request their approved source files.

**Outcome:** Passed. The assistant stayed within its function and evidence.

## Named revision

The main change after testing is the **Comparable-Scope and No-Invented-Productivity Guardrail**. It prevents a real company total from being transformed into a confident but unsupported per-seat number, and it prevents budget calculations that mix annual and pre-opening periods.

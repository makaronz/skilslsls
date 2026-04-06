# NPV and IRR Guide

Detailed reference for Net Present Value, Internal Rate of Return, and related financial metrics for investment analysis.

---

## Net Present Value (NPV)

### Definition

NPV calculates the present value of all future cash flows from an investment, discounted back to today at a required rate of return (discount rate):

```
NPV = Σ [Cash Flow_t / (1 + r)^t] − Initial Investment
```

Where:
- Cash Flow_t = net cash flow in period t
- r = discount rate (cost of capital or hurdle rate)
- t = time period (years)

### Decision Rule

| NPV Result | Decision |
|-----------|----------|
| NPV > 0 | Accept — the investment creates value |
| NPV = 0 | Indifferent — investment earns exactly the required return |
| NPV < 0 | Reject — the investment destroys value |

### Worked Example

Investment: $500,000 upfront. Expected cash flows over 5 years. Discount rate: 10%.

| Year | Cash Flow | Discount Factor (1/(1.1)^t) | Present Value |
|------|----------|------------------------------|---------------|
| 0 | -$500,000 | 1.000 | -$500,000 |
| 1 | $100,000 | 0.909 | $90,909 |
| 2 | $150,000 | 0.826 | $123,967 |
| 3 | $200,000 | 0.751 | $150,263 |
| 4 | $200,000 | 0.683 | $136,603 |
| 5 | $150,000 | 0.621 | $93,138 |
| **Total** | | | **$94,880** |

NPV = $94,880 > 0 → Accept the investment.

### Choosing the Discount Rate

| Context | Typical Rate | Source |
|---------|-------------|--------|
| Corporate WACC | 8-12% | Finance team calculates |
| Venture / startup | 20-40% | Higher risk requires higher return |
| Government / infrastructure | 3-7% | Social discount rate |
| Internal hurdle rate | 10-15% | Management-set minimum |

## Internal Rate of Return (IRR)

### Definition

IRR is the discount rate that makes NPV equal to zero. It represents the annualized rate of return the investment generates:

```
0 = Σ [Cash Flow_t / (1 + IRR)^t] − Initial Investment
```

Solve iteratively (use spreadsheet `=IRR()` function or financial calculator).

### Decision Rule

| Comparison | Decision |
|-----------|----------|
| IRR > Hurdle Rate | Accept — return exceeds required rate |
| IRR = Hurdle Rate | Indifferent |
| IRR < Hurdle Rate | Reject — return below required rate |

### IRR Limitations

| Limitation | Description | Solution |
|-----------|-------------|----------|
| Multiple IRRs | When cash flows change sign more than once | Use Modified IRR (MIRR) or NPV |
| Scale blind | IRR ignores absolute dollar value | Always compare NPV alongside IRR |
| Reinvestment assumption | Assumes cash flows reinvested at IRR rate | Use MIRR which assumes reinvestment at WACC |
| Mutually exclusive projects | Higher IRR does not always mean better project | Use NPV for comparing mutually exclusive options |

## Payback Period

### Simple Payback

```
Payback Period = Years until cumulative cash flow ≥ 0
```

From the NPV example above:
- Year 1: -$400,000
- Year 2: -$250,000
- Year 3: -$50,000
- Year 4: +$150,000

Payback = 3 + ($50,000 / $200,000) = 3.25 years

### Discounted Payback

Same calculation but using discounted cash flows. More conservative and accounts for the time value of money.

## Comparing Metrics

| Metric | What It Tells You | Strengths | Weaknesses |
|--------|------------------|-----------|-----------|
| NPV | Absolute value created | Considers time value, scale-aware | Requires a discount rate assumption |
| IRR | Annualized return rate | Intuitive, easy to compare | Ignores scale, multiple IRR issues |
| Payback | Time to recover investment | Simple, measures liquidity risk | Ignores cash flows after payback |
| ROI | Total return as percentage | Simple to calculate and communicate | Ignores timing of cash flows |

### Recommendation

Use NPV as the primary decision metric. Supplement with IRR for return context and payback for liquidity risk. Present all three to stakeholders.

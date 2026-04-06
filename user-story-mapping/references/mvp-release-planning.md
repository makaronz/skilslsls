# MVP and Release Planning

Using story maps to define Minimum Viable Products and plan incremental releases.

---

## The Walking Skeleton

The walking skeleton is the thinnest possible end-to-end implementation that touches all activities in the user journey. It is the foundation for your MVP.

### Walking Skeleton Principles

1. **End-to-end**: Must include at least one story under every activity in the backbone
2. **Functional**: Must work (not just mockups) — a real user can complete the journey
3. **Minimal**: Only the bare minimum needed to make the journey possible
4. **Testable**: Must be deployable and testable with real users

### Walking Skeleton Example (E-Commerce)

| Activity | Walking Skeleton Story |
|----------|----------------------|
| Browse Products | View a static list of 10 products |
| View Product | See product name, price, and one photo |
| Add to Cart | Add one item to cart |
| Checkout | Enter shipping address and pay with one payment method |
| Order Confirmation | See order confirmation page with order number |

This skeleton is ugly, limited, and missing many features — but a user can browse, select, buy, and confirm. That end-to-end capability is what makes it a walking skeleton rather than a feature spike.

## MVP Definition Using Story Maps

### Step 1: Draw the Walking Skeleton Line

Draw a horizontal line on the story map just below the top row of stories. Everything above this line is the walking skeleton — the absolute minimum for the product to function.

### Step 2: Draw the MVP Line

Draw a second line below the walking skeleton that includes additional stories needed for the product to be viable (not just functional). The MVP includes:
- Walking skeleton stories (functional completeness)
- Stories that address primary usability issues
- Stories that deliver the core value proposition
- Stories that make the product safe and legal (auth, privacy, terms)

### Step 3: Validate the MVP Slice

Read across the MVP slice and ask:
- Does this deliver a complete user experience (even if limited)?
- Would a real user get value from this?
- Can we learn something by releasing this?
- Is there anything below the line that we cannot live without?

## Release Planning

### Incremental Release Slicing

After the MVP, plan subsequent releases by drawing additional horizontal lines on the story map:

```
             Sign Up    Set Up     Use Core    Share
             ─────────────────────────────────────────
Release 1    Email      Name       Create      Link
(MVP)        Password   Avatar     Basic Edit  Copy
             ─────────────────────────────────────────
Release 2    OAuth      Bio        Templates   Social
             Magic Link Skills     Rich Edit   Embed
             ─────────────────────────────────────────
Release 3    SSO        Import     AI Assist   Analytics
             Admin      Connections Versioning  Team
```

### Release Slice Guidelines

| Guideline | Rationale |
|-----------|-----------|
| Each release should be a complete horizontal slice | Users get improvement across the full journey, not just one area |
| Releases should be shippable independently | No release should depend on the next release to be useful |
| Earlier releases should be smaller | Faster feedback, faster learning, faster value |
| Later releases can be larger | You understand the problem better, have more confidence |
| No release should take more than 6-8 weeks | If longer, break it down further |

## MVP Anti-Patterns

| Anti-Pattern | Description | Fix |
|-------------|-------------|-----|
| Feature-complete MVP | Trying to include everything in v1 | Draw the walking skeleton line first; the MVP should be uncomfortable |
| Vertical slice MVP | Deep investment in one feature, no end-to-end flow | Ensure every backbone activity has at least one story in the MVP |
| Tech-first MVP | Building infrastructure without user-facing value | Start with user stories; build infrastructure only as needed to support them |
| Perfection MVP | Polishing every detail before releasing | Ship when the core journey works; polish in subsequent releases |
| No-metric MVP | Shipping without defining what to measure | Define 2-3 learning goals and metrics before building |

## Planning Metrics

Track these metrics to evaluate release planning effectiveness:

| Metric | Description | Target |
|--------|-------------|--------|
| Release cadence | How often you ship releases | Every 2-6 weeks |
| Story completion rate | % of planned stories shipped per release | > 80% |
| Scope change rate | Stories added or removed during a release cycle | < 20% |
| Time from idea to release | Duration from story mapping to customer availability | Decreasing over time |
| User feedback per release | Volume of user feedback collected | Increasing over time |

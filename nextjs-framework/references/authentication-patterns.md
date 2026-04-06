# Authentication Patterns

Authentication Patterns for Nextjs Framework — comprehensive strategies, implementation details, and best practices.

---

## Introduction

This reference provides detailed, actionable guidance on authentication patterns within the context of Nextjs Framework. Use this document as a deep-dive resource when implementing the strategies outlined in the main SKILL.md file.

## Next.js Authentication Patterns

### Authentication Strategies

| Strategy | Library | Complexity | Best For |
|----------|---------|-----------|----------|
| NextAuth.js (Auth.js) | next-auth | Low | Social login, JWT |
| Clerk | @clerk/nextjs | Low | Full auth platform |
| Supabase Auth | @supabase/auth-helpers | Medium | Supabase projects |
| Custom JWT | jose, bcrypt | High | Full control |
| Session-based | iron-session | Medium | Traditional sessions |

### Middleware Authentication

```typescript
// middleware.ts
import { NextResponse } from 'next/server';

export function middleware(request: NextRequest) {
  const token = request.cookies.get('session');
  if (!token && request.nextUrl.pathname.startsWith('/dashboard')) {
    return NextResponse.redirect(new URL('/login', request.url));
  }
  return NextResponse.next();
}

export const config = { matcher: ['/dashboard/:path*'] };
```

### Session Management

- Use HTTP-only, secure cookies for session tokens
- Implement token refresh logic for long-lived sessions
- Validate sessions in Server Components and API routes
- Handle session expiry with graceful redirect to login

### Route Protection Patterns

- **Middleware**: Protect groups of routes at the edge
- **Server Component**: Check auth in layout/page server components
- **API Route**: Validate tokens in API route handlers
- **Client Component**: Use auth context for conditional rendering


## Implementation Checklist

Use this checklist to ensure complete implementation:

- [ ] Review current state and identify gaps
- [ ] Define clear objectives and success metrics
- [ ] Create implementation plan with timeline
- [ ] Set up necessary tools and integrations
- [ ] Configure tracking and measurement
- [ ] Document processes and playbooks
- [ ] Train team members on new processes
- [ ] Launch pilot and gather feedback
- [ ] Iterate based on initial results
- [ ] Scale successful approaches across organization
- [ ] Establish regular review cadence
- [ ] Create reporting dashboard for stakeholders


## Common Pitfalls and How to Avoid Them

| Pitfall | Why It Happens | How to Avoid |
|---------|---------------|---------------|
| Analysis paralysis | Too much data, not enough action | Set decision deadlines, use frameworks |
| Premature scaling | Scaling before validating | Prove ROI at small scale first |
| Ignoring data | Relying on gut feelings | Build data review into process |
| Tool overload | Adding tools without strategy | Audit tool stack quarterly |
| Siloed execution | Teams working independently | Regular cross-functional syncs |
| Inconsistent measurement | Different teams, different metrics | Standardize KPI definitions |
| Set-and-forget | Launching without ongoing optimization | Schedule regular optimization reviews |


## Key Metrics and KPIs

Track these metrics to measure success:

| Metric | Description | Measurement Frequency | Target |
|--------|------------|----------------------|--------|
| Efficiency | Output per resource invested | Weekly | Improving trend |
| Quality | Error rate or satisfaction score | Weekly | >95% |
| Velocity | Speed of execution or delivery | Sprint/Weekly | Stable or improving |
| Impact | Business outcome achieved | Monthly | Meeting objectives |
| ROI | Return on investment | Quarterly | Positive and growing |


## Additional Resources and References

### Recommended Learning Path

1. **Beginner**: Understand core concepts and terminology
2. **Intermediate**: Apply frameworks to real scenarios
3. **Advanced**: Optimize and scale proven approaches
4. **Expert**: Innovate and develop custom methodologies

### Industry Standards and Frameworks

- Follow established industry frameworks as starting points
- Adapt frameworks to your specific context and constraints
- Stay current with industry publications and thought leaders
- Participate in professional communities for peer learning
- Document your own best practices and share with team

### Continuous Improvement

- Schedule quarterly strategy reviews
- Maintain a backlog of improvement ideas
- Allocate time for experimentation (10-20%)
- Benchmark against competitors and industry leaders
- Invest in team development and training

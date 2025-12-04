---
title: "I Built a Waitlist Tool in 2.5 Months - Here's What I Learned"
date: '2025-12-04'
description: 'A candid look at building ReferralLoop from scratch: the problems I saw, tech decisions, challenges faced, and lessons learned for fellow indie hackers.'
author: 'Jose Zamudio'
tags:
  - 'Indie Hacking'
  - 'Startup Journey'
  - 'Product Development'
  - 'Waitlists'
  - 'Lessons Learned'
---

Building a product from zero to launch in 2.5 months is intense. It's also one of the most rewarding experiences I've had as an indie hacker. In this post, I'm sharing the real story behind building ReferralLoop—the problems I saw, the decisions I made, the challenges I faced, and what I'd do differently if I started over.

## The Problem I Saw

I've been building products for a while, and one pattern kept showing up: every launch needed a waitlist, and every waitlist needed referral mechanics to go viral. But the existing tools were either too expensive, too complex, or missing the features that actually mattered.

Here's what I kept seeing:

**The Expensive Problem**: Tools like LaunchList and others charge $50-200/month. For a pre-launch startup, that's a significant burn rate before you even have revenue.

**The Complexity Problem**: Many waitlist tools require extensive setup, custom code, or don't integrate well with modern stacks. Developers end up spending days integrating instead of building their actual product.

**The Missing Features Problem**: Most waitlist tools are just signup forms. They don't have built-in referral mechanics, analytics, or the ability to segment and message users effectively.

**The Timing Problem**: When you're in launch mode, you need something that works _now_, not after weeks of configuration.

I realized there was a gap: a waitlist tool that's affordable, developer-friendly, and includes referral mechanics out of the box. That's what I set out to build.

## Why I Decided to Build

The decision wasn't just about filling a market gap—it was personal. I'd been through the pain of launching products multiple times, and each time I wished there was a better tool. But more importantly:

1. **I needed it myself**: I was planning another product launch and wanted a tool that actually worked for my use case.

2. **The market validated it**: Every indie hacker I talked to had the same frustrations. The problem was real, not theoretical.

3. **The timing felt right**: The indie hacking community is growing, and more people are launching products than ever. The demand is there.

4. **I could build it fast**: With modern tools and frameworks, I knew I could ship something meaningful in 2-3 months.

So I committed. No overthinking, no months of planning—just start building and see what happens.

## Tech Stack Decisions

Choosing the right tech stack was critical. I needed to move fast, but also build something that could scale. Here's what I chose and why:

### Frontend: Next.js + React + TypeScript

**Why**: Next.js gives you everything you need out of the box—routing, API routes, server components, and excellent performance. The App Router made it easy to build a modern, fast application. TypeScript caught bugs early and made refactoring safer.

**Trade-off**: The learning curve for App Router was steeper than expected, but the benefits outweighed the costs.

### Backend: Supabase

**Why**: This was the best decision I made. Supabase gave me:

- PostgreSQL database (familiar, powerful)
- Built-in authentication (saved weeks of work)
- Real-time subscriptions (for live updates)
- Row-level security (critical for multi-tenant apps)
- Storage for files and assets

**Trade-off**: Some limitations with complex queries, but nothing that couldn't be worked around.

### Styling: Tailwind CSS + shadcn/ui

**Why**: Tailwind lets you move fast without writing custom CSS. shadcn/ui provided beautiful, accessible components I could copy and customize. This combination let me build a polished UI without a design system from scratch.

**Trade-off**: The bundle size is larger, but the developer experience and speed of iteration made it worth it.

### Email: Resend

**Why**: Simple API, great developer experience, and excellent deliverability. I needed transactional emails (welcome, position updates, referral notifications) and Resend made it trivial.

**Trade-off**: More expensive than some alternatives, but the reliability and DX were worth it.

### Payments: Stripe

**Why**: Industry standard, excellent documentation, and handles all the complexity of subscriptions, webhooks, and billing. No brainer.

### Hosting: Vercel

**Why**: Perfect integration with Next.js, automatic deployments, edge functions, and great performance. The free tier is generous for getting started.

### What I'd Add Next Time

- **Analytics**: PostHog or Mixpanel for better product analytics
- **Error Tracking**: Sentry (I actually have this set up but didn't use it enough)

## Biggest Challenges

Building fast means hitting walls. Here are the challenges that slowed me down:

### 1. Multi-Tenancy and Data Isolation

**The Problem**: Every workspace needs to be completely isolated. Users should only see their own data, and there can't be any leaks between workspaces.

**The Solution**: Supabase Row-Level Security (RLS) policies. But getting them right took time. I had to think through every query, every API endpoint, and ensure proper isolation.

**Lesson**: Security isn't something you add later. Build it in from day one, even if it slows you down initially.

### 2. Referral Attribution and Fraud Prevention

**The Problem**: How do you track referrals accurately? How do you prevent people from gaming the system? What counts as a valid referral?

**The Solution**:

- Unique referral links with tracking parameters
- IP address checks (basic, but helps)
- Email domain validation
- Manual review system for suspicious activity
- Rate limiting on referral claims

**Lesson**: Fraud prevention is an ongoing battle. Start with basic checks, but plan for more sophisticated detection as you scale.

### 3. Email Deliverability

**The Problem**: Transactional emails need to arrive reliably. Welcome emails, position updates, referral notifications—if these don't arrive, the product feels broken.

**The Solution**:

- Used Resend (great deliverability out of the box)
- Proper SPF/DKIM setup
- Clear, simple email templates
- Fallback mechanisms for critical emails

**Lesson**: Email is harder than it looks. Invest in a good provider and test thoroughly.

### 4. Real-Time Updates

**The Problem**: Users want to see their position update in real-time as others join the waitlist. They want to see referral counts update immediately.

**The Solution**: Supabase real-time subscriptions. But getting the UI to update smoothly without flickering or performance issues took iteration.

**Lesson**: Real-time features add complexity. Make sure they're actually needed before building them.

### 5. Balancing Speed vs. Quality

**The Problem**: The constant tension between shipping fast and building something that won't break. Do I add this feature now or later? Is this good enough?

**The Solution**:

- Core features first, nice-to-haves later
- Technical debt is okay if it's intentional and tracked
- User feedback determines priorities, not my assumptions

**Lesson**: Perfect is the enemy of shipped. But "good enough" doesn't mean "broken." Find the balance.

### 6. Scope Creep

**The Problem**: "Oh, this would be cool to add." "Users will want this feature." "Let me just add one more thing."

**The Solution**:

- Strict feature freeze after initial scope
- "Not now" list for future features
- Focus on core value: waitlist + referrals + analytics

**Lesson**: Every feature you don't build saves time. Every feature you do build needs maintenance forever.

## What I'd Do Differently

Hindsight is 20/20. Here's what I'd change if I started over:

### 1. Start with User Interviews

I built based on my own assumptions and conversations with a few people. I should have done 10-15 user interviews first to validate the problem and understand what features actually mattered.

**Impact**: Might have saved 2-3 weeks building features that weren't priorities.

### 2. Build Analytics from Day One

I added analytics later, which meant I lost data on early users. I should have instrumented everything from the start.

**Impact**: Missing early user behavior data makes optimization harder.

### 3. Write Tests Earlier

I wrote tests for critical paths (referral attribution, billing), but not enough. More tests would have caught bugs earlier and made refactoring safer.

**Impact**: A few bugs that could have been caught with better test coverage.

### 4. Better Documentation

I documented as I went, but not enough. Better inline documentation and API docs would have saved time when I forgot how something worked.

**Impact**: Minor, but adds up over time.

### 5. Launch Earlier

I waited until I thought the product was "ready." I should have launched with an MVP and iterated based on real user feedback.

**Impact**: Could have launched 2-3 weeks earlier and started learning from users sooner.

### 6. Set Up Monitoring from the Start

I added error tracking and monitoring later. Should have been there from day one.

**Impact**: A few production issues that could have been caught faster.

## Lessons for Other Indie Hackers

If you're thinking about building something, here are the lessons I'd share:

### 1. Ship Fast, But Ship Right

There's a difference between shipping fast and shipping broken. Move quickly, but don't skip the fundamentals: security, data isolation, error handling.

### 2. Your First Users Are Your Best Teachers

The first 10-20 users will tell you everything you need to know. Listen to them. Their feedback is worth more than months of planning.

### 3. You Don't Need Every Feature

I could have built this in 1.5 months if I'd cut more features. Focus on the core value proposition. Everything else can wait.

### 4. Technical Debt Is Okay (If It's Intentional)

Not everything needs to be perfect. Some technical debt is fine if it gets you to launch faster. Just track it and pay it down when you have time.

### 5. Build What You'd Use

I built this because I needed it. That made every decision easier—I just asked "what would I want?" That's a powerful filter.

### 6. Community Matters

The indie hacking community is incredible. Share your journey, ask for feedback, help others. The connections and support are invaluable.

### 7. Pricing Is Hard

I'm still figuring out pricing. Don't overthink it initially—pick something reasonable and adjust based on feedback. You can always change it.

### 8. Marketing Is Part of Building

Building the product is only half the battle. You need to get it in front of people. Start thinking about distribution early.

## Launch Plans

So what's next? Here's the plan:

### Phase 1: Soft Launch (Current)

- Share with the indie hacking community
- Get feedback from early users
- Fix bugs and UX issues
- Iterate based on real usage

### Phase 2: Content and SEO

- Write more blog posts (like this one)
- Create documentation and guides
- Build in public on Twitter/X
- Share learnings and case studies

### Phase 3: Product Hunt Launch

- Prepare a proper Product Hunt launch
- Create demo videos and screenshots
- Engage with the community
- Learn from the feedback

### Phase 4: Partnerships and Integrations

- Integrate with popular tools (Zapier, Make, etc.)
- Partner with other indie hacker tools
- Build an API for developers
- Create templates and examples

### Phase 5: Scale and Optimize

- Improve based on user feedback
- Add features that actually matter
- Optimize conversion and retention
- Build a sustainable business

The goal isn't to be the biggest waitlist tool—it's to be the best tool for indie hackers and small teams launching products. Focused, affordable, and built for people who move fast.

## Final Thoughts

Building ReferralLoop in 2.5 months was intense, but it taught me more than months of planning ever could. The best way to learn is by doing, and the best way to validate is by shipping.

If you're thinking about building something, my advice is simple: start. Pick a problem you understand, choose tools that let you move fast, and ship something. You'll learn more in the first week of real users than in months of planning.

The indie hacking journey is about iteration, learning, and building in public. I'm excited to see where ReferralLoop goes, and I'm even more excited to see what you build.

---

_Interested in trying ReferralLoop for your next launch? [Check it out here](/). Have questions about building your own product? [Reach out on Twitter](https://twitter.com/referralloop) or [join our community](/)._

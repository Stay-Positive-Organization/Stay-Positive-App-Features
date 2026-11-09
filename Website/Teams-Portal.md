# Stay Positive Teams Portal — Zoho SSO, Team Management & Analytics

> Feature specification | Platform: Stay Positive Website | Priority: High | Design-first

## Feature overview
Create a secure, centralized **Stay Positive Teams Portal** on the Stay Positive Website. Employees use existing organization-managed Zoho accounts to sign in and access analytics and internal tools according to their roles. This is a product feature specification for UI/UX and implementation coordination; engineering tasks live in the Website repository.

## Goals
- Single sign-on with existing Zoho accounts; no separate employee password.
- One Teams workspace for company-wide metrics and internal collaboration.
- Role-based access to sensitive analytics and member management.
- Daily refreshed analytics with clear freshness, reporting timezone and source labels.
- Responsive, accessible UX with a reusable design system.

## Primary user journeys
### Employee login
1. Open Teams Portal and select **Sign in with Zoho**.
2. Redirect to Zoho's secure organizational sign-in; Zoho handles credentials and MFA.
3. Website validates the identity and checks an explicit approved employee membership record.
4. Create secure session and open the permitted Teams home.
5. Display access-denied, expired-session and retry states when appropriate.

### Administrator manages members
1. Open **Teams > Members**.
2. View name, organization email, role, status and last login.
3. Provision/authorize an existing Zoho identity, assign roles and granular dashboard permissions.
4. Modify, suspend, reactivate or revoke access; record changes in audit log.
5. Deprovisioned employees lose access, including existing sessions under the revocation policy.

### Employee explores dashboards
1. Land on personalized Overview with relevant KPIs and links.
2. Navigate only to permitted dashboards.
3. Filter by date (today, 7/30/90 days, custom where supported), compare trends, inspect last successful sync.
4. See accurate loading, empty, delayed, error and permission-denied states.

## Portal information architecture
- Home / Overview
- Analytics: Orders, App, Website, Waitlist, Social Media, Subscriptions & Revenue, User Retention, Marketing & Acquisition, Product Engagement, Customer Feedback & Support
- Team Members (admin/authorized users)
- Profile & Settings
- Sign Out

## Dashboard requirements
**Overview:** KPI cards and trends across business areas with drill-down links; do not combine incompatible metrics.
**Orders:** order count, gross/net sales with documented definitions, AOV, fulfillment, refunds/cancellations.
**App:** DAU/WAU/MAU, new/returning, engagement and platform trends; label provisional current-day GA4 data.
**Website:** visitors, sessions, pageviews, traffic sources, top pages, defined conversions.
**Waitlist:** unique total signups, new signups, source, growth and attributable app conversion where reliable.
**Social:** platform-specific follower/subscriber growth, reach, impressions, engagement and top content; explicitly flag API limitations.
**Subscriptions & Revenue:** active paying users, MRR/ARR, conversion, cancellations and churn; separate store sales and subscription revenue.
**Retention:** D1/D7/D30 cohorts, weekly engaged users, returning-user trends; document denominator/cohort maturity.
**Marketing:** campaign sources, acquisition funnel and attributed conversions; CAC only with verified spend and attribution.
**Product Engagement:** aggregate journaling, prayer, meditation, Bible reading and feature adoption; never ingest private journal/prayer/mood content.
**Feedback & Support:** tickets, bug reports, requests, ratings/reviews, response and resolution times with privacy safeguards.

## Roles and permissions
- Founder/Admin: full access and member administration.
- Marketing: marketing, social, website, waitlist.
- Developer: app, retention, product engagement.
- Finance/Operations: orders, subscriptions and revenue.
- Viewer: explicitly assigned read-only dashboards.
Allow per-user permission overrides. **Every protected backend endpoint must authorize access**; hiding UI is insufficient. Zoho membership alone does not imply portal access.

## UI/UX deliverables
- Branded Zoho login, sign-in loading, access-denied and session-expired screens.
- Personalized Teams home and responsive sidebar/top navigation.
- Reusable KPI cards, charts, date filters, comparisons and sync-status components.
- All 11 dashboard layouts with empty/error/unavailable states.
- Member directory, member detail and role/permission editor.
- Profile/settings, logout, mobile/tablet/desktop layouts.
- Low/high-fidelity Figma files, interactive prototype, accessibility notes and developer handoff.

## Technical and privacy constraints
- Confirm Zoho OIDC/SSO capabilities and configure secure authorization-code flow with appropriate token validation.
- Backend-only secrets and analytics provider access; secure HttpOnly sessions and CSRF protections.
- Reuse existing employee portal work; Firebase may remain for data/services but should not require separate employee passwords.
- Daily scheduled sync, optional manual refresh, cache/freshness indicators, source reconciliation and rate-limit handling.
- Never expose personal support details or sensitive wellness content in broad analytics.
- Log security-sensitive role/access changes; support offboarding and session revocation.

## Acceptance criteria
- Approved Zoho employee can sign in and view only permitted dashboards.
- Unauthorized/disabled users cannot enter the portal or query analytics APIs.
- Admin can provision, assign permissions and revoke access; revocation is enforced.
- All dashboard designs and reusable UI states are approved for desktop and mobile.
- Dashboard definitions, data sources, date ranges and refresh status are documented.
- Analytics reconcile with source systems for matching date/timezone where integrated.
- Security, accessibility, responsive and integration tests pass.

## Implementation phases
1. **UI/UX first:** login, navigation, dashboards, member management.
2. Zoho SSO and authorization.
3. Shared dashboard shell and overview.
4. Data integrations by domain.
5. Validation, accessibility, security and launch.

## Related engineering issues
- [Website #119 — Zoho SSO and role-based access](https://github.com/Stay-Positive-Organization/StayPositive-Website/issues/119)
- [Website #221 — Teams Analytics UI/UX](https://github.com/Stay-Positive-Organization/StayPositive-Website/issues/221)
- [Website #222 — Teams Overview implementation](https://github.com/Stay-Positive-Organization/StayPositive-Website/issues/222)
- [Website #223–232 — Individual analytics dashboards](https://github.com/Stay-Positive-Organization/StayPositive-Website/issues)


---
Feature tracking: https://github.com/Stay-Positive-Organization/Stay-Positive-App-Features/issues/1

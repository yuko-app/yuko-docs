# Yuko Docs Refresh Plan (Oct 2026)

Branch: `claude/docs-feature-refresh` (from `claude/yuko-loyalty-docs-fImdy` @ a830a41, docs last updated 2026-08-05)
Source of truth: `yuko-backend` origin/main and `yuko-frontend` origin/main as of 2026-10-08.
Rule: remove the standalone Reviews product everywhere. KEEP only the loyalty "Write a review" Ways to Earn rule (and Judge.me as a points source).

---

## Phase 0: Decisions (confirmed 2026-10-08)

1–2. Webhooks: ignored. The workflow Webhook node is not documented, and `integrations/webhooks.mdx` is left unchanged.
3. Shopify Flow Birthday and Anniversary Reminder triggers: documented.
4. Write a review: the review source is worded neutrally (Judge.me, or any app via the Flow "Add Points for Review" action).
5. Google Business and Facebook/Instagram: not documented (pages deleted).
6. Plans & Billing: ignored. The page is untouched and no plan names or prices appear elsewhere.
7. India-only checkout/auth apps and the Storefront POS contract: not documented. Only Shopify POS is.
8. Visit URL: only one link (one campaign) is allowed.

## Phase 1: Reviews removal and repo cleanup

- Delete orphan Reviews-era pages:
  - `quickstart.mdx` (root)
  - `integrations/{google-seo,google-shopping,facebook,zapier,index,shopify,woocommerce,wployalty}.mdx`
  - `installation-and-setup/woocommerce.mdx`
  - `workflows/{index,getting-started-with-workflows}.mdx`
  - `account/{account-settings,updating-logo,multi-store-management,security-and-access}.mdx`
  - `snippets/essentials/*` and `snippets/snippet-intro.mdx` (Mintlify boilerplate)
  - `DOCUMENTATION_ANALYSIS.md`
- Delete `integrations/google-business.mdx` and `facebook-instagram.mdx` and remove them from the nav and the overview cards (pending Q5).
- Edit pages that are in the nav:
  - `getting-started/welcome.mdx`: remove "reviews" and the Yuko Reviews WooCommerce warning.
  - `integrations/klaviyo.mdx`: remove the "Reviews events" section.
  - `integrations/overview.mdx`: reword line 118 and remove the Google Business card.
  - `snippets/related-integrations.mdx`: remove the Google Business card.
  - `integrations/judgeme.mdx`: remove the Yuko-Reviews tip and FAQ. Also fix the wrong "backfill old reviews" claim.
  - `loyalty/ways-to-earn/write-a-review.mdx`: neutral review source; media bonus and reversal caveats.
  - `multi-action-challenge.mdx`: check the Klaviyo "Review submitted" event mention.
- Keep review-only items out of all new content:
  - Review and Q&A Flow triggers
  - Review and question API endpoints and scopes
  - Review email templates, shortcodes and workflow triggers
  - The Reviews nav item, the Reviews add-on and "Include Reviews" sync
  - Reviews theme blocks and Google Fonts
- Delete unreferenced and review images (`review*.png`, `star.png`, `importa.png`, … plus the root `prnew.png`). Add `redirects` in `docs.json` for deleted public paths.

## Phase 2: Information architecture (docs.json) to mirror the admin nav

Admin order: Dashboard · Loyalty (Programs, Widgets, Emails, Settings) · VIP · Referral (Program, Widgets, Emails) · Membership (Plans, Members, Widgets, Emails) · Customers · Analytics · Workflows · Integrations · Billing · Account (General, Platforms, Email Settings, Translations).

- Promote VIP Tiers and Customers to top-level groups. Rename "Contracts" to "Members". Rename "Order Frequency" to "Order Booster".
- Add new groups and pages: Dashboard & Analytics, Shopify POS, Translations, Email Settings. (Plans & Billing dropped per Phase 0.)
- Fix every "Location: …" breadcrumb ("Notifications" becomes "Emails" under each module, "Loyalty → VIP Tiers" becomes "VIP", and so on).

## Phase 3: Loyalty core

- **Program settings (rewrite):** Rounding Type; singular and plural Point and Store Credit labels; 100-points value; Earning Status (Paid / Fulfilled / **Delivered**); Revert Point Status; Custom login trigger; languages; Exclude customers by tag; Shopify **order** tagging (earned/redeemed); Reset activities. Remove the invented eligibility, exclusions and customer tags.
- **Ways to Earn:**
  - New pages: **TikTok Follow, Pinterest Follow, Visit URL, Subscribe to SMS, Subscribe to WhatsApp, Twitter Share**.
  - Shared options: icon, per-campaign **Tiers / Tier Multipliers**.
  - Place an order: Incremented vs Fixed, Holding period, exclusions, exclude customers.
  - Write a review: Limits (verified purchase, one per order) and the Flow action route.
  - Fix the Facebook Like and Facebook Share fields.
- **Ways to Redeem:**
  - New pages: **POS Amount Discount** and **POS Percentage Discount** (channel concept, Online Store vs Shopify POS).
  - Add to existing pages: Purchase type, specific products/collections, once per order, Coupon Prefix, minimum quantity, combinations.
  - Percentage discount: Maximum Discount Amount (Yuko discount function).
  - Free shipping: countries and maximum shipping rate.
  - Store credit: Shopify-native only.
- **Booster campaigns:**
  - New page: **Product & Collection Multiplier**.
  - Rewrite Spending Goal and Order Booster as milestones with any reward type.
  - Fix First Purchase Boost, Streak (no Day period) and Multi-action ("Match any").
  - Overview: full targeting rules with AND/OR, limits, stacking, "ignore VIP multiplier", widget labels, schedule types, archive, disabling the program, and the Participants/Activity tabs.
- **One-time campaigns:** Customer Tags audience, **Conversions** tab, Trigger workflow events plus Identifier, the Campaign Identifier/Name workflow conditions, `redemption_link` in the CSV, Pending status. Remove the "no reporting" limitation.
- **Backfill:** minor breadcrumb fix; mention Conversions.
- **Customers (rewrite):**
  - Member / Guest / Excluded statuses; operator filters, including Total Redeemed.
  - Import: 500 KB limit, sync prerequisite, creates missing customers.
  - Adjust balance with expiry; Redeem points on a customer's behalf.
  - Assign tier override; Exclude from Program.
  - Shopify admin customer block and Adjust balance action.
  - Remove the Export FAQ.
- **VIP tiers (rewrite):**
  - Top-level nav; qualification basis and period with "Include the last year" carryover.
  - Reset options; Tier Identifier; default and **per-campaign** multiplier and bonus; tier icons.
  - Benefits: Bonus points, recurring store credit, % cashback, Automatic vs code, purchase type.
  - Retention windows and warning; tier benefit product cards; manual override.

## Phase 4: Onsite widgets and storefront

- **Overview:**
  - Correct the extension types. Order status, order list and profile are customer-account UI extensions.
  - Plan and Shopify Plus gating.
  - "Recommended" widgets.
- **Theme app embed:** rename to "Yuko App"; list what depends on it.
- **Floating launcher → "Floating Rewards" (full rewrite of the revamp):**
  - Tabs.
  - Colours and shapes (Square / Shaved / Rounded / Circular).
  - Placement: left by default, with spacing.
  - Visibility rules and URL exclusions.
  - Banner and brand icon; button modes.
  - Home page sections: featured booster, referral share.
  - **Deep links** (`#yuko-<section>`).
  - Custom CSS and shadow DOM.
- **Rewards landing page:**
  - The 7 theme blocks and their settings.
  - Auto-created page at `/pages/loyalty-info-page`, plus Create and Check.
  - FAQ section; logged-in redirect.
- **Loyalty Nudges:** `[ ]` placeholders, Drawer sections, Drawer Height, Visibility card.
- **Branding & locale (rewrite):** 8 palettes, 5 colours, "Apply to all widgets", per-widget Editing language. Remove logo, typography and Markets.
- **Per-widget defaults and labels** for product, cart earn and redeem, checkout earn and redeem, order status, order list, profile and account page:
  - Product: Custom CSS.
  - Checkout redeem: "Hide for customer tags".
  - Account page: reorderable sections.
- **Placeholders snippet:** add the missing tokens.
- **Custom login trigger** (shared by launcher, Nudges and cart redeem).
- **Checkout and customer-account extension setup pages:** correct block names and targets.

## Phase 5: Referrals, Memberships, Emails

- **Referrals:**
  - Program setup: Fraud Prevention (IP Address Match on Growth, Block Self-Referrals), "Enroll on first point earned", UTM Campaign only, social sharing.
  - Reward types: "Earn Points", limit to recipient, purchase type, combinations, shipping restrictions.
  - Widgets: split into **4 widgets** (Post-Purchase, Landing Page, Friend Welcome Popup, Share Product).
- **Memberships:**
  - Plans: real benefit list (Bonus points, Store credit, Custom), Merchant Code / Identifier, Add Member / by tag, Active/Inactive.
  - Members (renamed from Contracts): statuses, change next billing date, earned and scheduled benefits.
  - Widgets: **Purchase Options widget** (new); profile widget self-serve upgrade, downgrade and cancel.
  - Validation extension: fix the path.
- **Emails:**
  - Loyalty: 11 templates. New: Points expired, Birthday award, Anniversary award, Reward expired. Delays are configurable.
  - Referral: 3 templates with corrected names.
  - Membership: Created, Upgraded, Downgraded, Cancelled.
  - Shortcodes: rewrite with `{{ }}` and the real keys, including the redemption link.
  - Template editor: basic editor plus the plan-gated **Advanced Editor** (MJML), test email, per-email analytics, monthly limit.
  - Sender & branding becomes **Email Settings**: sender identity and **Custom Domain Emails** with DNS verification.

## Phase 6: Workflows

- **Triggers & conditions:** the current trigger list, including Order Delivered, the One-time Campaign Points Awarded event and the full VIP / Booster / Membership events. Also trigger and profile filters, re-entry, If/Else, and the Campaign Identifier/Name conditions.
- **Build your first:** a new example on a real trigger; Live/Draft.
- **Action nodes:** Email, Coupon, Points Credit (Fixed / Incremental, hold, expiry), Points Debit, and **Webhook** (pending Q1).
- **Wait & exit:** Minutes, Hours or Days; time of day; days of week; auto Exit node.
- **WhatsApp and partner nodes:** 13 providers.
- **Analytics (rewrite):** Subscribers tab (statuses, timeline, failure tooltip) and Emails tab.

## Phase 7: Integrations, Shopify POS, API

- **Overview:** add the categories (Checkout, Authentication minus India-only apps, plus Shopify POS). Move Checkout Boost out of the Shopify Flow group. Change "11 providers" to 13.
- **New pages:**
  - **Shopify POS:** setup, the POS rewards, the cashier tile and modal, 39 text keys and placeholders.
  - ~~India-only checkout apps~~: dropped per Phase 0.
  - **Whamaa, ConvertWay.**
- **Updates:**
  - Interakt: CTA button parameters.
  - Judge.me: OAuth, Review Status condition.
  - Klaviyo, Omnisend and Retainful: new `yuko_points_expiring_in_*` properties.
- **Shopify Flow (rewrite):** the real loyalty, VIP and referral triggers with their payloads; exclude the review triggers and action.
- **Webhooks (rewrite):** real topics, `X-YUKO-HMAC-SHA256` signature, 3 retries (60s / 5m / 15m), auto-disable after 10 failures (pending Q2).
- **REST API:**
  - New endpoints: Get reward, List booster campaigns (no partner or Storefront POS endpoints, per Phase 0).
  - New page listing all scopes.
  - Fix `third-party-checkout-integrations.mdx` (scope format, broken links).

## Phase 8: Getting started, Dashboard, Analytics, Billing, Account

- **Quickstart and onboarding:** contact-only onboarding; 100 points = $1 auto default; seeded campaigns, rewards, launcher and referral.
- **New pages:**
  - **Dashboard:** setup checklist, order usage, revenue cards.
  - **Analytics:** tabs, plan gating, comparisons, View report / CSV, Export Report.
- ~~Plans & Billing~~: dropped per Phase 0.
- **Account:**
  - General: timezone, date and time format, Coupon Prefix, logo, languages.
  - Platforms: sync.
  - **Translations** (new).
  - Email Blacklist: it is a suppression list, under Email Settings.
  - Account overview.
- **Glossary and FAQ** sweep for renamed terms.

## Phase 9: QA and polish

- Run a link check (`mint broken-links`) and confirm no orphans or missing nav entries.
- Update the related-* snippets and cross-links.
- Grep for leftover review terms and old labels ("Notifications", "Contracts", "Order Frequency", `[shortcode]` syntax in emails).
- List screenshot placeholders that need fresh captures.
- `mint dev` smoke test, then a PR to `main`.

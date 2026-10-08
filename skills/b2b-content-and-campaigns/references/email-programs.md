# Nurture, Lifecycle & Event Email (B2B)

Use this for marketing programs sent to contacts who are not in an active sales cycle. For 1:1 sales outreach and follow-ups, use `executive-outreach`.

## Program design
- **Define the entry and exit for every track.**
  - Who enters, and on what trigger.
  - Who leaves, and when: became an opportunity, unsubscribed, went inactive, or finished the track.
  - Every track ends with a sunset step. Re-permission inactive contacts or suppress them.
- **Governance:**
  - One primary nurture track per contact.
  - Priority order: transactional > behavioral trigger > active campaign > evergreen nurture.
  - Cap total marketing touches per contact per week across channels, coordinated with sales sequences.
  - Suppress contacts whose account is in an active deal, unless sales asks otherwise.
- **Stage-appropriate content:**
  - Early stage: insight, benchmarks from real data, frameworks.
  - Evaluation: comparisons, ROI tools, case studies, security overviews.
  - Customers: adoption, advanced use, community, expansion stories.
  - Don't send educational basics to late-stage buyers.

## Each email
- **One job:** one idea, one CTA, written as a value phrase ("Get the PDP content benchmark"), never "Learn more".
- **Subject line:** specific and honest; it delivers what it promises. Draft three variants:
  1. curiosity grounded in substance
  2. specific benefit
  3. contrarian or reframing (only if it's true)
- **Body:** a hook that names the problem → one insight → a takeaway the reader can act on → the CTA. Mobile-first and skimmable.
- **Personalization:** use only reliable fields. A wrong first name or company is worse than none, so set fallbacks for every merge field.

## Event and webinar promotion
- Invite sequence: announce → value reminder (speakers, specific takeaways) → last chance → day-of reminder for registrants.
- Afterwards, send attendees and no-shows different messages: recording, resources, a relevant next step.
- Give sales a list of target-account attendees with what each person engaged with.

## Compliance and deliverability (non-negotiable)
- **Lawful basis and consent appropriate to each market.** See the claims reference in `customer-facing-quality-gate`: CAN-SPAM, CASL, GDPR/PECR.
- **Required elements:** an unsubscribe that is honored promptly across all programs, an accurate sender, and a physical postal address.
- **Bulk senders:** Gmail and Yahoo also require one-click unsubscribe (RFC 8058) and low spam-complaint rates.
- **Sender authentication:** SPF, DKIM and DMARC. Monitor complaint and bounce rates, and remove hard bounces immediately.
- **Keep transactional email transactional.** Don't add marketing content to it.

## Measurement
- **Primary:** clicks, replies, meetings and pipeline from target accounts.
- **Secondary:** unsubscribes and complaints, as a health signal.
- **Opens:** unreliable because of mail privacy protections. Use them only as a rough deliverability indicator.
- **A/B tests:** only with enough volume to read the result. Otherwise call results directional.

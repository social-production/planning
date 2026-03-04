# Open Questions — Social Production Planning Documents

These questions need team answers before the four planning documents can be finalised and architecture work can begin.

---

## Governance

### Badges

**1. What actions earn a badge? (e.g. creating first project, completing X projects, voting X times, participating across different categories)**

all of those

**2. Are badges purely cosmetic with zero effect on platform standing, voting, or access?**

yes, purely cosmetic

**3. Are badges visible on user profiles publicly, or only in certain contexts?**

publicly visible

---

### Moderation

**4. Do we move to category-based moderators (Production, Service, Living Condition and sub-categories) rather than for all channels? (for example some small location based channels may have very few members)**

category-based rather than all channels

**5. Do we adopt a tiered escalation model — project managers handle spam and minor issues first, category moderators handle escalations and serious issues?**

yes

**6. At what point does a channel or category need a moderator — is there a minimum size threshold before one is required?**

i think every project automatically has its creator as moderator, but they're overseen by the category mods, but categories should get moderators once they have some solid activity (ex. 5+ active projects or 30+ active members) so votes for category mods would be fair and needed (not just for empty categories)

**7. How is a moderator elected — community vote within their category, platform-wide vote, or something else?**

community vote within their category because ideally they would be best suited for that specific category

**8. What does a moderator need to maintain their role — a specific vote count, a review period, no sustained reports against them? How often is this reviewed and where does it happen on the platform?**

review period every quarter, if they get reported above a threshold (ex. 3+ reports), it triggers removal vote.

**9. Are moderator roles and voting visible on user profiles?**

roles and voting are visible on moderator profiles so everyone can see how many votes a moderator has, but voting shouldn't be visible on regular user profiles as in no one should see who voted for who.

---

### Voting Thresholds

**10. What is the participation threshold at different project sizes? (e.g. 5 members = 100%, 50 members = 50%, 1000+ members = 10% — actual figures need to be agreed)**

<10 members = 100%, 10-50 = 60% 51-100 members = 40%, 101-999 members = 25%, 1000+ members = 10%

**11. Is there an absolute minimum number of votes regardless of percentage — for example, high-stakes decisions always need at least X votes no matter how small the project?**

absolute minimum should be 5 votes, maybe minimum 10 for major changes?

---

### Discussions and Voting

**12. Can members continue to discuss, comment, and submit new proposals while a vote is actively open, or does discussion close when voting begins?**

yes members can continue discussing/commenting while a vote is open, but new proposals that are major amendments to what's getting voted on should require resubmission and voting period reset.

---

### Threads

**13. How do pure threads work — posts not attached to any project? Who can post, can anyone reply, is there any moderation or governance structure attached to them?**

anyone can post, anyone can reply, threads also has category moderators chosen by platform-wide vote. a "general discussion" category can be made which handles non-project-specific posts, and posts would have a tag requirement similar to projects. or maybe posts are automatically tagged as "general discussion" and they can add other tags to specify their topic.

**14. Can threads have tags that feed into the demand signal and category system the same way projects do?**

yes, there would be a tag requirement for moderation purposes but they can also tag other things like mutual aid or direct need support, which would feed into the demand signal and suggestion list system

---

## Distribution

### Need Verification and Priority

**15. Do we scrap the priority need panel entirely and move to a simpler model — first-come-first-served for most goods, with housing projects designed to include both emergency bare-minimum accommodation and a regular waitlist as separate tiers?**

yes, scrap priority need panel and move to simpler model. but housing projects should be required to specify capacity upfront. also we should clearly define what counts as emergency in the documents.

**16. If we keep any form of priority, how is a genuine need claim verified without creating bureaucracy — default acceptance unless publicly challenged and put to a community vote?**

yes

---

### Inter-Project Resource Flows

**17. Who initiates a resource transfer between projects — a manager of the sending project, the receiving project, or either?**

either is able to, but the receiving project should because they know what they need. sending project then votes to approve.

**18. Does a transfer require a vote from project members, or is it a manager-level decision recorded on-chain?**

require a vote from project members.

**19. Does the receiving project need to confirm and record the transfer separately, or is one on-chain record from the sending side sufficient?**

one on-chain record is sufficient. but i think transfers should require votes from both projects for accountability. the sending project votes to authorize giving the resource away. the receiving project votes to accept the terms of receipt.

---

### Distribution Queue and Delivery

**20. Do we adopt FIFO (first in, first out) as the default distribution method, with managers having the option to manually override for practical reasons such as a recipient being temporarily unavailable?**

yes. but clearly define what allows overrride in the documents.

**21. Should recipients confirm readiness before dispatch — a Kickstarter-style signal when the project nears completion?**

yes, something like "project 80% complete, confirm delivery details within 7 days" and their project timeline of completion should be publicly visible and updated.

**22. If a recipient does not respond within a set period after being contacted, does their allocation automatically pass to the next person in the queue?**

yes

**23. What are the project checkpoints that trigger community updates and milestone notifications — who defines these, is it the project manager or voted on by members?**

i think completion updates, ex. 25% completed, 50% completed, 75% completed, 100% completed, the project manager defines these. also if there's significant delays, the manager has to post an update explaining the delay and revised public timeline.

---

## Production

### Ongoing Projects

**24. How do ongoing projects work — projects with no defined end state like a resource database or a community tool library? Do they follow the same lifecycle or have a separate status?**

lifecycle events for ongoing projects: creation → funding (if needed) → active-ongoing → periodic reviews → dissolved (if voted), i think ongoing projects should track updating or maintenance tasks rather than completion milestones

**25. Does an ongoing project ever reach "completed" or does it stay in "producing" indefinitely with periodic reviews?**

i think it stays in "active-ongoing" indefinitely with periodic reviews (every 6-12 months?)

---

### Service Listings

**26. Should individual service offerings (e.g. "offering: haircuts in this area") be a separate lightweight post type distinct from a full service project?**

i think formal services like "community bike repairs service" with multiple people offering skills should be an ongoing service project using the full project structure (managers, members, voting) whereas individual service projects like "i offer haircuts on mondays" can be posts tagged to a "services" category, moderated like threads.

**27. If so, what governance or safety structure applies to individual service listings — tags, location, manager review, or simply community reporting?**

i think these projects should have safety reviews with community reporting. would escalate to category mods if 3+ bad reports or something

---

## Legal Asset Holding

**28. What is the extraordinary vote threshold required to amend the foundation's core principles — a specific percentage needs to be defined (e.g. 80%, 90%, unanimous)?**

80% or 90% of votes cast with mandatory 50% minimum particpation threshold

**29. What is our preferred jurisdiction to bring to legal counsel first — Switzerland, Netherlands, or Estonia?**

Estonia, but maybe bring all 3 and let them advise based on our model

---

## Open Questions Extended

**1. What if managers violate platform rules? Who's holding them accountable? Because project members wont care enough to memorize the platform's rules. We have category mods, do they overlook this aspect too in a quarterly review? We should clearly define the job of the mod. We should also specify what a mod/project manager should do if they want to step down or turn the position to someone else - obviously cast a proposal/vote but does someone else initiate a proposal to nominate themselves as new mod? I know we said category mods would be elected via vote but how do they get elected? What if no one signs up for it?**

Category moderators oversee project managers in their category. Apart from periodic reviews, reports trigger moderator review. Moderators can issue warnings, temporary restrictions, or initiate removal votes.

Moderator job definition: Respond to community reports within their category. Review flagged content/behavior for rule violations. Issue warnings for minor violations. Initiate removal votes for serious or repeated violations. Post quarterly transparency reports showing actions taken. Must maintain positive community signals (maybe automatic removal vote if 20% of active category members flag concerns).

Category Moderator elections: Once a category has 5+ active projects or 30+ active members, election is auto-triggered. Any member can nominate themselves (or others?) Category members vote using ratio system, 30% participation threshold. Term length: 12 months, eligible for re-election. If no one signs up, category functions without dedicated moderator temporarily. Project managers handle their own projects. Platform-wide moderators (elected separately) can step in for serious issues. Platform prompts members periodically to nominate candidates.

Platform Moderator elections: Annual platform-wide vote. All platform users vote. Ratio voting system (same as everything else). Multiple seats available (start with 3-5 platform-wide mods). 20% participation threshold. Top ratio winners get the seats.

Stepping down process: Moderator or manager posts resignation notice, triggers immediate election/selection process, current moderator/manager stays in role until replacement confirmed or current moderator/manager can nominate a successor members vote to approve.

---

**2. Also what does it mean to report project managers, mods, or even other users? Where do you report and to whom? after someone gets reported, do they automatically escalate to removal votes (for project managers or mods) or is there a number of reports they need against them to trigger a removal vote?**

Every user profile, post, and project has a "report" button. Report form asks: What rule was violated? What happened? Evidence/screenshots? Reports go to appropriate moderator: Project manager behavior → category moderator, Category moderator behavior → platform-wide moderators, User behavior within project → project manager first, escalate to category mod if unresolved, User behavior in threads → category moderator for that thread's category. Appropriate moderators triggers removal votes based on  number of reports (maybe 5+ require removal vote), pattern of rule violations even if below threshold, Repeated warnings ignored. Process: Moderator reviews reports → issues warning or initiates removal vote → removal vote requires 60% approval with 40% participation threshold.

---

**3. Did we decide what we're going to do if someone isn't following the rules of the platform or gets continuous bad reports escalated to moderators? Are they allowed to use the platform?**

Escalating consequences (tiered approach):
- First violation (minor): Warning from moderator, recorded in moderation log
- Second violation or moderate severity: Temporary posting restriction (7-30 days depending on severity). Can still vote and participate in their projects.
- Third violation or serious issue: Removal from specific projects by vote. Can still use platform elsewhere.
- Severe or repeated violations: Platform-wide posting restrictions (can vote but cannot create projects/posts) for defined period
- Extreme cases only: Platform-wide ban (requires platform-wide vote, 70% approval, 30% participation threshold)

Yes, they're allowed to use the platform under restrictions. Full bans are last resort. The platform emphasizes rehabilitation and community accountability over exclusion. Severe violations warranting faster escalation: Harassment, threats, hate speech, Fraud or misappropriation of collective resources, Sharing private information without consent, Repeatedly sabotaging projects.

---

**4. What happens to ghost members who join projects but disappear? After X months of no participation, should they get auto-removed from the project (their history in the project would obviously be preserved)?**

They get to stay in the project. but maybe after (6 months or 1 year?) of inactivity (Definition of inactive: No votes cast, no comments/posts, no task updates for 6 months or 1 year?) they get messaged asking if they're still interested in the project and if they click yes, they stay in the project, otherwise they can click no and they'll be removed from the project, but their full participation history will be preserved and they can rejoin any project instantly by clicking "join" again.

---

**5. If multiple projects need the same limited resource, how is priority decided? First come first serve? Voting?**

first come first serve at project level. if someone requests something later, they can join the waitlist. FCFS can be overrriden by:
- Emergency/crisis projects (voted as "priority" by category) jump the queue
- Projects serving more people might get priority by category vote

Deadlock resolution: If two projects need the same resource and dispute priority, category-wide vote decides (40% participation, highest ratio wins)

Implementation:
- Resources are tagged in database by type
- When project requests resource, platform or sending project checks inventory
- If sufficient: approved
- If insufficient: added to waitlist, platform/sending project notifies projects in category that resource is constrained
- Any project can propose a priority vote if they believe their need is more urgent

---

**6. Can you explain how exactly funding works on the platform? Are contributions tied to user accounts? can fund drives happen off-platform with collected funds inputted to the platform afterwards by a project member?**

Yes, contributions tied to user accounts for return-on-failure. User clicks "Contribute" on project page → enters amount → payment processed. Funds go directly to foundation escrow account (never to individuals). Project page shows: Goal amount, current amount, number of contributors. Progress bar updates in real-time. if user funds a project, their financial contribution amounts stay private (only totals are public).

Off-platform contributions allowed with documentation. Project manager records something like: "Received $500 cash from Alex Smith for lumber purchase" in platform database, noted as "external contribution" with the contributor's name or "anon". If project fails, external contributors contacted via information provided for refund.

Release of funds: Project hits funding goal → project manager submits purchase plan → funds released to foundation to make purchases on project's behalf. or: manager requests specific payment (e.g., "pay Lumber Co. $1,200") → foundation makes payment directly. All transactions recorded on-chain.

Refund process: Project cancelled before goal met → automatic refunds to all contributors. Project cancelled after goal met but before production → vote required on whether to refund or reallocate funds to similar project.

---

**7. What about cross-border complications? Projects spanning multiple countries? How is shipping physical goods internationally handled? Tax laws in some jurisdictions? Local regulations on food, healthcare, other things?**

Short-term approach (MVP): Projects spanning multiple countries tagged as "international collaboration" but operate as separate projects coordinating with each other. Cross-border shipping handled by projects themselves as regular shipping (no special platform support initially). Legal compliance is responsibility of project managers in consultation with category moderators.

Medium-term (scaling): Legal counsel per region as platform expands to 3+ countries with significant user bases. Regional foundation chapters: Foundation establishes legal entities in each major region to hold assets locally, reducing cross-border transfer complications. Shipping partnerships: Platform negotiates with international shipping services for reduced rates. Compliance tools: Platform provides checklists for common regulations (food safety, healthcare services, import/export) per region.

Tax considerations: Foundation is non-profit, but members may owe taxes on received goods in some jurisdictions (treated as gifts or barter). Platform should include disclaimer: "Consult local tax advisor regarding tax obligations" Platform does not provide tax reporting (too complex across jurisdictions).

Food and healthcare regulations cross-border: Platform includes prominent warnings on projects involving regulated goods. Project managers must confirm compliance with local regulations. Category moderators should include subject-matter experts where possible (e.g., food safety certified person moderates Food Production category). Platform does not verify compliance—this is community responsibility with legal liability on individuals.

---

**8. What data does the platform collect and store? What's public vs. private?**

Public by default: Project details, posts, votes cast (but not voting choices on user profiles), distribution allocations, moderation actions, funding

Private: DMs between users, personal delivery addresses, if user funds a project their financial contribution amounts stay private (only totals are public)

User control: Members set visibility for: full name vs. username, location (specific address vs. city/region only), contact details

Data retention: All data preserved indefinitely for transparency. Users can delete their account but public participation history remains (anonymized to "deleted user")

---

**Communities are a proposed organisational layer for groups of people with a shared identity or real-world connection — a local chapter, an existing organisation, a neighbourhood group. They are social and organisational tools only. Communities do not own production, do not control distribution, and do not hold assets. Everything produced through the platform belongs to the collective regardless of which community's members produced it. A community is a club, not a cooperative within a cooperative.**

**1. Is a community an optional feature or a core object all users exist within by default?**


---

**2. Can a community be closed and should open or closed be the default?**


---

**3. When someone is invited to a closed community is a membership vote automatically triggered?**


---

**4. Does a community have its own internal governance or does it only use the platform-wide model?**


---

**5. Can a community join a project as a unit, and if so do members vote individually or does the community cast a collective signal?**


---

**6. Can a community have internal discussion channels visible only to its members?**


---

**7. Does a community have its own internal moderator and how do they relate to channel moderators?**


---
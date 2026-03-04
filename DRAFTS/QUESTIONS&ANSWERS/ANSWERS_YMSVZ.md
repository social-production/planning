# Open Questions — Social Production Planning Documents

These questions need team answers before the four planning documents can be finalised and architecture work can begin.

---

## Governance

### Badges/Reputation

**1. What actions earn a badge? (e.g. creating first project, completing X projects, voting X times, participating across different categories)**

yes easy to hard basically to introduce users to different aspects of the program, give something visual for users to work towards.

**2. Are badges purely cosmetic with zero effect on platform standing, voting, or access?**

purely cosmetic

**3. Are badges visible on user profiles publicly, or only in certain contexts?**

visible publicly, i guess users can have option to turn off

---

### Moderation

**4. Do we move to category-based moderators (Production, Service, Living Condition and sub-categories) rather than for all channels? (for example some small location based channels may have very few members)**

i believe all channels should have moderators, similar to reddit, they would only really be dealing with spam, and always would be revocable from power. any user can make channels, its not like they would be real determinants, just an easy place to coalesce posts with tags.

**5. Do we adopt a tiered escalation model — project managers handle spam and minor issues first, category moderators handle escalations and serious issues?**

i think we only need channel moderators. the channel moderator can see the report and deal with accordingly to their channel. users can be silenced etc to specific channels.

**6. At what point does a channel or category need a moderator — is there a minimum size threshold before one is required?**

i think all channels should have a moderator.

**7. How is a moderator elected — community vote within their category, platform-wide vote, or something else?**

within the channel page would be list of moderators, with favourable percentage number next to their name, users can like or dislike whenever they see fit

**8. What does a moderator need to maintain their role — a specific vote count, a review period, no sustained reports against them? How often is this reviewed and where does it happen on the platform?**

as explained in previous, they must maintain a certain positive ratio. people can voluntary put themselves up for "election"

**9. Are moderator roles and voting visible on user profiles?**

moderator roles sure, you shouldn't see what people voted for that is private. their ratio of support should be visible on the channel they moderate

---

### Voting Thresholds

**10. What is the participation threshold at different project sizes? (e.g. 5 members = 100%, 50 members = 50%, 1000+ members = 10% — actual figures need to be agreed)**

yeah those numbers seem fine to me

**11. Is there an absolute minimum number of votes regardless of percentage — for example, high-stakes decisions always need at least X votes no matter how small the project?**

i dont know,  guess we could implement this, project managers when putting something to vote could choose the minimum threshold

---

### Discussions and Voting

**12. Can members continue to discuss, comment, and submit new proposals while a vote is actively open, or does discussion close when voting begins?**

absolutely

---

### Threads

**13. How do pure threads work — posts not attached to any project? Who can post, can anyone reply, is there any moderation or governance structure attached to them?**

of course anyone can post and reply. moderation would go to the channel moderators in which the post was tagged

**14. Can threads have tags that feed into the demand signal and category system the same way projects do?**

interesting i think it should be possible, but not sure how that would work, maybe can do some sort of expression of interest vote like a poll within  a thread/project

---

## Distribution

### Need Verification and Priority

**15. Do we scrap the priority need panel entirely and move to a simpler model — first-come-first-served for most goods, with housing projects designed to include both emergency bare-minimum accommodation and a regular waitlist as separate tiers?**

yes i think we scrap it entirely and plans should incorporate emergency situations in them

**16. If we keep any form of priority, how is a genuine need claim verified without creating bureaucracy — default acceptance unless publicly challenged and put to a community vote?**

no we should scrap verification

---

### Inter-Project Resource Flows

**17. Who initiates a resource transfer between projects — a manager of the sending project, the receiving project, or either?**

sending manager initiates, receiving manager confirms.

**18. Does a transfer require a vote from project members, or is it a manager-level decision recorded on-chain?**

members already vote on the distribution plan before completion of project

**19. Does the receiving project need to confirm and record the transfer separately, or is one on-chain record from the sending side sufficient?**

yes i think they do

---

### Distribution Queue and Delivery

**20. Do we adopt FIFO (first in, first out) as the default distribution method, with managers having the option to manually override for practical reasons such as a recipient being temporarily unavailable?**

i think it should be automated based on signals

**21. Should recipients confirm readiness before dispatch — a Kickstarter-style signal when the project nears completion?**

yes they should

**22. If a recipient does not respond within a set period after being contacted, does their allocation automatically pass to the next person in the queue?**

yes i believe so

**23. What are the project checkpoints that trigger community updates and milestone notifications — who defines these, is it the project manager or voted on by members?**

percentage of collective fund, managers posting updates as they see fit. they would update in the timeline, appearing in "latest" sorting mode again. in feed, projects would have time of creation and time of last update. also when moving into suggestion - on going- completed etc

---

## Production

### Ongoing Projects

**24. How do ongoing projects work — projects with no defined end state like a resource database or a community tool library? Do they follow the same lifecycle or have a separate status?**

i guess they would just be on going. because anything may be completed if it gets replaced by something bigger and better

**25. Does an ongoing project ever reach "completed" or does it stay in "producing" indefinitely with periodic reviews?**

i think it just stays on going until it is replaced or people stop using it

---

### Service Listings

**26. Should individual service offerings (e.g. "offering: haircuts in this area") be a separate lightweight post type distinct from a full service project?**

yes i believe it should.

**27. If so, what governance or safety structure applies to individual service listings — tags, location, manager review, or simply community reporting?**

tags to channels, always subject to channel moderators, location would be good. ideally we set up communities halls to facilitate services

---

## Legal Asset Holding

**28. What is the extraordinary vote threshold required to amend the foundation's core principles — a specific percentage needs to be defined (e.g. 80%, 90%, unanimous)?**

this would have to depend on userbase. if we had an extreme amount of users, for example billions, it would be crazy to want 90%, or maybe it wouldn't, i think the legal documentation like this can be more finalized later

**29. What is our preferred jurisdiction to bring to legal counsel first — Switzerland, Netherlands, or Estonia?**

to be determined after legal counsel at appropriate time.

---

## Open Questions Extended

**1. What if managers violate platform rules? Who's holding them accountable? Because project members wont care enough to memorize the platform's rules. Do category mods overlook this aspect too in a periodic review? We should clearly define the job of the mod. We should also specify what a mod/project manager should do if they want to step down or turn the position to someone else — obviously cast a proposal/vote but does someone else initiate a proposal to nominate themselves as new mod? How do mods get nominated? What if no one signs up for it?**

channel moderators and project managers are revokable at any time, permanently subject to a vote of confidence ratio displayed on the channel and project info. they have to maintain a given ratio of positive signal (lets say 70% for now). the moderator of a channel exists to basically remove spam, deal with complaints about users or punish to some degree bad behavior, silencing chat within the channel for a certain amount of time etc. project managers exist to give updates on the project, create meetings, create collective funds. channel moderators and project managers can step down at any time and users can ask put themselves up for election at any moment. if no one signs up for channel moderation, it goes unmoderated until someone puts their hand up

---

**2. Also what does it mean to report project managers, mods, or even other users? Where do you report and to whom? After someone gets reported, does it automatically escalate to removal votes (for project managers/mods) or is there a number of reports they need against them to trigger a removal vote?**

reports of project managers goes to the channels in which the channel/s the project is tagged. same goes for users. report of channel moderators, would go to the other moderators of the channel i guess? important that channel moderators are always revokeable by automatic dismissal if low confidence ratio falls below a number.

---

**3. Did we decide what we're going to do if someone isn't following the rules of the platform or gets continuous bad reports escalated to mods? Are they allowed to keep using the platform?**

i think chat bans, each longer than the last is the best option. they can still vote, and even go to meetings.

---

**4. What happens to ghost members who join projects but disappear? After X months of no participation, should they get auto-removed from the project (their history in the project would obviously be preserved)?**

nothing really, i think being a member is more or less like following a project, being notified when there are updates, votes etc. actually maybe after a given time of activity they get some sort of notification to ask if they are still interested. but i think with the function to lower the threshold for voting requirements as the project membership gets larger should deal with it

---

**5. If multiple projects need the same limited resource, how is priority decided? First come first serve? Voting?**

distribution of resources is decided before acquisition or production of them. in the case that someone perhaps donates resources, a following post and vote for distribution and application of the new resources would have to be done

---

**6. Can you explain how exactly funding works on the platform? Are contributions tied to user accounts? Can fund drives happen off-platform with collected funds inputted to the platform afterwards by a project member or manager?**

contributions are just a donation essentially. contributions are not tied to user accounts. although im not opposed for under the collective fund, a list of distributors shows, with users opting for anonymous if they so choose. people are of course motivated by recognition for their input

---

**7. Do we need to consider cross-border complications from projects spanning across multiple countries? Shipping physical goods internationally? Tax laws in some jurisdictions? Local regulations on food/healthcare/other? Would we need legal counsel per major region eventually?**

yeah very very likely. we talked earlier of even sub organizations per region where it might be necessary, of course under command from the overarching organization. but could be necessary in some jurisdictions to hold certain assets, simplify or reduce tax.

---

**8. We should also clearly document: what data does the platform collect and store? What's public vs. private?**

Public by default: Project details, posts, votes cast (but not voting choices on user profiles), distribution allocations, moderation actions, funding

Private: DMs between users, personal delivery addresses, if user funds a project their financial contribution amounts stay private (only totals are public)

User control: Members set visibility for: full name vs. username, location (specific address vs. city/region only), contact details

Data retention: All data preserved indefinitely for transparency. Users can delete their account but public participation history remains (anonymized to "deleted user")

---

**Communities are a proposed organisational layer for groups of people with a shared identity or real-world connection — a local chapter, an existing organisation, a neighbourhood group. They are social and organisational tools only. Communities do not own production, do not control distribution, and do not hold assets. Everything produced through the platform belongs to the collective regardless of which community's members produced it. A community is a club, not a cooperative within a cooperative.**

**1. Is a community an optional feature or a core object all users exist within by default?**

completely optional.

---

**2. Can a community be closed and should open or closed be the default?**

i think they can be closed, but open by default. essentially just a club channel

---

**3. When someone is invited to a closed community is a membership vote automatically triggered?**

yes i think so

---

**4. Does a community have its own internal governance or does it only use the platform-wide model?**

i think it should follow platform wide model

---

**5. Can a community join a project as a unit, and if so do members vote individually or does the community cast a collective signal?**

i think community can just connect to a project, community moderator essentially adds the tag to the community and the project is then posted in the feed of the community channel. individuals in the comminity signal, vote on plans of distribution and production as ordinary individuals.

---

**6. Can a community have internal discussion channels visible only to its members?**

the community essentially acts as a discussion only channel. but can connect to projects 

---

**7. Does a community have its own internal moderator and how do they relate to channel moderators?**

the community has moderators, essentially acts as a channel

---

**Storage**

**1. Is a warehouse/storage facility its own project type on the platform, with managers and governance like any other project?**

yes
---

**2. Who can deposit into collective storage — any production project, or does a vote authorise what gets stored?**

any production project
---

**3. Who can request from collective storage — any project manager, or does it require a member vote within the requesting project?**

project manager after production plan finalized, receiving project manager at warehouse, confirms (or possibly flags request for discussion) and sends material. production manager at project confirms receival of material. all recorded on blockchain
---

**4. When stock is limited and multiple projects need the same resource, how is priority decided — FIFO, urgency signal, community vote?**

fifo
---

**5. Is storage location tied to region — does a New York warehouse serve New York projects by default, or is stock platform-wide?**

platform wide, 
---

**6. How is inventory tracked — in the platform database with on-chain records for every movement in and out?**

yes absolutely
---

**7. Does stored stock have an expiry or review cycle — for example perishable goods or equipment that degrades?**

yes definitely. also some stock needs stored seperately, fuel and fire hazard material for example
---

**Inter-Project Linking and Interest Signalling**

**8. Can a project formally link to another project to signal it is a downstream recipient of its output?**

yes
---

**9. Who initiates a link — the producing project, the receiving project, or either?**

receiving project manager initiates, producing project manager accepts
---

**10. Does linking require a vote from the producing project's members to accept the receiving project as a recipient in their distribution plan?**

no they would just be signalled under demand, to be considered  by users/ai suggestions when creating a distribution and production plan. link does not guarantee allocation, just signals demand and consideration
---

**11. Can a project signal interest in future production before a production project even exists — feeding into the suggestion list as a demand signal?**

yes absolutely
---

**12. Can multiple projects link to the same production project, and if so how is the available output divided between them?**

yes they can. they would come under demand signal, and in production and distribution plans would be considered
---

**13. Is the full map of linked projects publicly visible so the community can see the supply chain forming around a production effort?**

yes sounds like a great idea
---


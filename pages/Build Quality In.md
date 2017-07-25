# Build Quality In

Software systems are not built and then tested after the fact. A proper testing strategy will be incorporated with every feature, bug fix, database upgrade, etc.

### Cross-Functional Teams
Testers live on feature development teams alongside the other disciplines (product, development, design, operations). Their charter is *not* to test every change, but to own quality throughout the lifecycle. This could include manual testing, building automated tests, and/or directing testing activities for the team.

### Testing Activities/Gates
1. All work items must be vetted by cross-functional teams for acceptance criteria *BEFORE* work begins. Testing a feature in your mind before it comes one.
2. All tasking (and estimates) related to new changes must consider impacts to automated tests. Trade-offs can be made by group decision, but the work must be catalogued for future prioritization. (Example: Delay test automation for faster release, but the deferred work must be added to the backlog as technical debt.)
3. Cross-functional sign-off of all new work. Go/No-go decisions are made at the feature level before merge, not at the release level.
4. More on #3. There are no "Go/No-Go" ceremonies or meetings. Once new changes are merged, they are going live shortly, _unless someone stops the line_. All team members have the responsibility to actively look for defects or other vulnerabilites in pre-production environments.
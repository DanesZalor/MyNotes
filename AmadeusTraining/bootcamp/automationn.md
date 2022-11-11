## automation 101

Navitaire test automation principles, automation culture and processes

Automation is everyone's responsibility:
- **Devs** - make sure the code is automatable
- **QA** - drives automation of tests with consistent and reliable results
- **PO** - there's room for automation in each adn every sprint being planned
- **Srum Master** - make sure everyone in Scrum is placing sufficient attention and value to test automation

Components of Automated Testing
- Lab/Environment - dedicated CI/CD, vm, etc where only automated tests are being executed
- Automated Tools - dictates the success/failure of the tests  
- Test Scripts - the test cases automated
- Input
- Test Results
- Software to Test

Automated Test Process
- Define scope of automation (what part to be automated)
- planning, design and developement of the automation solution
- test execution
- maintenance

## AGILE

goal of automation in AGILE
- provides rapid feedback to the team
- ensures previously built functionality still works
- can perform testing as often as required

Iteration with AGILE
- **In-Sprint Automation** automated tests as part of the "Definition of Done"
- **PArallel with Developement Work** - during development, QA can already plan and create automated tests
- **Continuous Integration** - automated tests is integrated with build allows for earlier detection of potential bus or issues.
- **Reports** tool or framework should provide meaningful test results which should be madew available to everyone in the team. 

### Agile Test workflow
1. Create a test plan
2. Identify test cases that can be automated and provide value to business
3. Write automated tests
4. Execute against daily build
5. Stabilize automated tests against the final developement output.
6. Integrated with CI


### tips for integrating automated tests
- start small and simple functionalities
- allocate backlogs per sprint for automation
- create meaningful test that ensure the validity of the product
- setup a CI system
- Resolve test failures ASAP
- have an intuitive reporting mechanism in place

### Indicators for good automated testing
- Decisive - contains all info to automatically determine success/failure
- Accurate - results https://dev.azure.com/Navitaire/
- Complete - performs all activities and data necessary
- Repeatable - deterministics and always gives the same results
- Isolated - not affected by other tests
- Unique - provides new info not given by other test
- Fast 

## Navitaire Automation Tools
- **Navitaire Automation Framework** (NAF) - Common automation framework used accross Navitaire. Developed and managed by the automation team. Built using C# and requires test scripts to be written in C#. Currently being used in a variety of applications ranging from web, mobile, desktop, API, SQL and even core layer.
- **SOAP UI** - mainly used for API testing. implements a Request-Response approach
- **Powershell** - used to automate tasks and trigger tests using different tools. Task based command-line shell and scripting language. 

---

**Epics** represent a business initiative to be accomplished. It is a big work that can be divided into smaller works which are called **Features**. **Product Backlogs** are like idk

### Sprint
can reach out to the scrum team and participate in discussing workflow or code review

### Daily Scrum (stand up)
inspects the progress. Dev team is required to attend the Standup and is alloted 15 minutes. keeping it quick, focused and relevant. Everyone is required to answer the following questions:
1. What did I do yesterday?
2. What will I do today?
3. Do I see any impediments that will hinder us from meeting the sprint goal?

### Sprint Retrospective
held at the end of every sprint. Scrum team identifies:
1. What went well?
2. What went wrong?
3. What can be improved?


## Automation Dash board
#### GQM
- *G*oal (Conceptual Level)
- *Q*uestion (Operation Level)
- *M*etric (Quantitative Level)

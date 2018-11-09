Table of Contents

Naming

- --Test suite names
- --Test case names
- --Keyword names
- --Naming setup and teardown

Test Case Structure

- --Tests and Resources Lay-out
- --Workflow tests

User keywords

Variables

- --Variable Naming

Avoid sleeping

#

# Robot Framework Coding Style

# Naming

**Test suite names**

- Suite names should be as descriptive as possible.
- Test Script names should be less than 20 characters.
- Names are created automatically from file or directory names:
- Extensions are stripped.
- Underscores are converted to spaces.
- Name is all lower case, with  the first letter of words being capitalized.
- Names can be relatively long, but overly long.
- The name of the top-level suite can be overridden from the command line using the --name option if needed.
- Explains &quot;what&quot; not &quot;how&quot;

Examples:

Login\_tests\_using\_selenium.robot  -\&gt;  Login Tests

IP\_v4\_and\_v6       -\&gt;  IP v4 and v6

**Test case names**

- Test names should be descriptive, like the suite names.
- If a suite contains many similar tests, and is well named, test names can be shorter.
- Name is the same as you specified in the test case file without any conversion.
- For example, if we have tests related to invalid login in a file invalid\_login.robot, these would be

| **OK test case names:** | **Poor test case names:** |
| --- | --- |
| Empty Password | Login With Empty Password Should Fail |
| Empty Username | Login With Empty Username Should Fail |
| Empty Username and Password | Login With Empty Username And Password Should Fail |
| Invalid Username | Login With Invalid Username Should Fail |
| Invalid Password | Login With Invalid Password Should Fail |
| Invalid Username and Password | Login With Invalid Username And Invalid Password Should Fail |





**Keyword names**

- Keyword names should be descriptive and clear.
- Should explain what the keyword does, not how it does its task(s).
- Very different abstraction levels (e.g. Input Text or Administrator logs into system).
- Keyword name should have each first letter capitalized. (e.g.  Valid Login Chrome)

| **OK:** | **Poor:** |
| --- | --- |
| Login With Valid Credentials | Input valid username and valid password and click login button |

**Naming setup and teardown**

- Use a name that describes what is done.
- Possibly use an existing keyword.
- More abstract names are acceptable if a setup or teardown contains unrelated steps.
- Listing steps in name is duplication and a maintenance problem (e.g. Login to system, add user, activate alarms and check balance).
- Often better to use something generic (e.g. Initialize system).
- BuiltIn keyword Run Keywords can work well if keywords implementing lower level steps already exist.
- Not reusable so best used when the setup or teardown scenario is needed only once.
- Everyone working with these tests should always understand what a setup or teardown does.

| **Good:** | **Bad:** |
| --- | --- |
| Suite Setup     Initialize System | Suite Setup     Login To System, Add User, Activate Alarms And Check Balance  |
| **Good (if only used once):** |   |
| Suite Setup     Run Keywords...             Login To System    AND...             Add User           AND...             Activate Alarms    AND...             Check Balance  |   |



**Test case structure**

- Test case should be easy to understand.
- One test case should be testing one thing.

**Tests and Resources Lay-out**

- Tabs or Spaces?
  - Spaces are the preferred indentation method.
  - Indentation is 1 space between words and 2 spaces between variables.
  - Tests should be indented from the title of the test
- Maximum Line Length
  - Since Robot Framework is a Domain Specific Language, and sometime the sentence may a little long, we don&#39;t need limit the maximum line length.
- A single line should be used to separate Tests. For keywords a single line should be used to separate **non-related tasks**. Related tasks do not need this.

\*\*\* Test Cases \*\*\*

Valid Login

  Given browser is opened to login page

  When user &quot;demo&quot; logs in with password &quot;mode&quot;

  Then welcome page should be open

**Workflow tests**

- Have Keywords describe what a test does.
  - Use clear keyword names and suitable abstraction level.
  - Should contain enough information to run manually.
  - Should never need documentation or commenting to explain what the test does.
- Different tests can have different abstraction levels.
  - Tests for a detailed functionality are more precise.
  - End-to-end tests can be on very high level.
  - One test should use only one abstraction level
- No complex logic on the test case level.
- No for loops or if/else constructs.
- Use variable assignments with care.
- Test cases should not look like scripts
- Max 10 steps, preferably less. (If more, Keywords are likely too specific)
- Should be written in gherkin if possible (Given/When/Then)

Eg:

\*\*\* Test Cases \*\*\*

Valid Login

    Given browser is opened to login page

    When user &quot;demo&quot; logs in with password &quot;mode&quot;

    Then welcome page should be open

**User keywords**

- Should be easy to understand.
  - Same rules as with workflow tests.
- Different abstraction levels.
- Can contain some programming logic (for loops, if/else).
- Especially on lower level keywords.
- Complex logic in libraries rather than in user keywords.

**Variables**

- Used for long and/or complicated values.
- Pass information between keywords.
- Pass information from them command line using the --variable option.

**Variable naming**

- Clear but not too long names.
- Can use comments in variable table to document them more.
- Use case consistently:
  - Lower case with local variables only available inside a certain scope.
  - Upper case with others (global, suite or test level).
  - Both space and underscore can be used as a word separator.
- Recommended to also list variables that are set dynamically in the variable table.
- Set typically using BuiltIn keyword Set Suite Variable.
- The initial value should explain where/how the real value is set.

\*\*\* Variables \*\*\*

# Default system address. Override when tested against other instances.

${SERVER URL}     http://nuance.com/     #main server URL

${USER}           Value set dynamically at suite setup

**Avoid sleeping**

- Sleeping is a fragile way to synchronize tests.
- Safety margins cause too long sleeps on average.
- Instead of sleeps, use keyword that polls if an action has occurred.
- Keyword names often starts with Wait ....
- Should have a maximum time to wait.
- Possible to wrap other keywords inside the BuiltIn keyword Wait Until Keyword Succeeds.
- Sometimes sleeping is the easiest solution.
- Use with care.
- Never use in keywords that are used often.
- Can be useful in debugging to stop execution.
- Dialogs library often works better.

Library

- --Markdown lang coding guide upload to repository
- --Table of contents
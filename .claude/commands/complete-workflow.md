I'll guide you through a complete workflow for implementing issue #$ARGUMENTS, from analysis to PR creation.

Let's start the workflow:

## STEP 0: ANALYZE ISSUE

I'll analyze GitHub issue #$ARGUMENTS to get a clear understanding of the requirements and create a technical spec.

First, I'll fetch the issue details:

[After this I'll output the complete issue details and my analysis below]

### Technical Specification for Issue #$ARGUMENTS

#### Issue Summary
- Title: [Issue title]
- Description: [Brief description]
- Labels: [Labels]
- Priority: [High/Medium/Low]

#### Problem Statement
[1-2 paragraphs explaining the problem]

#### Technical Approach
[Detailed technical approach]

#### Implementation Plan
1. [Step 1]
2. [Step 2]
3. [Step 3]

#### Test Plan
1. Unit Tests:
   - [test scenario]
2. Component Tests:
   - [test scenario]
3. Integration Tests:
   - [test scenario]

#### Files to Modify
- [file path]: [changes]

#### Files to Create
- [file path]: [purpose]

#### Existing Utilities to Leverage
- [utility name/path]: [purpose]

#### Success Criteria
- [ ] [criterion 1]
- [ ] [criterion 2]

#### Out of Scope
- [item 1]
- [item 2]

### Create comment on GitHub isssue with Technical Details
I'll create a comment on the GitHub issue containing the Technical 

### REVIEW POINT 0:
Are you satisfied with this analysis? Type "Yes" to proceed with TDD implementation or "No" provide feedback to adjust the analysis.

If "No" is provided, I'll pull the updated issue from GitHub, review any added comments, then update the Technical Specification for the Issue, provide a comment with the updated details, then repeate Review Point 1.

## Step 1: CREATE FEATURE BRANCH
Create a feature branch for implementing this issue:

1. Check if the branch exists
2. If it exists, provide interactive options:
   - Use the existing branch (continue previous work)
   - Delete and recreate the branch (clean start)
   - Create a new branch with timestamp (avoid conflicts)
3. If it doesn't exist, create it from the master branch

## STEP 2: TDD IMPLEMENTATION

I'll now implement the feature using Test-Driven Development:
1. Write tests that define expected behavior
2. Verify tests fail (red)
3. Implement code to make tests pass (green)
4. Refactor while keeping tests passing

[I'll output the complete implementation details below]

## REVIEW POINT 2:
Are you satisfied with the implementation? Type "continue" to proceed with documentation or provide feedback to improve the implementation.

## STEP 3: CREATE DOCUMENTATION

I'll now create documentation for the implemented feature:

[I'll output the complete documentation below]

## REVIEW POINT 3:
Is the documentation complete and accurate? Type "continue" to proceed with creating a PR or provide feedback to enhance the documentation.

## STEP 4: CREATE PULL REQUEST
I'll prepare and submit a pull request for your changes:

[I'll output the complete PR details below]

## WORKFLOW COMPLETE
The feature implementation workflow is now complete! The PR has been created and is ready for review.
# Git Principles

## One Task One Branch
### Branch Name As A Task
**To ensure that each branch corresponds to a specific task**, making it easier to track progress and manage changes.
- **Example**: Jira task ID `CRM-100` -> `feat/CRM-100-add-new-application-form`

## One Subtask One Commit
### Subtasks As A Unit
**To effectively manage a task, break it down into different area subtasks for a single commit.** This approach helps in organizing work and ensuring that each aspect of the task is addressed.
- **Example**: Breakdown of the Jira task to add a new application form: 
  1. **Frontend**: Form layout design
  2. **Backend**: Form fields implementation
  3. **Database**: SQL Preparation

### Descriptive Commit Message
**To ensure clarity and effective tracking of changes, a well-structured commit message is essential.**
- **Example**: Commit the frontend subtask
  - **Header**: `feat(CRM-100): Design new application form layout`
  - **Body**: Created the initial UI layout for the new application form, which includes:
    1. Added input fields: name (Required), email (Required), phone number, address
    2. Implemented validation for required fields and error handling.
  
  **🚨 Note on `feat(CRM-100)` Commit Message Format**: Ensure pipeline automation settings align with branch commit message.

## Parent First, Merge Next
### Sync For Conflict-Free Code
**To maintain code integrity and minimize merge conflicts, always sync with the parent branch before merging your changes.**
- **Example**: Before merging your feature branch `feat/CRM-100-add-new-application-form` into the main development branch:
1. First, pull the latest changes from the parent branch (sales-form-update-2025-06):
     ```
     git checkout sales-form-update-2025-06
     git pull
     git checkout feat/CRM-100-add-new-application-form
     git merge sales-form-update-2025-06
     ```
  2. Resolve any conflicts that arise during the merge process
  3. Run tests to ensure everything works correctly after the merge
  4. Then proceed with creating a pull request or merging your feature branch

## Test First, Push Next
### Local Testing As A Rule
**To ensure code quality and prevent issues in the main codebase, always test your changes locally before committing and pushing them.**
- **Example**: Before finalizing your changes with a commit:
  1. Run all automated tests to ensure your changes work as expected:
     ```
     # Stage your changes
     git add .
     
     # Run automated tests before committing
     npm run test
     ```
  2. Perform manual testing to verify the user experience and edge cases:
     ```
     # Start local development server
     npm run dev
     
     # Manually test the application form:
     # - Test with valid inputs
     # - Test with invalid inputs
     # - Test required field validation
     # - Test form submission
     # - Test across different browsers if applicable
     ```
  3. Once all tests pass, commit your changes:
     ```
     git commit -m "feat(CRM-100): Implement new application form"
     ```
  4. If any tests fail, make the necessary fixes and test again before committing:
     ```
     # Make necessary fixes
     
     # Re-run automated tests
     npm run test
     
     # Perform manual testing again
     npm run dev
     
     # Only commit when everything works
     git add .
     git commit -m "feat(CRM-100): Implement new application form"
     ```
  5. After successful testing and committing, push your changes:
     ```
     git push origin feat/CRM-100-add-new-application-form
     ```

## Review First, Merge Next
### Pull Request For Quality Assurance
**To maintain codebase integrity and foster collaboration, always create a Pull Request when proposing to merge your feature branch into a shared development or integration branch, ensuring review by relevant developers.**
- **Example**: To integrate your `feat/CRM-100-add-new-application-form` into the shared `sales-form-update-2025-06` development branch:
  1. **Create a Pull Request** on your Git hosting platform (e.g., GitHub, GitLab, Bitbucket):
     - **From branch (Compare)**: `feat/CRM-100-add-new-application-form`
     - **To branch (Base)**: `sales-form-update-2025-06`
     - **Title**: `feat(CRM-100): Add new application form for sales update`
     - **Description**:  
       This Pull Request implements the new application form as part of feature CRM-100, targeting the `sales-form-update-2025-06` branch.
       
       **Key contributions:**
       - Developed the user interface for the new application form.
       - Implemented comprehensive input validation for all fields.
       - Integrated form submission with the relevant backend APIs.
       
       **Testing:**
       - All automated tests (`npm run test`) are passing.
       - Manual testing scenarios, including valid/invalid inputs, required field validation, and form submission, have been thoroughly verified.
       
       This change addresses the requirements outlined in ticket CRM-100 and enhances the user experience for the sales application process.
  2. **Request Review**:
     - Assign relevant developers as reviewers. These are typically team members familiar with the `sales-form-update-2025-06` project or the CRM module.
  3. **Address Feedback Collaboratively**:
     - Engage in discussions on the Pull Request regarding any comments or suggestions.
     - Make necessary code revisions based on feedback and push these updates to your feature branch (`feat/CRM-100-add-new-application-form`). The Pull Request will update automatically with your new commits.
  4. **Merge After Approval**:
     - Once all feedback has been addressed and the Pull Request receives the necessary approvals from reviewers, it can be merged into the `sales-form-update-2025-06` branch by an authorized team member.


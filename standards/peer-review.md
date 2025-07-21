## PR Review Guidelines & Best Practices

These guidelines establish the principles and processes for Pull Request (PR) reviews. Following them ensures we maintain high code quality, share knowledge effectively, and foster a collaborative and supportive engineering culture.

All pull requests (PRs) **must** be reviewed by at least one other engineer before being merged. Exemptions to this rule require a specific, written policy agreed upon by the team and approved by an Engineering Manager or Director.

- **PR reviews are a core responsibility**
  This isn't an "extra" task; it's a fundamental part of every engineer's job, regardless of level. Actively participating in reviews is crucial for code quality, knowledge sharing, and team success.

- **Be timely & responsive**
  Prioritize reviews to keep the development flow moving. Aim for initial feedback within a **24-48 hour** timeframe. If you have thoughts but can't give a full review, consider setting up a 30-minute walk-through with the author. After you have pushed updates based on feedback, **re-request a review** from the original reviewers to notify them that the PR is ready for another look. This helps everyone track the status and keeps the process moving.

- **Be constructive & kind**
  Focus on the code, not the person. Frame feedback as suggestions ("What do you think about trying...?") and questions ("Is there a reason we chose this approach?"). Avoid demands. Use "we" or "us" language where appropriate to foster a sense of shared ownership.

- **Understand the goal**
  The PR author should provide a descriptive title and sufficient context in the PR description. As a reviewer, review the code against its stated purpose and acceptance criteria. Does the code achieve what it set out to do?

- **Check for clarity & maintainability**
  Is the code easy to understand? Are variable and function names clear? Will future developers be able to work with this? Look for opportunities to simplify, clarify, or refactor. Good code is not just clever; it's maintainable.

- **Verify functionality & tests**
  Does the code work as expected? Are there adequate tests covering new functionality and edge cases? When necessary, pull down the branch and run the code locally to verify its behavior.

- **Encourage small, focused PRs**
  Smaller PRs are easier and faster to review, lead to more thorough feedback, and reduce risk. Reviewers can and should request that large changes be broken down into smaller, logical PRs as a requirement for approval.

- **Use Draft PRs for early feedback**
  For work-in-progress, use GitHub's "Draft" status to signal that a PR is not yet ready for a formal review. This is a great way to get early feedback on an approach without blocking reviewers. Reviewers should provide feedback on Draft PRs but should not use the "Request Changes" option until the PR is marked "Ready for Review."

- **Approve when ready**
  Don't hold up a PR for minor, non-blocking nits once the core functionality and quality are solid. Clearly communicate if a PR is ready to merge or if further changes are required. As a critical quality gate, a PR **must not** be merged if a reviewer has formally requested changes. Once all required changes are addressed and approved, the PR can be merged.

- **Learn and share**
  Use reviews as a chance to learn new approaches or share knowledge. Code reviews are a key part of mentorship and career growth, happening across teams, titles, and levels of experience. More junior engineers can and should review more senior code and vice versa. Remember to point out excellent solutions, not just areas for improvement.

- **Automate where possible**
  Utilize linters, formatters, and CI/CD pipelines to automatically handle style, formatting, and other mundane checks. This frees up human reviewers to focus on what they do best: assessing logic, architecture, and maintainability. Teams are encouraged to use features like `CODEOWNERS` files to automate reviewer assignments.

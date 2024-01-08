# Summary
This file contains tips and tricks for using the stuff we have already set up on GitHub. It also contains some best practices.

# Pull requests
We use feature branching on the [code repo](https://github.com/lee-blake/Commitment-to-Change-App). **You should open a PR to `develop` under most circumstances.** All PRs to `master` should be releases from `develop` after more thorough testing.

## Opening PRs
If you are committing to one of our code repos, you should use one of our
[pull request templates](https://github.com/lee-blake/Commitment-to-Change-App/tree/master/.github/PULL_REQUEST_TEMPLATE) 
to make sure you have not forgotten anything in your write-up. 

### Using a PR template
First, begin opening a PR in the normal way. You then need to add the filename of the template to the URL as the `template` 
GET parameter.

Here is example with `generic_pull_request.md`. Before:
```
https://github.com/lee-blake/Commitment-to-Change-App/compare/modularity-examples?expand=1
```
After:
```
https://github.com/lee-blake/Commitment-to-Change-App/compare/modularity-examples?expand=1&template=generic_pull_request.md
```

Here is another example with `short_pr.md` where there are no parameters to start with. Before:
```
https://github.com/lee-blake/Commitment-to-Change-App/compare/modularity-examples
```
After:
```
https://github.com/lee-blake/Commitment-to-Change-App/compare/modularity-examples?template=short_pr.md
```

The PR will then autofill with the contents of the template file. Edit it as needed, providing all relevant information.

If you dislike this method, you can also copy and paste from the template file directly.

## Reviewing PRs
You should always perform a full code review when reviewing a PR. This includes both reviewing the code and testing 
it yourself. You can use the templates below to help cover everything.

**You should close PRs of a new feature directly to `master` without approval.** The PRs should be made to `develop` instead.

### Templates for reviews
Currently, there is no way to make a template for reviews to autofill. You can copy and paste the markdown below 
into your review to make sure you have a checklist.

#### For reviews on our code repos
```
# Checklist
- [ ] Tests pass on my machine
- [ ] Features work on my machine
- [ ] Features look okay on mobile using the following
  - [ ] Firefox/Gecko dev tools
  - [ ] Chrome/Chromium dev tools
  - [ ] Edge dev tools
  - [ ] Other (please specify)
- [ ] Code quality is good

# Changes requested
<!-- If you request changes, summarize them here. Otherwise delete this section. -->

# Comments
<!-- Put any additional comments you have here -->

<!-- You can always add more sections if you want to -->
```

## Merging PRs
It is fine to merge open PRs as long as they do not have a "do not merge" section and have passed review, with one caveat:

**Any pull request that has force-pushes or commits after a review should be re-reviewed.** An exception can be made if
the only commits are merging in changes from the branch it will be merged into.

# Git practices
Any specific practices for our repos should be documented here.

A nice cheat sheet exists [here](https://education.github.com/git-cheat-sheet-education.pdf).

## Rewriting history
This covers commands like `rebase` and `commit --amend`, as well as functionality from IDEs like squashing commits. The 
general rule is that it is rewriting history if it would require force-pushing to the repo if the branch was already 
pushed with the state that existed prior to executing the commands. 

Rewriting history is not prohibited, but you should follow the guidelines below

### The golden rule of rewriting history
If an idea *requires* force pushing, it is most likely a bad idea. Making another branch is preferable.

### Various scenarios
Here are some general guidelines for using these commands based on which situation you are in.

#### All rewritten history is local
If you are not changing anything that would affect the repo, there is no problem. It is still recommended that you create
a quick savepoint branch in case things go wrong. You should test your changes because rewriting history can break things.

#### A branch exists on the repo but is not an open PR
If you know someone else is working on it, do not rewrite history.

If you do not think anyone is working on it, you should check with everyone on Slack. In case someone is working on it
but does not see your message before you rewrite history, push to another branch instead of force pushing.

### A PR is open for the branch
Ideally, you should never have to do this because you should fix your history prior to opening a PR. However, if you
realize something after the fact, keep the following in mind: force pushing after a review will void the review, as well as 
make life harder for the reviewers. You should not force push open PRs. Push to a new branch and close your original PR. 
You should let everyone know on Slack in case they are reviewing your code. 

There is one scenario where force pushing to an open PR is acceptable: if you are using the open PR to test your changes
to the actions workflow, force pushing to keep an intellible history is okay. **Make sure you note that the PR is not ready
for reviews if you are going to do this.** 

### You are rewriting history that involves commits from other people
This already falls under one of the scenarios above, but additionally, you should not be rude in the way you rewrite
the history. Using `rebase` could result in giving you credit for someone else's work. Always check with that person
first and make sure they are one of the reviewers when you open a PR. 

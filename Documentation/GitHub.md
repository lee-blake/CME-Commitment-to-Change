# Summary
This file contains tips and tricks for using the stuff we have already set up on GitHub. It also contains some best practices.

# Pull requests
We use feature branching on the [code repo](https://github.com/lee-blake/Commitment-to-Change-App). Currently, you should 
open a PR to `master` for your feature, but this is likely to change to `develop` in the future.

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

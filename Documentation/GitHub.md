# Summary
This file contains tips and tricks for using the stuff we have already set up on GitHub. It also contains some best practices.

# Pull requests
We use feature branching on the code repo. Currently, you should open a PR to `master` for your feature, but this is 
likely to change to `develop` in the future.

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
https://github.com/lee-blake/Commitment-to-Change-App/compare/modularity-examples?template=generic_pull_request.md
```

The PR will then autofill with the contents of the template file. Edit it as needed, providing all relevant information.

If you dislike this method, you can also copy and paste from the template file directly.

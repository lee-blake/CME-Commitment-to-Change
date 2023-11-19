# How to Git

## Checking out a branch on the repo

1. `git checkout origin/repo-branch-name`
2. `git branch repo-branch-name`
3. `git checkout repo-branch-name`
4. Once your branch exists locally, future updates can be done by 
`git pull origin repo-branch-name`

## Pulling in changes from `master` for a pull request

1. Make sure you're on the right branch
2. `git pull origin master --rebase=false` to merge
3. If there are merge conflicts, git will let you know. Fix them
4. ***Retest your software.***
5. `git push origin master` if branch exists on the repo, else 
`git push origin master --set-upstream`
6. At this point your branch should be fully ahead of `master` and ready for a pull request.

# How to Docker

We're not done with this but here is some documentation:
- [https://wiki.archlinux.org/title/Docker](https://wiki.archlinux.org/title/Docker):
may not be entirely applicable to non-Arch systems but has some good recipes.
- [https://medium.com/@jonas.granlund/docker-essentials-building-and-running-your-first-container-47aff380b50b](https://medium.com/@jonas.granlund/docker-essentials-building-and-running-your-first-container-47aff380b50b)
- [https://medium.com/@jonas.granlund/running-django-with-postgresql-in-docker-a-step-by-step-guide-f6ab3bf05f44](https://medium.com/@jonas.granlund/running-django-with-postgresql-in-docker-a-step-by-step-guide-f6ab3bf05f44)

# How to use Pytest with Django
- Not just this page, but the site as a whole: https://pytest-django.readthedocs.io/en/latest/index.html
- https://djangostars.com/blog/django-pytest-testing/
- https://mattsegal.dev/django-with-pytest-on-github-actions.html
## (Important) General Django Test Features - check if supported in pytest
- https://docs.djangoproject.com/en/4.2/topics/testing/tools/#email-services

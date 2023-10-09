# Project Tech Stack

This file details the tech stack chosen for the CME Commitment to Change project.

## General Constraints

Per our meeting with the client, our choice of tech stack is free so long as it meets the following requirements:

1. The project will deliver a web application that is responsive on desktop, tablet, and mobile devices.

2. The tech stack should be deployable to the cloud as that is preferred to server hosting.

3. The tech stack should scale well with larger numbers of users.

## Content Delivery/Web Server: [Django](https://www.djangoproject.com/start/overview/)

Django is a well-established web server framework in Python. Our mentor recommended a server in either Python or PHP. We chose Python since it is a language our team has significantly more experience in. Django is a proven Python server technology with a large community, which means that documentation, tutorials, and support are all readily available. Crucially, both AWS and Azure both have significant documentation for cloud deployment of Django servers. Additionally, Django's template engine and built-in authentication system should improve the speed of development.

## Business Logic: [Python](https://www.python.org/)

One advantage to using a Python-based web server over a PHP server is that both the server and business logic code can be written in the same language. Since Python is one of the languages our team is more familiar with, we should have a significantly easier time getting the project off the ground than if we were to choose something few of us had encountered. With support for object-oriented programming paradigms, extensive documentation and tutorials, and vast libraries of plugins, Python should be a solid choice for our business logic.

## Unit Testing: [Pytest](https://docs.pytest.org/en/7.4.x/)

`pytest` is a framework for unit tests in Python. It has three main advantages over the JUnit-style `unittest` module. First, it allows the writing of more 'pythonic' tests, which makes for more readable testing code. Second, it has automatic test discovery, which makes writing testing scripts much easier. Finally, the support for test fixtures is more flexible and module than in `unittest` as it is based on annotations, rather than on specific method-name conventions.

## Database: [PostgreSQL](https://www.postgresql.org/)

PostgreSQL is an open-source SQL database system. It is widely used and was one of the databases recommended by our mentor. Crucially, PostgreSQL is well-documented for both AWS and Azure. Futhermore, it has horizontal scaling features that have an especially good track record for read scaling, which is likely to be the primary database scaling difficulty on a commitment-based social media platform. Finally, the longstanding cross-platform support for PostgreSQL will enable all team members to use it with few (technical) difficulties.

## Frontend: [Bootstrap](https://getbootstrap.com/)

Bootstrap is a CSS and Javascript framework that allows websites to scale well across for devices from desktop to mobile phones. Our mentor highly recommended it for responsive mobile design. Bootstrap speeds CSS development using SASS. Additionally, it can automate many JS behaviors using HTML data attributes. Bootstrap also works with jQuery, which will be important if we find that much of our frontend development could be sped up with jQuery. Bootstrap should enable us to design for different devices in an efficient and robust manner.

## Cloud deployment: [AWS](https://aws.amazon.com/console/) or [Azure](https://azure.microsoft.com/en-us)

Both of these environments are well-documented and established. As the client has no preference, and as our tech stack should support either cloud computing environment, the choice between the two rests on which system is more comfortable for the team to use. We have elected to defer this decision until we have experimented with deployment on both platforms.

## SMTP Server: [Gmail SMTP](https://support.google.com/a/answer/176600?hl=en)

Gmail has a SMTP server and you can send 100 messages per day with a free account. The process is basically identical to that described in the link, but with lower numbers. For development and early deployment, this amount should be adequate with minimal setup required. However, we do need to be mindful of this low limit and find another solution as the platform is growing but before the limit is reached. One contingency we have for an explosion in numbers is Amazon's SES, which features linear scaling of cost with usage, and therefore serves well as a way to maintain service for a short period of exploring alternatives.

## Backend IDE: [PyCharm](https://www.jetbrains.com/pycharm/)

PyCharm is an IDE for Python. While the professional version has a number of tools that might be helpful for our project, we plan on proceeding with the free community version. PyCharm is from the same developer as IntelliJ and has a similar layout. This should enable team members who have not used to before to adapt to it with relative ease. PyCharm has extensive plugin support and Python package/dependency management tools.

## Frontend IDE: [VSCode](https://code.visualstudio.com/)

VSCode is a much broader IDE that supports languages via extensions. Given the many languages involved in even our relatively basic frontend stack, this will be an advantage, as we can support any new additions simply by installing a respective language plugin. VSCode is cross-platform and has an open-source MIT licensed version, so all team members should be able to use it.


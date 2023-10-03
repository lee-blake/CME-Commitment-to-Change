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

## Unit Testing:

<!-- TODO decide between unittest and pytest -->

## Database: [PostgreSQL](https://www.postgresql.org/)

PostgreSQL is an open-source SQL database system. It is widely used and was one of the databases recommended by our mentor. Crucially, PostgreSQL is well-documented for both AWS and Azure. Futhermore, it has horizontal scaling features that have an especially good track record for read scaling, which is likely to be the primary database scaling difficulty on a commitment-based social media platform. Finally, the longstanding cross-platform support for PostgreSQL will enable all team members to use it with few (technical) difficulties.

## Frontend: [Bootstrap](https://getbootstrap.com/)

Bootstrap is a CSS and Javascript framework that allows websites to scale well across for devices from desktop to mobile phones. Our mentor highly recommended it for responsive mobile design. Bootstrap speeds CSS development using SASS. Additionally, it can automate many JS behaviors using HTML data attributes. Bootstrap also works with jQuery, which will be important if we find that much of our frontend development could be sped up with jQuery. Bootstrap should enable us to design for different devices in an efficient and robust manner.

## Cloud deployment: 

<!-- TODO wait for response on whether we can list both AWS and Azure -->

## Backend IDE: [PyCharm](https://www.jetbrains.com/pycharm/)

PyCharm is an IDE for Python. While the professional version has a number of tools that might be helpful for our project, we plan on proceeding with the free community version. PyCharm is from the same developer as IntelliJ and has a similar layout. This should enable team members who have not used to before to adapt to it with relative ease. PyCharm has extensive plugin support and Python package/dependency management tools.

## Frontend IDE: [VSCode](https://code.visualstudio.com/)

VSCode is a much broader IDE that supports languages via extensions. Given the many languages involved in even our relatively basic frontend stack, this will be an advantage, as we can support any new additions simply by installing a respective language plugin. VSCode is cross-platform and has an open-source MIT licensed version, so all team members should be able to use it.

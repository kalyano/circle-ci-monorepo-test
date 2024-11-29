# CircleCI Path Filtering Setup for Monorepo

This repository contains a CircleCI configuration for triggering specific workflows based on file changes in a monorepo. The setup uses the path-filtering orb to dynamically determine which workflows to execute based on the paths modified in a commit.

**Overview**

In a monorepo setup, you may want to:

	•	Build only the project(s) affected by recent changes.
	•	Avoid running unnecessary workflows for unrelated changes.

This configuration achieves the above using:

	•	Path Filtering Orb: Dynamically detects file changes and triggers the appropriate workflows.
	•	Dynamic Configuration: Utilizes continue_config.yml to load workflows and jobs based on the changes.

**Repository Structure**

```bash
.
├── .circleci
│   ├── config.yml          # Main CircleCI configuration file
│   ├── continue_config.yml # Continuation configuration file
├── project1/
├── project2/
├── shared/
└── README.md
```

- config.yml:
    - Main CircleCI configuration file
    - Detects changes via the path-filtering orb 
    - Dynamically triggers the continuation configuration (continue_config.yml)
- continue_config.yml:
    - Defines workflows and jobs for specific parts of the monorepo
    - Includes conditional logic to execute jobs only for affected projects
- project1/, project2/, shared/:
    - Example folders representing distinct projects and shared code in the monorepo
 
## Dependencies
- [CircleCI Path Filtering Orb](https://circleci.com/developer/orbs/orb/circleci/path-filtering)
- Docker Image:
    - The jobs use the circleci/node:14 image
 
## Setting Up

1. Fork or Clone the Repository:
```bash
git clone https://github.com/kalyano/circle-ci-monorepo-test.git
cd your-repo
```

2. Login to CircleCI & add this repo to your projects

3. Trigger builds by making changes to the repo files in "project1/, project2/, shared/"

4. Examine the CircleCI pipeline to view the extra build options depending on which folder was modified

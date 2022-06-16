# Pipeline process
For this project, we used CircleCI's pipeline as a service. To use the pipeline of CircleCI we did the following:
- Sign in CircleCI using the GitHub account, so that every time we push to GitHub the project is built and deployed.
- From `Projects` we click `Setup Project` for udagram.
- We create the `.circleci/config.yml` file in the root of the project.

## .circleci/config.yml
The pipeline uses the following orbs:
- `circleci/node@5.0.2`
- `circleci/aws-cli@3.1.1`
- 
The pipeline has one workflow, `build-and-deploy` which has two jobs `build` and `deploy` run in sequence.

### build job
The `build` job consists of the following basic steps:
1. The `checkout` step to clone the source code and use it in the next steps.
2. Install node version 16.3.
3. install backend/frontend dependencies.
4. Build backend then frontend.
5. Persist to the workspace to use in the `deploy` job.

### deploy job
The `deploy` job goes like the following:
1. Attach workspace from the previous job.
2. Setup AWS CLI.
3. Deploy the backend.
4. Deploy the frontend.

## Resources
- [circleci/node@5.0.2](https://circleci.com/developer/orbs/orb/circleci/node)
- [circleci/aws-cli@3.1.1](https://circleci.com/developer/orbs/orb/circleci/aws-cli)
- [circleci/aws-elastic-beanstalk@2.0.1](https://circleci.com/developer/orbs/orb/circleci/aws-elastic-beanstalk)
- [Sharing code checkout step between jobs](https://discuss.circleci.com/t/sharing-code-checkout-step-between-jobs/29918/2)

## Author
- Shorouk Elkhateeb
# Project Setup Checklist

Checklist for setting up the GitHub repository, Heroku, and other integrations when starting a new project.

This checklist assumes that the new repo was created using `client-template`.

## GitHub

- [ ] Create a new repo in GitHub under the LaunchPad organization (do not initialize with a README)
- [ ] Add the repo as origin (following [GitHub's instructions](https://help.github.com/en/articles/adding-a-remote)) and push the initial commit from the template

### Settings

#### Options

- [ ] Only allow squash and merge behavior by **unchecking** both "allow merge commits" and also "allow rebase merging"
- [ ] Check "automatically delete head branches"

#### Branches

- [ ] Create `dev` and `staging` branches from `main`
- [ ] Set default branch to `dev`
- [ ] Protect `main`, `staging`, and `dev` branches:
  - [ ] Require pull request reviews before merging
  - [ ] Require status checks to pass before merging

#### Collaborators

- [ ] Grant the `LPL` team write access to the repository

## Integrations

### Sentry
Sentry is a platform that provides error and performance monitoring. At LPL, we virtually always leverage just the error monitoring functionality in favor of other tooling (e.g., Heroku, New Relic).

- [ ] Create a new `React` project (add to LaunchPad Lab team) in [Sentry.io](https://sentry.io/organizations/launchpad-lab/projects)
- [ ] Add Sentry DSN to `application.yml` as `REACT_APP_SENTRY_URL` under `production`
  - [ ] If this file doesn't exist, follow [these instructions](https://github.com/LaunchPadLab/opensesame#opensesame)

### Travis
Travis CI is a continuous integration platform that supports development processes by automatically building and testing code changes.

- [ ] Confirm that repo has been added to [Travis CI](https://travis-ci.com/github/LaunchPadLab)
- [ ] Add any required env vars to travis (as defined in `config/figaro.js` initializer)

## Heroku

### Create New

- [ ] Create pipeline
- [ ] (Optional) Add `<APP_NAME>-client-development` app to pipeline in `development` stage (creating this stage requires an [extra step](https://devcenter.heroku.com/articles/pipelines#i-don-t-see-a-development-stage-how-do-i-add-a-development-app))
  - [ ] Set to automatically deploy on push to `dev` branch
- [ ] Add `<APP_NAME>-client-staging` environment app to pipeline
  - [ ] Set to automatically deploy on push to `staging`
- [ ] Add `<APP_NAME>-client-production` environment app to pipeline `production` stage
  - [ ] Set to automatically deploy on push to `main` (Require CI to pass)
- [ ] Enable Review Apps for pipeline
  - [ ] Automatically create review apps for new PRs
  - [ ] Destroy stale review apps automatically after 5 days
  - [ ] Under more settings, configure app config vars for all reviews apps to inherit from

### Access

- [ ] Add admins and collaborators to Heroku pipeline as needed

### Settings

- [ ] Add config vars from `application.yml` to the respective environment app (`figaro-js` provides [built-in functionality](https://github.com/LaunchPadLab/figaro-js/blob/master/docs.md#cli) for this)
- [ ] Optional: Add Heroku remotes for local branches (`git remote add dev <https:…>`). Git URLs may be found in the Info section of each app's Settings tab.

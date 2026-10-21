# renovate-47268-silent-dashboard

Reproduction for https://github.com/renovatebot/renovate/issues/47268: with `mode=silent`, Renovate still acts on checkboxes ticked on an existing Dependency Dashboard.

## Steps

1. Run Renovate with `"mode": "full"` and `dependencyDashboardApproval`: it creates the Dependency Dashboard (#1)
1. Tick the `lodash` approval checkbox on the dashboard
1. Switch to `"mode": "silent"` (commit `fd33c0f`)
1. Run Renovate again

## Result

- `main` (8ca0feca4c): logs `dependencyDashboardCheck=approve` and `Branch created`, and opens PR #2, although `mode=silent` should neither create branches nor PRs
- Fix branch (renovatebot/renovate#47271): logs `Ignoring Dependency Dashboard checkboxes when mode=silent` and `Branch renovate/lodash-4.x creation is disabled because mode=silent`

The PR rebase checkbox on #2 was also ticked and Renovate run with `mode=silent`: the branch was rebased once and the checkbox unticked, so it does not loop.

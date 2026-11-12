# Publishing TaskTuning on GitHub and AtomGit

Keep the Python package `task_tuning`, the `task-tuning` CLI, and the reviewed
source history consistent across hosting platforms.

The project repositories are:

- [GitHub](https://github.com/SamdianJ/TaskTuning)
- [AtomGit](https://atomgit.com/SamiulJ/tasktuning)

## Validate the release commit

Run the checks in [CONTRIBUTING.md](../CONTRIBUTING.md), including both synthetic
demos and an installed-wheel smoke test. Check README links and the local HTML
report navigation. Preserve the evidence and historical acceptance outcomes.

Record the selected commit with `git rev-parse HEAD`. Check that package metadata,
the English and Chinese READMEs, and the cable setup instructions agree about
dependencies. Core tests and archive verification do not validate a new Newton
runtime.

## Synchronize the repository

For an initial copy, AtomGit supports importing an external Git repository by URL.
Its import documentation states that Wiki pages, issues, pull requests, and releases
are not included in the Git repository migration. See the
[AtomGit import guide](https://docs.atomgit.com/en/docs/help/home/org_project/project_manage/getting_started/project_creation_and_import/).

For subsequent updates, keep one reviewed source branch and publish its selected
commit to both repositories. Inspect `git remote -v` and the destination branches
before pushing. In a checkout whose `origin` is the GitHub project, add the second
remote once:

```bash
git remote add atomgit https://atomgit.com/SamiulJ/tasktuning.git
```

After the reviewed changes have landed on GitHub `main`:

```bash
git fetch origin main
git push atomgit FETCH_HEAD:refs/heads/main
git ls-remote origin refs/heads/main
git ls-remote atomgit refs/heads/main
```

The two `main` references should identify the same commit. If a push is rejected
because AtomGit contains additional commits, fetch and review them before merging
or retrying. Synchronize release tags explicitly when needed; avoid publishing
unrelated development branches with a blanket mirror push.

AtomGit also offers [repository mirroring](https://docs.atomgit.com/docs/help/home/org_project/project_manage/project_settings/repository_mirroring/).
If maintainers enable it, choose one authoritative source and configure one-way
synchronization. No automatic mirror or credentials are configured by this repository.

## CI and reports

The existing `.github/workflows/ci.yml` defines GitHub CPU checks. Copying the Git
repository does not demonstrate that AtomGit has executed those checks. Configure
and verify an AtomGit pipeline separately if checks are required on that platform,
or run the documented commands against the exact published commit.

HTML reports and their source evidence are bundled. Follow the
[local preview instructions](publishing-results.md) to view them after cloning from
either host. A hosted report site requires a separate publishing configuration.

Redistribute `LICENSE`, `LICENSE-DOCS`, `NOTICE`, and the Newton patch's original
license together with the corresponding files. Keep third-party notices intact.

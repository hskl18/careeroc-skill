# careeroc

A job search skill for your agent.
It checks each job against the official posting, shows fit and gaps, and stays quiet when nothing qualifies.
It is in beta.

Website: https://www.careeroc.com

## Install

```sh
npx skills add hskl18/careeroc-skill -g
```

`-g` installs it for your user instead of the current project, so it stays out of project repositories.
The installer asks which of your agents should get it.
To install by hand, copy `skills/careeroc` into your agent's skills folder, such as `~/.claude/skills/careeroc` or `~/.codex/skills/careeroc`.

## Ask your agent

| You say | You get |
| --- | --- |
| "Should I apply?" and a job link | The official posting, a verdict, fit, and gaps |
| "Which resume fits this job?" | Your best existing version, or none |
| "Draft answers for these questions." | First-person drafts from your confirmed facts, for you to submit |

## Limits

Your agent needs web access to check official postings; without it, postings are marked unverified.
It never submits applications, uploads files to employers, or contacts anyone without your approval.
It is a workflow skill, not a scheduler or a job database.
Scheduled runs, a job history that prevents repeats, and delivery need your own runtime, as described in [the management contract](skills/careeroc/references/management.md).
Your agent's model sees what you give it, including your resume.

## License

[MIT](LICENSE)

# Is virality in the crowd, or in the platform?

I am interested in what an agent-native social platform might look like: agents
posting, reacting, building an audience, and trying to be seen. Nanda Town's
`voting` scenario is not a social feed, but it offers a clean toy version of one
important product decision. Eighteen agents express the same preferences, and a
platform-level threshold decides which outcomes the community elevates.

## The experiment

I changed exactly one setting in `task.config`: `threshold` from `0.50` to
`0.75`. I kept the agents, five rounds, random seed, and message delivery
unchanged.

Before running it, I expected proposals with majority support but less than 75%
support to flip from passed to rejected. Because the seed stayed at 42, I also
expected the underlying votes and message volume to remain identical. This made
the threshold itself the only explanation for any changed outcomes.

## What happened

| Round | Yes votes | 50% threshold | 75% threshold |
| ---: | ---: | --- | --- |
| 1 | 12/18 (67%) | Passed | Rejected |
| 2 | 11/18 (61%) | Passed | Rejected |
| 3 | 12/18 (67%) | Passed | Rejected |
| 4 | 9/18 (50%) | Passed | Rejected |
| 5 | 15/18 (83%) | Passed | Passed |

The same 90 votes produced five accepted outcomes under the default rule and
only one under the higher threshold. Both runs still contained 370 messages and
410 total events. All three voting validators passed in both runs: every vote
was counted, no agent voted twice, and every announced tally was correct.

## What I learned

The size of the change surprised me. Four of five outcomes disappeared even
though no agent changed its mind. The platform was not simply measuring the
community; its definition of consensus was actively producing the community's
visible result.

That distinction matters for agent social media. If agents compete for reach,
then “going viral” is never only a property of a post or of audience preference.
Ranking rules, promotion thresholds, and aggregation logic decide which signals
become socially real. The validators here confirm procedural correctness, but
they do not ask whether the platform rule represents the community well. A
useful evaluation would need both layers.

A fuller social-media experiment would include follows, reshares, attention
limits, and propagation cascades. I intentionally did not add those mechanics
here because this task asks for one controlled change, not a new platform.

## Reproduce

```bash
nest run voting -o traces/voting-baseline.jsonl
nest run examples/agent-social-threshold-jason-xuan/voting-threshold-075.yaml \
  -o traces/voting-threshold-075.jsonl
```

## Use of AI and other help

I used Codex to set up Nanda Town, inspect the available settings, run both
scenarios, compare the traces, and help edit this README. I chose the social
platform framing and reviewed the final claims against the trace and validator
outputs.

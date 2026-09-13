# Hackathon operating constraints

**Status:** canonical external constraints

**Official source:** [Nebius x NVIDIA Global AI Hackathon 2026 rules](https://nebiusglobalaihackathon.devpost.com/rules)
**Last verified:** 2026-09-13

This is an operational digest, not a substitute for the rules. Re-verify before major architecture commitments and submission.

## Dates

| Official requirement | Team implication |
|---|---|
| Build/submission period: **2026-08-26 09:00 PT → 2026-10-30 10:00 PT** | Submit before the Devpost deadline; record what was built during the eligible period. Confirm local-time conversion near submission. |
| Judging: **2026-12-01 09:00 PT → 2026-12-15 12:00 PT** | Keep the demo/test build available, functional, free, and unrestricted through judging. |
| Winners announced around **2027-01-11 12:00 PT** | No architecture effect. |

## Product and technology

| Official requirement | Team interpretation / implication |
|---|---|
| Create a working software application that runs on **Nebius Token Factory or Nebius AI Cloud**, uses at least one **NVIDIA open-source model**, and fits one track. | Nebius and NVIDIA must be functional runtime dependencies, not logos or offline claims. Capture calls/deployment and model identifiers in the demo and repository. |
| “Runs on” means a runtime Token Factory inference API call, or deployment/execution on AI Cloud compute through Serverless Jobs, Serverless Endpoints, or DevPods. | Choose at least one qualifying path and make it reproducible. A local-only prototype using neither path is ineligible. |
| Coding and Agentic Engineering: build coding agents/developer tools—agents that write, run, and test code in Token Factory Sandboxes. | For this track, the end-to-end demo should visibly connect developer value, model behavior, code action, Sandbox execution, and test/verification evidence. The harness or sandbox alone is not the product thesis. |
| The application must install/run consistently and behave as shown/described. | Maintain one reliable judge path; rehearse from clean setup and keep graceful failure diagnostics. |
| A pre-existing project must be significantly updated after the submission period starts, with the update explained. | Treat this repository's dated history and ADRs as provenance. Document any imported pre-existing component and the hackathon work. |
| Third-party SDK/API/data use must be authorized and license-compliant; the submission must be original, owned by entrants, and non-infringing. | Track licenses and data rights from the first dependency/fixture. Do not include unlicensed demo media or private code/data. |

## Submission package

- A URL to a working hosted demo, application, or test build.
- A public GitHub, GitLab, or Bitbucket repository containing all necessary source, assets, setup instructions, and run guidance.
- A visible open-source license (examples in the rules: Apache-2.0, MIT, MPL-2.0). **License choice is still undecided and must be made before submission.**
- README coverage that highlights the NVIDIA open-source model(s), Token Factory acceleration/use, and any other Nebius services.
- A public YouTube demo video **under three minutes** showing the functioning product on its intended device. Judges need not watch beyond three minutes.
- An English description of features/functionality, selected track, testing instructions/credentials if private, and English translations for any non-English material.
- Feedback on the Nebius and NVIDIA technologies used.
- If applicable, a written account of significant changes to a pre-existing project.

Do not put real secrets in the public repository or video. Provide judge access by a controlled mechanism and verify it from a logged-out environment.

## Judging

**Stage 1 — pass/fail:** genuine fit to the selected track and meaningful use of required APIs/SDKs; a superficial rebrand fails.

**Stage 2 — equally weighted:**

1. **Technological implementation:** build quality and effective Nebius/NVIDIA use.
2. **Design:** complete, coherent product experience rather than only a technical proof of concept.
3. **Potential impact:** credible real problem, real audience, and demonstrated solution.
4. **Quality of idea:** creative, non-obvious technology use and real domain understanding.

**Team implication:** evaluation and demo planning must cover all four dimensions. Technical novelty cannot compensate for a missing user/problem or incoherent product.

## Eligibility and administration

- Each participant must be at least the age of majority where they reside and not fall into excluded jurisdictions, organizational conflicts, or other disqualifying categories in the rules. Each member must verify their own eligibility; this digest does not make a legal determination.
- A team must appoint one authorized representative to submit and, if applicable, receive/allocate a prize.
- Register/join on Devpost and complete every required submission field during the submission period.
- The project must remain accessible for testing until judging ends; judges may instead rely only on description, images, and video.
- Submission edits generally stop when the submission period closes, aside from limited administrator-approved corrections.

## Pre-submission gate

- [ ] Re-verify the official rules and deadline.
- [ ] Confirm every member's eligibility and the team representative.
- [ ] Demonstrate qualifying Nebius runtime use and identify the NVIDIA open-source model.
- [ ] Validate clean install/run and judge access through the end of judging.
- [ ] Add the selected open-source license and complete public-repo instructions.
- [ ] Verify third-party code, data, media, trademarks, and credentials.
- [ ] Record reproducible evaluation evidence under [`../app/evals/`](../app/evals/README.md).
- [ ] Publish and test a public YouTube video under three minutes.
- [ ] Complete English description, technology feedback, track, and any prior-project disclosure.

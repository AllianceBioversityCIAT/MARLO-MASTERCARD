# Repository Identity — MARLO-MASTERCARD

Read this before reasoning about programs, terminology or deployments in this checkout. Most documentation in this
repository is inherited unchanged from `CCAFS/MARLO`, whose examples come from AICCRA. **This repository does not
serve AICCRA.**

---

## 1. What this repository is

| Item | Value |
|---|---|
| Repository | `AllianceBioversityCIAT/MARLO-MASTERCARD` |
| Relationship | Fork of `CCAFS/MARLO` (remote `upstream`). Product changes land first in `CCAFS/MARLO` `staging` and arrive here by merging `upstream/staging` into this repository's `staging` |
| Program served | **REAP** (Mastercard Foundation) |
| Global Unit | Name **REAP - Mastercard Foundation**, acronym **`REAP-MCF`** |
| `crp_custom_file` | **`reap`** → labels come from `marlo-web/src/main/resources/custom/reap.properties` on top of `global.properties` |

---

## 2. Terminology

`custom/reap.properties` is currently a copy of `custom/aiccra3.properties`, so REAP uses the same labels as AICCRA 3:

| Internal name (code / data) | Shown in REAP |
|---|---|
| `Project` | Technical Implementation Team |
| `CrpProgram` (flagship) | Component |
| Flagship leader role | Component Leader |
| PMU / program management role | Secretariat / PIU |
| `CrpMilestone` | Year Target |
| `GlobalUnit` (plural label) | PTFs |
| Impact Pathway section | Overall Performance Indicators |

The full matrix and the traps (for example, *Cluster of Activities* is a different entity from `Project`) are in
[`docs/glossary.md`](./docs/glossary.md).

- When the inherited docs say *Cluster* or *Cluster Coordinator*, read *Project* / *Project Coordinator*; REAP shows
  it as *Technical Implementation Team*.
- Texts in `reap.properties` that mention AICCRA by name are inherited from the copy and have not been adapted to
  REAP yet.
- `reap.properties` is maintained in `CCAFS/MARLO`; it does not follow later changes to `aiccra3.properties`
  automatically.

---

## 3. Branches and deployment

| Branch | A push triggers | Effect |
|---|---|---|
| `staging` | `reap-staging-ci.yml` | CI only: image build (not published), Jenkins verification, Slack. **No deploy** |
| `main` | `reap-prod-ci.yml` (`dry-run: false`) | **Real REAP production deploy** (ECR `marloreap-app-prod`, Jenkins `marlo-reap-main-cd`) |

- Merge `upstream/staging` into **`staging`**, never into `main`. `main` only moves when `staging` is promoted.
- The `marlo-*.yml` and `jenkins-trigger-java-*.yml` workflows arrive with the `CCAFS/MARLO` merges and belong to
  CCAFS/MARLO; they are disabled in this repository's Actions settings. This repository deploys REAP only.
- Any change to `global.properties` or `custom/*.properties` needs an application restart after deploy.

---

## 4. Keeping this file current

- This file exists only in this fork: `CCAFS/MARLO` never has it, so upstream merges never conflict with it.
- Update it when the Global Unit, `crp_custom_file`, the deployment workflows or REAP's terminology change.
- Do not copy it into `CCAFS/MARLO` or other forks: each fork documents only its own program.

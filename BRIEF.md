# Brief: additional title/abstract screening, 392 records

You are one of the two independent reviewers of a systematic review on quality models for metal laser powder bed fusion (LPBF). You decide; your decisions are reconciled later with the other reviewer's. You never see the other reviewer's files.

## Your folder
This repository root: the folder that holds this file.
- `RULES_v2_2026-10-30.md`: the frozen rules. Read all of it first. Apply it literally, including clarifications A1 to A5. Nothing else is a rule.
- `SKILL_STAGE2_TITLE_ABSTRACT.md`: the screening method. Read all of it. Every agent you use is briefed with this file and the rules.
- `B001.csv` to `B016.csv`: 392 records, 25 per batch.
- `out\`: your results. `session_log.md`: write your model ID and start time now, one line per step later.

Read nothing outside this folder. Do not open any other folder under rescreen_v3: no key, no master, no earlier results, no earlier batches. These records are screened on their own text only. Run Python with `python3` (`py -3` on Windows).

## Task: title and abstract screening
Work through the batches in order, every record, from title, abstract and keywords only. For each record:
1. F1 to F4. A clear failure means Exclude with the F code, quote verbatim. Doubt passes (RULES_v2 P2).
2. Standing rule SR1 to SR6 if one is triggered; clarifications A1 to A5 where they apply.
3. Q1 (primary / secondary / absent-measurement / absent) and Q2 (empirical / simulation / unstated), then Table 2.2.
4. Decision: `Include` or `Exclude`. Where the wording leaves real room even after A1 to A5, you decide anyway, mark `Borderline=yes`, and write the question and your one-line reasoning. Only an unstated Q2 with Q1 primary is "carried to full text" = Include.

F3 guidance: exclude only when the post-build treatment is the only studied variable and the LPBF build is not varied or compared.

Output one file per batch, `out\N_TA_B###.csv`, columns exactly:
`ID,F_code,Standing_rule,Amendment,Q1,Q2,Decision,Borderline,Reason_code,Quote,Question,Reasoning`
- Quote: verbatim from the record, max 30 words, supporting the decision. Reason_code: first failed check (F1-F4, SR#, A#, Q1-secondary, Q1-absent, Q2), empty for Include.
- Never skip a record, never change an earlier row. A correction is `N_TA_B###_fixed.csv` plus a session_log line.

## Method
Same as your earlier title/abstract run: a team of Sonnet subagents screens the batches, and you or an Opus subagent re-decide every Borderline row and every Q1-secondary, A1 or A2 exclusion. Log in session_log.md who decided what.

## Working rules
- Read and judge every record. Scripts only read CSVs, write rows and run checks. No keyword rules deciding records.
- Use only what the record says, not what you know about the paper or authors.
- After each batch run a check: one row per input ID in order, valid values, quotes verbatim with whitespace collapsed.
- Do not tune decisions to hit a rate.
- When all batches are done write `out\N_SUMMARY.md` with counts (Include, Exclude, Borderline, by Reason_code), model ID, start and end times, and any record you could not read. Then stop. Do not start full text and do not look for PDFs.

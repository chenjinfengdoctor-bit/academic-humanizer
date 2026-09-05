---
name: academic-humanizer
version: 0.4.1-medical
description: |
  Improve the clarity and voice of AI-assisted academic writing (papers, theses, rebuttals) and
  funding proposals (NSF Project Summary/Description, NIH Specific Aims): preserve scholarly
  conventions, match claims to evidence (and, for proposals, claims to feasibility), and match the
  author's own voice. Includes a medical/clinical adaptation layer (Layer 7) enforcing CONSORT/STROBE/TRIPOD
  reporting discipline, precise medical terminology, mandatory methods-element checks (ethics approval,
  informed consent, follow-up duration, sample size justification), and specialty-specific terminology
  for oncology, respirology/pulmonology, and nanomedicine. It never changes a number, result, or
  citation, and it is not for evading AI-use disclosure. Use when editing AI-assisted academic prose or
  grant proposals.
license: MIT
compatibility: claude-code codex morphmind opencode
allowed-tools: [Read, Write, Edit, Grep, Glob, AskUserQuestion]
---

# Academic Humanizer

Improve the clarity and voice of AI-assisted *academic* writing while keeping the precise,
evidence-bound voice that scholarship requires and matching the author's own style. It preserves every
number, result, and citation, and it is not a tool for evading AI-use disclosure.

## When to use
Editing or reviewing academic prose: paper sections, abstracts, rebuttals, related work, and **funding
proposals** (NSF Project Summary/Description, NIH Specific Aims, fellowship and foundation proposals;
see Layer 6). For medical/clinical manuscripts, also apply Layer 7. **Not** for blogs, marketing, or
personal essays, and **never** inject opinion, humor, or first-person "personality" into a manuscript.
For technical writing, neutral and precise *is* the human voice. One caveat for proposals: their register
is different from a paper's, since they are sold on vision and feasibility, so the ambition language a
paper would trim is appropriate there; apply Layer 6, not the paper layers' stricter trimming, to vision
statements.

## Core principle
Academic writing already has a correct human voice: neutral, precise, third-person plural ("we"), every
claim tied to its evidence. The job is to (1) strip the AI *tells* without casualizing, and (2) enforce
the discipline a general humanizer misses: **every claim earns its number, figure, or citation, and no
verb is stronger than its evidence.**

## Process
1. **Read** the manuscript and any author writing sample; note the document type (paper vs. funding
   proposal) and the target venue or funding agency. For proposals, also apply Layer 6 and preserve
   appropriate vision. For medical/clinical work, also apply Layer 7.
2. **Audit** (do not edit yet): list each detected pattern with its location and proposed fix, and each
   empirical claim's evidence status. For medical papers, also run the mandatory methods-element checklist
   (7.4) and flag any missing item.
3. **Rewrite**: same structure and content, all claims and citations preserved, tells removed, over-claims
   matched to evidence, legitimate hedging kept.
4. **Report**: cleaned text plus a short change log (patterns removed, claims softened or given evidence
   pointers, voice notes, and—for medical papers—any missing methods elements flagged for the author).
   Cover everything the original covered: if it had five paragraphs, so does the rewrite.

---

## Layer 1: General AI-tell catalog
Scan for and fix the general patterns, subject to the academic exceptions in Layer 3:
inflated significance ("marking a pivotal moment"); superficial "-ing" tails that fake depth
("..., highlighting..."); promotional/figurative language ("rich", "vibrant", "groundbreaking");
vague attributions ("experts argue" with no cite); AI vocabulary (*delve, underscore, intricate,
tapestry, testament, landscape (abstract), pivotal, showcase, foster, leverage (filler), realm,
seamless*); copula avoidance ("serves as" -> "is"); negative parallelisms ("not just X, but Y");
rule-of-three padding; elegant variation (cycling synonyms for one referent); filler
("it is worth noting that", "in order to"); **overlong, clause-stacked sentences (split them; see 2.11)**;
and **em-dashes (remove entirely; recast with commas, colons, parentheses, or separate sentences)**.

**Before:** *Additionally, an enduring testament to the method's value is its ability to delve into
intricate dependencies, showcasing a seamless integration that underscores its pivotal role.*
**After:** *The method also captures higher-order dependencies, which the baselines miss (Table 2).*

---

## Layer 2: Academic AI tells (remove or fix)

### 2.1 Over-claiming verbs
Empirical work *shows* and *provides evidence*; it does not *prove* or *demonstrate* universal truths.
**Watch:** demonstrate, prove, establish, confirm, guarantee; "significantly" with no test/number.
**Before:** *We prove that our method significantly outperforms all prior approaches.*
**After:** *Our method improves held-out accuracy by 4--7 points over the strongest prior approach
(Table 3); the gain is significant at p < 0.01 by a paired test.*

### 2.2 Significance hype
**Watch:** paves the way for, a crucial/pivotal step toward, has the potential to revolutionize, opens
new avenues, sheds light on, of paramount importance, bridges the gap.
**Before:** *This work paves the way for a new paradigm and sheds light on a problem of paramount
importance.*
**After:** *This work addresses one failure mode of prior methods: error accumulation under long-horizon
rollout (Section 4).*

### 2.3 Empty intensifiers
**Watch:** extensive/comprehensive/thorough experiments, a wide range of, numerous, various.
**Before:** *We conduct extensive experiments on a wide range of datasets.*
**After:** *We evaluate on three datasets (ImageNet, CIFAR-100, and iNaturalist).*

### 2.4 Novelty padding
**Watch:** "novel" used more than once per section; "to the best of our knowledge"; "for the first time".
**Before:** *We propose a novel framework and, to the best of our knowledge, are the first to study this.*
**After:** *We study online calibration under delayed labels, which prior calibration work (offline) does
not address.*

### 2.5 Formulaic openers
**Watch:** "In recent years, X has attracted increasing attention"; "With the rapid development of...";
"Despite recent advances,...".
**Before:** *In recent years, tabular deep learning has attracted increasing attention.*
**After:** *Tabular deep learning has a structural limitation: most models discard feature-type metadata
and must relearn it from data.*

### 2.6 Connective overuse
Do not start consecutive sentences with Moreover/Furthermore/Additionally/In particular; let logic carry.
**Before:** *Moreover, the method is fast. Furthermore, it is simple. Additionally, it scales.*
**After:** *The method is fast and simple, and it scales to one million rows (Section 5).*

### 2.7 Contribution-list cliches
Each contribution names a *specific* result, not a restatement of the abstract.
**Before:** *Our contributions are: (1) a novel method; (2) extensive experiments; (3) strong results.*
**After:** *We (1) introduce a metadata-aware encoder that reaches 0.91 AUROC vs 0.86 for the strongest
baseline; (2) show it stays within 2 points under 20% label noise where the baseline drops 9; (3) release
the benchmark.*

### 2.8 Citation dumping
Cite the one or two works that matter and say why, not a bracketed list.
**Before:** *Many methods exist [3, 7, 9, 12, 15].*
**After:** *The closest prior method is TabNet [7], which encodes all features jointly; we instead
condition on feature-type metadata.*

### 2.9 Hedging-by-vagueness
**Watch:** somewhat, relatively, fairly, to some extent, quite. Quantify or cut.
**Before:** *Performance is somewhat better and relatively robust.*
**After:** *Accuracy is 3 points higher and varies by less than 1 point across five seeds.*

### 2.10 Boilerplate emphasis
**Watch:** "It is worth noting that", "It should be emphasized that", "Notably,", "Importantly,".
If it matters, the sentence shows it.
**Before:** *It is worth noting that, importantly, the gain holds across scenarios.*
**After:** *The gain holds across all three scenarios (Table 4).*

### 2.11 Overlong, clause-stacked sentences
AI favors long sentences that chain three or four clauses with commas and "which", "that", "while", "with".
Split them: one idea per sentence, and cut subordinate clauses that carry no weight. **Watch:** sentences
past ~30 words, or with 3+ subordinate clauses.
**Before:** *Existing methods, though promising, are largely empirical, with unclear principles
underpinning their behavior, which limits their reliability and further progress.*
**After:** *Existing methods stay empirical. Their principles are unclear, which limits reliability and
progress.*

---

## Layer 3: Preserve these (do NOT over-correct)
A general humanizer flattens legitimate scholarly constructs. Keep them.

- **Evidence-tied hedging is correct and required.** Keep "suggests", "is consistent with", "we
  hypothesize that", "may indicate", "appears to" when the claim is genuinely uncertain.
  *Wrong fix:* turning *"the results suggest X"* into *"the results prove X"*: this manufactures
  over-claiming. Keep the calibrated verb.
- **Passive voice** is fine when the actor is irrelevant: *"Samples were normalized to total protein."*
- **First-person plural "we"** is standard; do not rewrite to avoid it.
- **Semicolons and an occasional triple** are fine in moderation. Em-dashes are the exception: remove
  them entirely (Layer 1), recasting with commas, colons, parentheses, or separate sentences.
- **Formal definitions, named methods/metrics, technical terms, equations, and symbols** stay verbatim.
- **Never invent, drop, or alter a number, equation, or citation.** Same content; preserve every cite key.

---

## Layer 4: Claim-evidence discipline
For every empirical claim, check (a) is it backed by a number, figure, table, or citation in the text,
and (b) does the verb match the strength of that evidence?

- **Unbacked claim -> add the evidence pointer or soften.**
  *Before:* *Our method is more robust.*  *After:* *Our method's accuracy drops by 2 points under
  distribution shift, versus 11 points for the baseline (Figure 3).*
- **Verb stronger than evidence -> downgrade.**
  *Before:* *This demonstrates that our method is universally superior.*
  *After:* *On these three datasets, our method matches or exceeds the strongest baseline (Table 2).*
- **Vague magnitude -> a number or RANGE, attributed.**
  *Before:* *a large improvement.*  *After:* *a 2--6% improvement in balanced accuracy over the strongest
  baseline.*
  Prefer ranges (e.g., "2--6%") over single averaged values unless the averaging method is stated, and
  attribute each number to its method, metric, and baseline. When comparing, lead with the comparison
  against the strongest competitor, not the trivial baseline.

---

## Layer 5: Voice and venue matching
If the author supplies prior papers, read a sample first and note sentence rhythm, connective habits,
level and placement of hedging, how they open sections, notation, and recurring phrasings, then match
them. Match the venue's register too (e.g., ICLR/NeurIPS: terse, direct, results-forward; Nature/PNAS:
more expository; *Lancet/NEJM/JAMA*: structured, clinically anchored, strict reporting guidelines).
Absent a sample, default to clean, precise, venue-appropriate prose, not the casual, opinionated voice
of a general-purpose humanizer.

## Layer 6: Funding-proposal mode (NSF, NIH)
A proposal is not a paper. It is sold on **vision plus feasibility**, not on finished results, and
reviewers score it. The register shift matters: ambition language that the paper layers would trim
("long-term goal", "pioneer", "transformative", "establish a foundation") is *appropriate and expected*
here, provided a credible plan and evidence back it. So in proposal mode, **do not flatten the vision**;
enforce a different discipline instead: **claim <-> feasibility**.

### 6.1 Know the structure; the score lives in the first pages
Reviewers form a score from the opening, then skim the rest to confirm it. Put most editing effort there.
- **NSF.** A one-page **Project Summary** with the three review-criteria heads spelled out:
  **Overview**, **Intellectual Merit**, **Broader Impacts**, each self-contained. The Project
  Description then opens with **long-term vision -> this proposal's goal -> the gap -> the specific
  thrusts/aims -> the payoff**, ideally within the first 1--2 pages, with one overview figure. Broader
  Impacts must be substantive and integrated, never an afterthought.
- **NIH (R01).** The **Specific Aims page is the whole proposal in one page**, and is the most-read,
  most-decisive page. Standard arc: (1) opening: the problem, what is known, the **gap / critical need**;
  (2) the **long-term goal** and the **central hypothesis** with its rationale; (3) "**The objective of
  this application is...**" plus how the hypothesis was formed; (4) **2--3 Aims**, each a one-line goal +
  a phrase on approach + the expected outcome; (5) a **payoff** paragraph: what changes if it succeeds.
  Then **Significance, Innovation, Approach** as separately scored sections.

### 6.2 First-3-pages primacy (edit these hardest)
By the end of page 1 (NIH Aims) or pages ~2--3 (NSF), the reader must already hold: the **hook** (why it
matters, concretely), the **gap** (what is missing and the cost of the gap), the **central idea** (your
approach in one sentence), the **aims/thrusts** (crisp and parallel), and the **payoff**. If any is
missing or buried, fix that before touching later sections. A reviewer unconvinced by page 3 does not
recover on page 10.

### 6.3 Proposal-specific weak moves to fix
- **Vague importance.** *Watch:* "this is an important/timely problem", "X has many applications".
  **Before:** *Understanding this problem is critically important.*
  **After:** *Without bounds on how measurement noise propagates to diagnosis, clinical models are tuned by
  trial and error, the inefficiency this proposal removes.*
- **Method-as-aim** (an aim naming a technique instead of a question or outcome).
  **Before:** *Aim 2: Apply transfer learning to the dataset.*
  **After:** *Aim 2: Determine whether fusing wearable and lab signals improves early detection, and for
  which patient subgroups it helps or hurts.*
- **Dominoed aims** (Aim 2/3 collapse if Aim 1 fails; reviewers flag this as fragile). *Fix:* phrase
  aims as **parallel and independently valuable**; where one depends on another, state the fallback.
- **Ambition without feasibility.** Every bold claim needs a footing: preliminary data, a prior
  result/publication, a classical theorem you build on, or a collaborator/letter. *Fix:* attach the
  evidence beside the claim ("our preliminary result in Fig. X shows...", "building on a classical minimax
  lower bound...").
- **Boilerplate Broader Impacts / training plan.** *Watch:* "we will mentor students and disseminate via
  talks and papers." *Fix:* make it concrete, enumerated, and tied to the research: specific programs,
  named courses or tools, measurable outreach.
- **Hedged central hypothesis.** The Aims-page hypothesis is a falsifiable commitment, not "we will
  explore whether possibly...". Calibrated hedging belongs in the Approach's interpretation, not the
  central claim.

### 6.4 Preserve and deploy (funded-proposal craft)
These read as strength; keep or add them rather than editing them out.
- **Vision/ambition framing**: a bold long-term goal up front, with this proposal as one principled step
  toward it.
- **Run-in lead-ins for scannability**: bold/italic **Goal:**, **Motivation:**, **Innovation:**,
  *Thrust/Aim N (one-line mission):*. Reviewers skim; visible structure earns time.
- **A concrete running example or protagonist** to make an abstract method vivid and consistent across aims.
- **Sharp challenge/aim statements posed as questions**: a crisp open question reads as a well-posed
  problem (a boxed or set-off question per aim works well).
- **Anchoring novel work in deep, named classical results** to signal rigor and lineage: a known
  inequality, capacity notion, or test that the new method generalizes.
- **Foreground the team's standing as feasibility evidence**: prior funded work, preliminary results,
  publications, collaborators, and demonstration partners belong *early*, as proof the plan is executable.
  A real track record is evidence, not boasting; place it where it de-risks the aims. *(Use only the PI's
  own real, supplied record; never invent funding, results, partners, or letters.)*

### 6.5 Claim <-> feasibility (the proposal analog of Layer 4)
For every aim and promised outcome, check: is the ambition matched by a credible means, such as
preliminary data, a prior method, a classical foundation, a collaborator, or staged de-risking? If yes,
keep the ambitious verb. If no, attach the missing evidence or scale the claim to what the plan supports.
Never invent preliminary results, prior funding, partners, or letters; if the support does not exist, flag
the gap for the author rather than papering over it.

---

## Layer 7: Medical / clinical domain adaptation

Apply this layer to any manuscript involving human subjects, patient populations, clinical interventions,
diagnostic tests, epidemiological data, or preclinical animal studies. Medical writing has its own
reporting discipline and terminology precision that Layers 1--6 do not cover. The goal is not to
medicalize generic prose, but to enforce the rigor clinical reviewers and journals expect.

### 7.1 Clinical phrasing discipline

- **Patient-centered nouns.** Use *patients* for clinical populations, *participants* for healthy-volunteer
  or community studies, *subjects* only in formal study-design contexts (e.g., "study subjects"). Do not
  alternate among them for one cohort.
- **No curative overclaim.** *Watch:* cure, cured, curative, miracle, breakthrough, game-changer,
  "revolutionary treatment", "eliminates the disease". Clinical work *shows improved outcomes*, *reduces
  mortality*, *achieves response*—it does not cure unless the endpoint is explicitly disease-free survival
  with long-term follow-up.
  **Before:** *Our therapy cures lung cancer.*
  **After:** *Our therapy improved 12-month progression-free survival from 32% to 51% (HR 0.58, 95% CI
  0.41--0.82; Table 2).*
- **Interventions must be concrete.** Name the agent, dose, route, frequency, and duration. "Patients
  received treatment" is unacceptable; "patients received intravenous cisplatin 75 mg/m^2 every 3 weeks
  for up to 6 cycles" is the standard.
- **Outcomes: primary vs. secondary.** Distinguish the *primary endpoint* from *secondary endpoints*; do
  not let a secondary finding carry the abstract's main claim without labeling it.
- **Avoid "treatment" as a vague stand-in.** If the intervention is drug X, say drug X; if it is surgery,
  say surgery. "Treatment group" is acceptable only after the intervention has been defined.

### 7.2 Statistical reporting discipline

Match the reporting guideline to the study design and flag missing elements:

| Study design | Guideline | Non-negotiable elements |
|---|---|---|
| Randomized controlled trial | CONSORT 2010 | randomization method, allocation concealment, blinding/masking, sample size justification, flow diagram with attrition, intention-to-treat analysis, between-group effect sizes with 95% CI |
| Observational cohort / case-control | STROBE | eligibility criteria, setting and dates, exposure definition, outcome ascertainment, confounding control strategy, missing-data handling |
| Diagnostic / prognostic accuracy study | STARD | index test and reference standard definitions, blinding of test readers, spectrum of disease severity, 2x2 table data, sensitivity/specificity with 95% CI |
| Multivariable prediction model | TRIPOD | source population, candidate predictors, missing data, overfitting control (penalization / shrinkage), internal and external validation, calibration and discrimination metrics |
| Animal / preclinical in vivo | ARRIVE 2.0 | sample size justification, randomization and blinding, inclusion/exclusion, humane endpoints, housing and husbandry, adverse events |

- **Effect size over p-value alone.** Every between-group comparison should report the effect estimate
  (HR, OR, RR, mean difference) *with its 95% confidence interval*. A bare "p < 0.05" is insufficient.
  **Before:** *The difference was significant (p < 0.05).*
  **After:** *Median overall survival was 14.2 vs. 9.8 months (HR 0.67, 95% CI 0.49--0.91; p = 0.01).*
- **Statistical vs. clinical significance.** Do not call a result "clinically significant" unless the
  effect magnitude meets a pre-specified clinically meaningful threshold; "statistically significant"
  refers only to the p-value. Flag any conflation.
- **No "trend toward significance."** If p >= 0.05, report the actual p-value and the effect size; do not
  dress up a null result as a "positive trend."
- **Subgroup analyses.** Label them as *exploratory* unless pre-specified in the protocol; do not let a
  subgroup finding become the headline claim.

### 7.3 Medical terminology precision

These pairs are frequently conflated in AI drafts; enforce the correct distinction:

- **Incidence vs. prevalence.** Incidence = new cases over time; prevalence = existing cases at a point.
  Do not use "incidence rate" when describing a cross-sectional survey.
- **Mortality vs. fatality vs. death.** *Mortality* is the rate in a population; *case fatality rate* is
  deaths among confirmed cases; *death* is the event. Use the one that matches the denominator.
- **Risk vs. odds vs. hazard.** *Risk* = probability of event in a time window; *odds* = event / no-event;
  *hazard* = instantaneous event rate. Report the metric that matches the model (Cox -> HR; logistic ->
  OR; cumulative incidence -> risk ratio).
- **Sensitivity / specificity / accuracy / PPV / NPV.** Each has a fixed definition and denominator; do
  not call a high PPV "high accuracy" or report sensitivity without the disease prevalence context.
- **Disease names.** Use standard nomenclature (ICD-11 / MeSH / WHO terminology). Avoid colloquial
  shortenings ("lung cancer" is acceptable; "lung ca" in running text is not). Use tumor-node-metastasis
  (TNM) stage consistently.
- **Drug names.** Use the *generic (INN) name* on first mention; brand names belong in parentheses only
  if the specific formulation matters. Do not let a brand name become the default referent.

For specialty-specific terminology (oncology, respirology, nanomedicine), see **7.7**.

### 7.4 Mandatory methods-element checklist (audit, do not invent)

For any study involving human or animal data, audit the Methods section against this list. **Flag missing
items in the change report; never fabricate an ethics number, consent statement, or follow-up duration.**

- [ ] **Ethics approval / IRB / IEC** — institution name + approval number + approval date. For
  retrospective studies, note whether waiver of consent was granted.
- [ ] **Informed consent** — explicit statement (written / oral / waived with reason). For minors or
  incapacitated participants, note guardian/assent process.
- [ ] **Trial registration** — for prospective interventional studies: registry name (ClinicalTrials.gov,
  ChiCTR, etc.) + registration number + registration date relative to first enrollment.
- [ ] **Follow-up duration** — median and range, or minimum follow-up; not just "patients were followed
  up."
- [ ] **Sample size justification** — the assumed effect size, alpha, power, and any inflation for
  attrition. A bare "we enrolled N patients" without justification is a flag.
- [ ] **Randomization** — method (simple / block / stratified / cluster), allocation ratio, concealment
  mechanism. (Applies to RCTs only.)
- [ ] **Blinding / masking** — who was masked (patients, investigators, outcome assessors, statisticians)
  and how. If open-label, state explicitly why.
- [ ] **Inclusion / exclusion criteria** — enumerated, not "consecutive patients were enrolled."
- [ ] **Statistical analysis plan** — primary analysis (ITT / per-protocol), software + version,
  significance threshold, handling of missing data, multiplicity correction if multiple endpoints.
- [ ] **Data sharing statement** — required by many journals (ICMJE): state whether de-identified data
  are available and under what conditions.
- [ ] **Conflicts of interest / funding** — funding source and role of the funder; COI declaration.

If any item is missing, the change report must list it as **"Methods element missing — author must
supply"** rather than silently omitting or inventing it.

### 7.5 Medical manuscript structure

- **Structured abstract.** Clinical journals require *Background, Methods, Results, Conclusions* (or
  *Objective, Methods, Results, Conclusion*). Keep each section tight; Results must carry the primary
  endpoint number.
- **IMRaD discipline.** Introduction ends with the explicit study objective or research question; Methods
  is reproducible; Results follows the order of endpoints (primary first); Discussion interprets, does not
  repeat numbers, and includes limitations.
- **PICO anchoring.** In the Introduction's final paragraph, the Population, Intervention, Comparator,
  and Outcome should be identifiable. If any is vague, flag it.
- **Discussion limitations.** Every clinical manuscript needs a limitations paragraph that names at least
  the design's real weaknesses (retrospective, single-center, small sample, short follow-up, residual
  confounding). "Our study has some limitations" with no specifics is a flag.
- **GRADE / evidence framing.** When making practice recommendations, cite the evidence level (GRADE:
  high / moderate / low / very low) rather than asserting "doctors should use X."

### 7.6 Preserve (medical conventions to leave alone)

- Standard abbreviations on second mention: HR, OR, RR, CI, IQR, SD, SE, IQR, OS, PFS, DFS, ORR, DCR,
  AE, SAE, DLT, MTD, RP2D, ITT, PP, IRB, IEC, ICD, TNM, RECIST, WHO, ECOG, KPS. (Define on first use.)
- Disease stage / grade / histology terminology (e.g., "stage IIIA adenocarcinoma")—do not paraphrase.
- Anatomical and physiological terms in their standard form.
- Dosage expressions (mg/m^2, mg/kg, IU/mL) and units of laboratory values.
- The passive voice in Methods ("Blood samples were collected at baseline and at 4, 8, and 12 weeks") is
  standard and preferred; do not force active voice there.

### 7.7 Specialty-specific terminology

Apply the relevant subsection when the manuscript falls within that specialty. These are not exhaustive
glossaries; they flag the terms most often conflated or misused in AI-assisted drafts and the correct
usage expected by specialty reviewers.

#### 7.7.1 Oncology

**Response evaluation criteria** — name the criterion and version; do not say "tumor response was
measured" without specifying.
- Solid tumors: **RECIST 1.1** (default). Immuno-oncology trials: **iRECIST** (immune-related response
  criteria; distinguishes iUPD from iCPD). Brain metastases: **RANO** (and mRANO for meningioma,
  RANO-HGG for high-grade glioma). Lymphoma: **Lugano / Cheson 2014**. PET-based: **PERCIST 1.0**.
  Hepatocellular carcinoma: **mRECIST** (EASL criteria for viable tumor).
- **Before:** *Tumor response was assessed every 8 weeks.*
- **After:** *Tumor response was assessed by contrast-enhanced CT every 8 weeks according to RECIST 1.1;
  immune-related responses were also classified per iRECIST.*

**Endpoints — distinguish, do not collapse.**
- **OS** (overall survival): time from randomization to death from any cause.
- **PFS** (progression-free survival): time to progression or death.
- **DFS** (disease-free survival): post-curative-intent setting; time to recurrence or death.
- **EFS** (event-free survival): broader than DFS (includes second malignancy, treatment failure).
- **TTP** (time to progression): excludes death; use only when non-cancer deaths are common.
- **ORR** (objective response rate): CR + PR only. **DCR** (disease control rate): CR + PR + SD.
  **CBR** (clinical benefit rate): CR + PR + SD lasting ≥ a pre-specified duration (e.g., ≥24 weeks).
- **DoR / DOR** (duration of response): from first response to progression.
- *Flag:* calling DCR "response rate," or reporting "survival benefit" without specifying OS vs PFS.

**Response categories** — use the standard abbreviations after defining once: **CR** (complete
response), **PR** (partial response), **SD** (stable disease), **PD** (progressive disease), **NE**
(not evaluable). For iRECIST: **iCR / iPR / iSD / iUPD / iCPD**. Do not invent "partial remission" in
solid-tumor oncology (remission belongs to leukemia/lymphoma parlance).

**Toxicity and dose-finding.**
- Grade adverse events by **CTCAE** version (e.g., CTCAE v5.0). Distinguish **AE** (any untoward
  occurrence), **SAE** (serious: death, hospitalization, disability, congenital anomaly, life-threatening),
  **ADR** (adverse drug reaction: causal relationship assessed).
- **DLT** (dose-limiting toxicity): defined prospectively for the first cycle; **MTD** (maximum tolerated
  dose); **RP2D** (recommended phase II dose). Do not call MTD "the highest safe dose"—it is the dose
  below which DLT rate exceeds the pre-specified threshold.

**Staging and treatment setting.**
- **TNM** staging: specify **cTNM** (clinical), **pTNM** (pathologic), **ypTNM** (post-neoadjuvant),
  **rTNM** (recurrent). Cite the AJCC/UICC edition (e.g., AJCC 8th).
- Treatment setting: **neoadjuvant** (before surgery), **adjuvant** (after curative-intent surgery),
  **perioperative** (both), **definitive / concurrent chemoradiation**, **metastatic / advanced /
  recurrent**, **first-line / second-line / later-line**. Do not use "adjuvant" for metastatic
  maintenance therapy.

**Biomarkers — report the assay and threshold.**
- PD-L1: **TPS** (tumor proportion score) vs **CPS** (combined positive score = tumor + immune cells);
  specify the antibody clone and platform (22C3 pharmDx, SP263, etc.).
- **TMB** (tumor mutational burden): report mut/Mb and the assay panel size.
- **MSI-H / dMMR**: specify the method (PCR pentaplex vs IHC for MLH1/MSH2/MSH6/PMS2).
- HER2: **IHC 0/1+/2+/3+**; IHC 2+ requires **FISH/SISH** reflex with HER2/CEP17 ratio and average copy
  number.
- Driver mutations (EGFR, ALK, ROS1, BRAF V600E, KRAS G12C, MET exon 14, NTRK, RET): specify the
  specific variant, not just "EGFR mutation."

#### 7.7.2 Respirology / Pulmonology

**Pulmonary function testing (PFT).**
- **FEV1** (forced expiratory volume in 1 second), **FVC** (forced vital capacity), **FEV1/FVC ratio**
  (obstruction if < LLN or <0.70 per GOLD), **FEF25-75** (small-airway indicator, not diagnostic alone).
- **DLCO / TLCO** (diffusing capacity): corrected for hemoglobin and alveolar volume (**KCO**).
- **TLC** (total lung capacity), **RV** (residual volume), **FRC** (functional residual capacity).
  Restriction = reduced TLC; obstruction with air trapping = elevated RV/TLC.
- **BDT** (bronchodilator test): report absolute and percent change in FEV1; reversibility = ≥12% AND
  ≥200 mL. **BPT** (bronchial provocation test): methacholine PC20 or mannitol FEV1 fall.
- *Flag:* "mild obstruction" without specifying FEV1 % predicted and GOLD stage.

**Disease nomenclature and severity.**
- **COPD**: GOLD 2024 classification (spirometric grades 1-4 combined with symptom/exacerbation groups
  A/B/E). Do not use "COPD stage III" alone—specify spirometric grade and group.
- **Asthma**: GINA steps 1-5; distinguish **controlled / partly controlled / uncontrolled**. **Severe
  asthma** = uncontrolled despite high-dose ICS-LABA or requires high-dose therapy to maintain control.
- **ILD / DPLD**: specify the pattern — **IPF / UIP**, **NSIP**, **OP**, **HP**, **CTD-ILD**, **PPFE**.
  "Interstitial lung disease" alone is too broad for a study cohort.
- **Pulmonary nodules**: **GGO** (ground-glass opacity), **pGGN** (pure GGN), **mGGN** (mixed/part-solid
  GGN), **solid nodule**. Report size in mm (mean of long and short axis on axial CT) and growth rate
  (volume doubling time). Use **Lung-RADS** for screening-detected nodules.
- **Lung cancer histology**: adenocarcinoma (lepidic/acinar/papillary/micropapillary/solid), squamous
  cell carcinoma, **SCLC** (small cell), **LCNEC** (large cell neuroendocrine carcinoma), carcinoid
  (typical/atypical). Do not abbreviate "non-small cell lung cancer" as "lung cancer" in a cohort that
  includes SCLC.

**Imaging signs.**
- CT signs: **lobulation** (分叶), **spiculation** (毛刺), **pleural retraction/tailing** (胸膜牵拉),
  **vacuole sign** (空泡征), **air bronchogram** (支气管充气征), **calcification** (benign patterns:
  diffuse/popcorn/central/laminated; malignant: eccentric/stippled).
- **PET-CT**: report **SUVmax** and the uptake pattern; note that SUV is semiquantitative and affected
  by blood glucose, uptake time, and scanner calibration. Do not call "high SUV" diagnostic of malignancy
  without histologic correlation.

**Procedures and interventions.**
- **FOB** (flexible bronchoscopy), **EBUS-TBNA** (endobronchial ultrasound-guided transbronchial needle
  aspiration), **EUS-B** (esophageal ultrasound), **TBLB** (transbronchial lung biopsy), **cryobiopsy**,
  **navigational bronchoscopy**, **PTNB** (percutaneous transthoracic needle biopsy), **thoracentesis**,
  **pleural biopsy** (closed/CT-guided/thoracoscopic), **chest tube / indwelling pleural catheter**.
- For biopsies: report the diagnostic yield and complication rate (pneumothorax, bleeding) by approach.

**Infection and critical care.**
- Pneumonia setting: **CAP** (community-acquired), **HAP** (hospital-acquired, ≥48h after admission),
  **VAP** (ventilator-associated, ≥48h after intubation), **HCAP** (no longer a separate category in
  current ATS/IDSA guidelines—do not use).
- Severity scores: **CURB-65**, **PSI/PORT**, **SMART-COP**. Do not mix scores without justification.
- Tuberculosis: **sputum smear-positive / smear-negative**, **culture-positive / culture-negative**,
  **drug-sensitive / MDR / XDR / RR-TB**. Report the diagnostic method (smear, Xpert MTB/RIF, culture,
  LPA).
- **Oxygenation / gas exchange**: **PaO2/FiO2 ratio** (P/F ratio; ARDS: mild 200-300, moderate
  100-200, severe <100 per Berlin definition), **A-a gradient**, **SaO2 vs SpO2** (arterial vs pulse
  oximetry; do not equate). **PaCO2** with pH and **HCO3- / BE** for acid-base interpretation.

#### 7.7.3 Nanomedicine / Nanopharmaceutics

**Formulation type — be specific; "nanoparticle" is a last-resort umbrella term.**
- **Liposome** (unilamellar/multilamellar; PEGylated/stealth; stimuli-sensitive). **Micelle**
  (polymeric micelle; critical micelle concentration must be reported). **Dendrimer** (generation, e.g.,
  PAMAM G5). **Polymeric nanoparticle** (PLGA, PLA, PCL, chitosan, etc.—name the polymer). **SLN**
  (solid lipid nanoparticle) vs **NLC** (nanostructured lipid carrier). **Polymer-drug conjugate**.
- Inorganic: **gold nanoparticle** (sphere/rod/star/shell), **iron oxide nanoparticle** (SPION),
  **quantum dot** (core/shell composition), **carbon nanotube** (SWCNT/MWCNT), **MOF** (metal-organic
  framework; name the topology, e.g., ZIF-8, UiO-66, MIL-101).
- *Flag:* calling a liposome "a nanoparticle" without specifying the lipid composition, PEGylation, and
  lamellarity.

**Physicochemical characterization — report the method and conditions.**
- **Hydrodynamic diameter / Z-average** (DLS), **PDI** (polydispersity index; <0.3 = monodisperse,
  >0.7 = broad). Distinguish DLS intensity/volume/number distributions.
- **Zeta potential** (report medium pH and ionic strength).
- **EE** (encapsulation efficiency %) and **DL** (drug loading % or wt%). Do not conflate: EE =
  (encapsulated drug / total drug) × 100; DL = (encapsulated drug / total nanoparticle mass) × 100.
- Morphology: **TEM / SEM / AFM** (report staining and drying method; DLS size is always larger than
  TEM dry size—do not call the discrepancy an error).
- Crystallinity: **XRD**, **DSC**, **TGA**. Stability: storage conditions, time points, and what was
  measured (size, PDI, zeta, EE, drug retention).

**In vitro evaluation.**
- **Drug release**: specify the method (dialysis bag, ultrafiltration, centrifugal filter), medium
  (PBS pH 7.4, pH 5.0 endosomal, with/without serum), sink conditions, and sampling. Report with a
  kinetic model fit (zero-order, first-order, Higuchi, Korsmeyer-Peppas) only if justified.
- **Cellular uptake**: distinguish **qualitative** (confocal laser scanning microscopy) from
  **quantitative** (flow cytometry mean fluorescence intensity, or HPLC of cell-associated drug). Report
  incubation time, concentration, and cell line.
- **Cytotoxicity**: assay name (**MTT, CCK-8, SRB, LDH**), IC50 with 95% CI, cell line, seeding density,
  incubation time. Do not report "biocompatible" without a comparator and a tested concentration range.
- **Hemolysis**: report the method (ASTM E2524 or ISO 10993-4), positive/negative controls, and the
  concentration range; <5% hemolysis is the conventional threshold but must be stated.
- **Protein corona**: if studied, report incubation plasma source, time, temperature, and
  separation/wash protocol; distinguish hard corona from soft corona.

**In vivo evaluation.**
- **Pharmacokinetics**: report AUC0-t, AUC0-∞, t1/2, CL, Vd, MRT; compare to free drug. Specify the
  bioanalytical method and whether total or released drug was measured.
- **Biodistribution**: report %ID/g or %ID/organ at each time point; include major organs (liver, spleen,
  lung, kidney, heart, brain, tumor). Use **EPR effect** only when tumor accumulation exceeds blood and
  is shown relative to healthy tissue—do not assert EPR from a single time point.
- **Imaging**: modality (fluorescence, bioluminescence, MRI, PET, SPECT, photoacoustic), probe,
  excitation/emission or isotope, and quantification method. Ex vivo organ imaging must corroborate in
  vivo.
- **Tumor efficacy**: report tumor volume (calipers: V = length × width² / 2), body weight, survival,
  and toxicity. Include a free-drug comparator and an untreated control; do not claim "superior
  antitumor efficacy" from tumor volume alone without survival and toxicity data.

**Targeting strategies — classify explicitly.**
- **Passive targeting**: EPR-based; depends on tumor vascular permeability and retention.
- **Active targeting**: ligand-receptor (folate/FR, RGD/integrin, transferrin/TfR, aptamer, antibody,
  peptide, sugar/lectin). Report the ligand density per particle and the receptor expression level on
  target vs off-target cells.
- **Stimuli-responsive**: endogenous (**pH** endosomal/lysosomal, **redox** GSH, **enzyme**
  MMP/hyaluronidase, **ATP**) or exogenous (**temperature**, **light** NIR photothermal/photodynamic,
  **magnetic field**, **ultrasound**). Report the trigger threshold and release kinetics.
- *Flag:* "targeted nanoparticle" without specifying passive vs active, the ligand, and evidence of
  receptor-mediated uptake.

**Safety, regulation, and translation.**
- Toxicity: **acute** (single-dose LD50 or MTD) vs **subacute / subchronic / chronic** (repeat-dose,
  duration specified). Report hematology, clinical chemistry, organ histopathology, and organ coefficient.
- **Immunogenicity**: complement activation (**CARPA**), cytokine release, anti-PEG antibodies (if
  PEGylated), hypersensitivity.
- **RES / MPS uptake**: liver (Kupffer cells) and spleen are expected; report as %ID/g and explain if
  unusually high or low.
- **Clearance**: renal (particles <~5.5 nm hydrodynamic diameter) vs hepatobiliary (larger particles);
  do not assert renal clearance for 100 nm particles.
- **CMC / quality**: batch-to-batch consistency (size, PDI, zeta, EE across ≥3 batches), sterility,
  endotoxin (<0.5 EU/mL per USP), filter sterilization method, and scale-up (lab vs pilot batch).
- *Flag:* claiming "clinical translation potential" without addressing scalability, sterilization,
  stability, and batch consistency.

---

## Output
Return the cleaned text plus a short change report: patterns removed (by type), claims softened or given
evidence pointers, voice/venue notes, and—for medical papers—any missing methods elements from the 7.4
checklist (flagged as author-supplied, never invented). Confirm that no number, equation, or citation was
altered.

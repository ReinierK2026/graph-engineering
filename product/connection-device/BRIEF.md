# The Connection Device — design brief

**Pressure-testing three products hiding inside one idea: an always-listening device that
helps parents who have lost direct connection with their children.**

Compiled September 2026. Downstream of
[`research/parental-employment-and-childcare/`](../../research/parental-employment-and-childcare/README.md).

---

## Contents

1. [The two findings that reorder the options](#1--the-two-findings-that-reorder-the-options)
2. [Pressure test, with kill criteria](#2--pressure-test-with-kill-criteria)
3. [Recommendation](#3--recommendation)
4. [Concept specs](#4--concept-specs)
5. [Hard constraints and the architecture they force](#5--hard-constraints-and-the-architecture-they-force)
6. [Evidence base](#6--evidence-base)
7. [Prototype plan](#7--prototype-plan)
8. [Open questions](#8--open-questions)

---

## 1 · The two findings that reorder the options

### 1.1 Surveillance does not produce parental knowledge. Disclosure does.

This is the most decisive result in the brief, and it is not a soft ethical point — it is a
finding about whether the Monitor *works at its own stated job*.

Parental "monitoring" was assumed for decades to mean tracking and surveillance. Stattin and
Kerr tested it and found the field had been measuring parents' **knowledge** while assuming
its **source**:

| Study | Design | Finding |
|---|---|---|
| Stattin & Kerr 2000, *Child Development* (2,377 cites) | 703 14-year-olds + parents, Sweden | Parental knowledge came **mainly from child disclosure**. Disclosure — not surveillance — was the source most closely linked to lower delinquency. Conclusion: "tracking and surveillance is not the best prescription for parental behavior." |
| Kerr & Stattin 2000, *Developmental Psychology* (1,734 cites) | 1,186 14-year-olds + parents | Disclosure explained more of the knowledge→adjustment link than tracking did. Parents' control efforts related to good adjustment **only after** partialling out the child's *feelings of being controlled* — which were themselves linked to **poor** adjustment. |
| Kerr, Stattin & Burk 2010, *J. Research on Adolescence* (624 cites) | 938 students, longitudinal, 2 years | Youth disclosure predicted parental knowledge. **Neither control nor solicitation did.** Monitoring efforts did not predict change in delinquency; disclosure did. |
| Keijsers 2016, *IJBD* | Random-intercept cross-lagged, within-family | The monitoring→delinquency correlation **was not present at the within-family level**. The disclosure association was. Prior findings were between-person artefacts. |
| Rote et al. 2018, *Developmental Psychology* | 174 families, 1-year follow-up | **Snooping** was the variable that most differentiated family profiles. "Intrusive communicators reported more negative interactions concurrently and greater depression and **less maternal knowledge over time**." |

Read that last row again. Intrusive monitoring produced **less** parental knowledge a year
later, alongside more depression. The Monitor doesn't merely trade relationship quality for
information — over time it loses the information too, because it suppresses the disclosure
that was generating the knowledge in the first place.

> **Design consequence.** The objective function is not *maximise what the parent knows*. It
> is **maximise what the child volunteers**. Every feature should be evaluated against
> whether it increases or suppresses voluntary disclosure. That single reframe kills most of
> the Monitor and specifies most of the Conduit.

A supporting note on timing: a meta-analysis of 31 longitudinal studies (Lionetti et al.
2018) found disclosure declines (d = −.147) and secrecy rises (d = .194) normatively across
adolescence. You are fighting a developmental headwind that gets stronger every year, which
is an argument for entering **early** (ages 4–10) rather than at the age when parents panic
and start shopping for monitoring products.

### 1.2 The technology splits cleanly: health alerting works, emotional alerting doesn't

The "device hears something and alerts you" idea depends entirely on *what* it's listening
for, and the two branches are in completely different states of readiness.

**Emotional distress detection — not viable.**

- Speech emotion recognition reaches roughly **79% accuracy on curated open-source datasets**
  — i.e. clean, acted, adult data under laboratory conditions.
- Models trained on adult speech **degrade on children's speech**; children's voice quality
  varies enough between ages 6 and 18, across gender and age, that training sets need to be
  clustered into separate groups.
- Clinical voice corpora are **biased toward negative emotions** (fear, anger, sadness),
  which inflates apparent sensitivity and makes genuine distress hard to separate from
  ordinary bad moods.

At ~79% on clean adult data, a device firing on children's real-world audio would generate a
false-positive stream that (a) makes parents anxious, (b) trains them to ignore it, and
(c) the first time a child discovers a false alarm was raised about them, ends disclosure
permanently. This branch is not a "needs more training data" problem on a 12-month horizon.

**Respiratory/health detection — viable today.**

- A smartphone cough-analysis algorithm achieved **89% positive percent agreement and 84%
  negative percent agreement** against expert clinical diagnosis for **asthma exacerbations**,
  without clinical examination or lung-function testing.
- CNN approaches reach **~92% accuracy**, sensitivity up to 89%, specificity up to 90%,
  **AUC > 95%** distinguishing asthma from healthy.
- Cough/wheeze/breath classification runs **in real time on commodity Android hardware**, and
  pediatric-specific cough detection algorithms have been technically validated.
- Commercial precedent exists (Hyfe, Swaasa), so this can be partnered rather than built.

> **Design consequence.** "Alert me to what it hears" is a real product — but the signal is
> **physiological, not emotional**. Alerting on a wheeze is a medical service to the child.
> Alerting on a mood is a report on the child. Those are different businesses with different
> buyers, and only one of them is buildable now.

---

## 2 · Pressure test, with kill criteria

### A · The Monitor — hears the child, alerts the parent

**The case for.** It is the intuitive product, it is what worried parents ask for, and there
is a mature market (Bark scans messages, images and songs for 29+ harmful themes with
real-time alerts; Gabb removes browser/social/app-store entirely; AngelSense and Jiobit do
location). Buyers exist and are already spending.

**What kills it.**

1. **It fails at its own job.** §1.1. Intrusive monitoring reduces parental knowledge over a
   one-year horizon. You would be selling a knowledge product that destroys knowledge.
2. **The core detector doesn't work.** §1.2. Emotional distress detection is ~79% on clean
   adult data and degrades on children.
3. **Third-party consent is unsolvable.** Your child talks to other children. You cannot
   obtain consent from their parents. Ten to twelve US states require all-party consent
   (below, §5.1) and this is criminal law, not a terms-of-service matter.
4. **It has a discovery date.** Every covert-monitoring product is eventually found. The
   relationship cost is paid in full at that moment, and it is paid by the child.
5. **Peer stigma is a harm you impose on the child to solve the parent's problem.** Note that
   Jiobit's own positioning — designed to be sewn into clothing "for kids who won't tolerate
   visible wearables" — is the industry conceding this point.

**What survives.** A **narrow health-alerting device** for children with asthma, epilepsy,
or complex medical needs, and **developmental screening** (low conversational-turn counts
flagged for professional assessment, which is LENA's validated use). Both are defensible
because the signal is physiological, the alert is actionable, and the child is the
beneficiary. This is a **different product with a different buyer** — it is medical, not
relational. It should not be bolted onto a connection device.

**Verdict: kill the relational Monitor. Spin the health variant out as its own thing.**

### B · The Mirror — measures the parent, coaches the parent

**The case for.** The strongest evidence base of the three. The underlying measures are
validated: LENA's automated adult word count, child vocalisation count and conversational
turn count show fair-to-excellent agreement with manual counts. The target variable is
known — roughly **40 conversational turns per hour** is LENA's benchmark. There is no child
surveillance problem, because the consenting adult is the one being measured. It attacks the
mechanism the research actually identifies: conversational turns predicted language-related
brain function **over and above SES and sheer word count**.

**What complicates it — and this is the real problem.** The intervention evidence is mixed in
a specific and commercially awkward way. Across reviewed LENA-feedback studies, quantitative
feedback to parents **did not improve outcomes for the full sample** — but **each study
reported improvements for families below the 50th percentile**.

> The people who will buy a parenting-feedback device are, overwhelmingly, parents already
> above the median. **The people it demonstrably helps are below it.** That is not a product
> flaw; it is a distribution problem, and it determines the whole go-to-market: pediatric
> practices, early-intervention programmes, home-visiting services, WIC, school districts —
> not direct-to-consumer.

**Second risk: measurement becomes the relationship.** A parent optimising a turn-count
dashboard is performing contingency rather than practising it. Mitigation: report weekly, not
live; no streaks; no score; no comparison to other families; and make the metric disappear
once it stops moving.

**Verdict: strongest evidence, cleanest legal path, hardest commercial story. Viable if sold
B2B2C.**

### C · The Conduit — carries something between them

**The case for.** It is the only one of the three that directly implements the §1.1 finding:
it is a **disclosure-maximising** design rather than a knowledge-extraction one. The
underserved market is enormous and documented — 41.8m rural left-behind children in China
(2020 census), ~9m Filipino children with a migrant parent, plus divorced co-parents,
shift workers and deployed military in every high-income country. And the incumbent solution
is known to underperform: the transnational-parenting literature finds scheduled video calls
serve the parent more than the child, with children describing mediated contact as
*justifying and prolonging* the absence, and the "mediated family gaze" as something they
resent and negotiate around.

**What's weak.** No direct evidence, because nobody has built it — the theory is strong and
the empirics are absent. Hardest to demonstrate value for, hardest to price, and the buyer
(parent) is not the primary beneficiary (child), which makes the value proposition
awkward to articulate at point of sale.

**Verdict: biggest market, best theoretical fit, most product risk. This is the one worth
inventing.**

---

## 3 · Recommendation

**Build C, fund it with B, spin out the health variant of A.**

| | Product | Buyer | Legal load | Evidence | Verdict |
|---|---|---|---|---|---|
| **A** | Relational Monitor | Anxious parent | Extreme | **Against** | Kill |
| **A′** | Health alerting (cough/wheeze/seizure) | Parent of medically complex child; possibly payer | Moderate (medical device path) | **Strong** | Separate company |
| **B** | The Mirror | Pediatric practice, early-intervention programme | Light | **Strong but targeted** | Fund the work; B2B2C |
| **C** | The Conduit | Distance/disconnected parent | Moderate | Theory-strong, empirics-absent | **Build this** |

The unifying principle across everything that survives:

> **Give the parent less information than they want, and give the child more control than
> they expect.**

That sentence is the product. It is also the thing that will be hardest to hold onto under
commercial pressure, because every customer conversation will push toward more information
and more parental control — toward A. Write it into the design principles now, while it
costs nothing.

---

## 4 · Concept specs

### C1 · Tonight's Three Questions

**User** Parent of a 5–12-year-old who gets "fine" in response to "how was school?"
**Job** Give me a handle to grab so the conversation can start.

**What it does.** On-device topic extraction across the day. At a parent-set time, three
conversation openers: *"Ask about the beetle." "Thursday's test came up twice." "Someone
called Maya."*

**What it deliberately does not do.** No transcript. No quotes. No audio. No sentiment. No
timeline. No search. **The output is engineered to be too low-resolution to use as
surveillance** — you cannot reconstruct what was said, so you cannot police it, so the only
way to find out is to go and ask. The information gap *is* the product.

**Child's view.** The child sees the same three prompts before the parent does, and can veto
any of them with one tap. A vetoed topic is deleted, not flagged, and the parent is never
told a veto occurred — a visible veto is itself a disclosure, and would make the veto
unusable.

**Why the veto doesn't gut it.** Per §1.1, the objective is voluntary disclosure. A child who
controls the channel uses it; a child who doesn't, routes around it. Vetoes are a **health
metric, not a leak** — a rising veto rate is the product telling you trust is falling.

---

### C2 · The Asynchronous Mailbox

**User** A parent separated by migration, shift work, deployment, custody, or incarceration.
**Job** Let me be in my child's daily life without either of us having to perform.

**The insight.** The scheduled video call is close to the worst possible format for a child:
it is a performance, under observation, on the adult's schedule, frequently with a
grandparent prompting them to "say hello to Daddy." That is precisely the dynamic the
research finds children resenting.

**What it does.** A physical object — a handset, not a screen — that the child talks into
*whenever they want*. The parent receives it whenever they can, and sends one back.
Asynchrony is the feature: it fits time zones and night shifts, and it removes the
performance. There is **no live mode**, on purpose.

**The inversion that matters.** The child initiates. No parental "record now" command exists.
This is the whole design: it moves the channel from parental solicitation (which Kerr &
Stattin found predicts nothing) to child disclosure (which predicts everything).

**Third node.** The grandparent gets their own identity on the device, not a monitored role.
96% of Chinese children whose parents both migrate are raised by grandparents; 77.7% of urban
Chinese families have grandparents caring for under-3s; 2.1m US grandparents are primary
caregivers and are ageing (59.5% are 60+, up from 47% in 2012). Every product in this space
treats this person as either invisible or a subject. **Nobody has built for them.**

---

### C3 · The Relationship Mirror

**User** Initially, a clinician or home-visiting programme. Eventually, a below-median-input
family reached through them.
**Job** Show me what I'm actually doing, not what I think I'm doing.

**Measures — all of the parent.**

| Metric | Why |
|---|---|
| Conversational turns per hour | The validated active ingredient; ~40/hr benchmark |
| Turn distribution across the day | Reveals the 6pm collapse most parents can't see |
| **Wait-time** — pause after the child speaks before the adult fills it | Directly coachable, high-leverage, invisible to self-report |
| Technoference — phone in hand during conversation | Self-measured; the mechanism is lost contingency, not lost time |

**Reporting rules.** Weekly, never live. No score, no streak, no leaderboard, no
cross-family comparison. Show the parent's own trend only. When a metric stops moving, retire
it from the report — a dashboard you keep looking at has become the relationship.

---

## 5 · Hard constraints and the architecture they force

### 5.1 All-party consent — criminal law, not terms of service

The federal Wiretap Act (18 U.S.C. § 2511) sets a **one-party** consent baseline but **does
not preempt stricter state law**.

**All-party consent states:** California, Connecticut, Florida, Illinois, Maryland,
Massachusetts, Montana, New Hampshire, Pennsylvania, Washington — with Delaware and Nevada
added by some authorities. Nevada's statute reads as one-party but its Supreme Court has
interpreted it as all-party. Illinois's original statute was struck down in 2014 and
immediately replaced with a near-identical one.

For recordings spanning states, **the strictest standard applies**.

**The unsolvable version of this problem:** your child speaks to other children, teachers and
neighbours. You cannot obtain consent from their parents. No consent flow fixes this. The
only thing that fixes it is **not creating a recording**.

### 5.2 COPPA

- The 2013 Rule amendments added **an audio file containing a child's voice** to the
  definition of personal information.
- A 2017 FTC enforcement policy statement created a narrow carve-out, **codified in the 2025
  Rule amendments** (published in the Federal Register 22 April 2025, effective 23 June 2025,
  compliance date 22 April 2026 — already in force).
- The carve-out is genuinely narrow. The FTC will decline enforcement only where the operator:
  1. collects the voice file **solely as a replacement for written words** (a search, a
     verbal instruction or request);
  2. uses it for **nothing else** — no behavioural targeting, no identification — before
     deleting;
  3. retains it **only as long as needed** to execute the instruction, then deletes
     immediately;
  4. **discloses** the collection, use and deletion policy in the privacy policy.

  It does **not** apply where the operator requests personal information such as the child's
  name.
- Separately, the amended Rule bars retaining children's personal information **longer than
  necessary for the specific documented purpose**, after which it must be deleted.

**Note carefully:** the carve-out covers voice-as-text-input. It does **not** obviously cover
"listen ambiently all day and extract topics." Whether ambient feature-extraction without
retention constitutes "collection" at all is the pivotal legal question for C1, and it needs
a real opinion from counsel, not an inference from this brief.

### 5.3 The architecture all of this forces

```
microphone → on-device processing → derived features → audio destroyed (seconds)
                                          ↓
                            no raw audio ever stored
                            no raw audio ever transmitted
                            no transcript ever produced
                            no cloud inference on speech
```

This is simultaneously the legal answer, the trust answer, and the differentiation. Every
incumbent in the category is cloud-based. "The audio never leaves the device and is destroyed
within seconds" is a claim none of them can make, and it is verifiable by a third-party audit
you should commission and publish.

Corollary: **derived features are themselves personal information about a child.** "Topics my
9-year-old discussed today" is sensitive even with no audio attached. Minimise, expire on a
short clock, and keep it on-device wherever the product allows.

### 5.4 The consent ladder

A 4-year-old and a 14-year-old are not the same product.

| Age | Child's relationship to the device |
|---|---|
| 0–3 | Parent-controlled. Effectively a language-environment instrument; no autonomy issue. |
| 4–7 | Child knows it exists. Has an off button **that actually works**. |
| 8–12 | Child sees exactly what the parent sees. Co-review is the default interaction. |
| 13+ | Child controls it entirely, or you do not ship to them. |

Disclosure declines and secrecy rises normatively through adolescence (§1.1). A product that
fights that curve with surveillance loses, and the Rote finding says it loses *knowledge*,
not just goodwill.

**If the off button is fake, the product is a lie with a discovery date attached.**

### 5.5 Form factor — consider not putting it on the child

Wearing it imports school recording bans, loss and breakage, battery anxiety, and real peer
stigma. Two alternatives:

**The car.** The highest-density parent–child conversation space left in modern family life:
captive, recurring, and **side-by-side** — no eye contact, which lowers the stakes for
children raising hard subjects. It sidesteps school policy entirely, narrows third-party
consent to mostly family members, and the parent is *present*, so the device can prompt in
the moment rather than reporting after the fact.

**Bedtime.** 90% of parents have a routine and 67% include a story — but only **23% include
talking about the day**. A specific, measured, device-shaped gap.

---

## 6 · Evidence base

**On what builds connection**
- Conversational **turns** predicted language-related brain function over and above SES and
  sheer quantity of words heard (Romeo et al., *Psychological Science*, 2018). Reciprocity,
  not volume.
- The Hart & Risley 30-million-word gap is now regarded as inflated — a 329-family Denver
  replication put it nearer 4 million by age 4 — but the mechanism survived even as the
  magnitude didn't.
- LENA benchmark: ~40 conversational turns/hour. LENA's own research associates each
  additional 2 turns/hour with ~1 point of Full Scale IQ up to that ceiling; treat a
  vendor-generated effect size with appropriate caution.

**On what parents currently do**
- Parents spend *more* time with children than any prior generation (mothers 54→104 min/day,
  fathers 16→59, 1965–2012, 122,271 parents across 11 countries). **Time is not the deficit.**
- Technoference: 68% of parents feel phone-distracted with their children; the measured harm
  is **reduced contingency**, not reduced time. It attacks exactly the mechanism above.
- Only 23% of bedtime routines include talking about the day.

**On distance**
- Technology restores the *parent's* sense of parenting more reliably than the *child's*
  sense of being parented; children are markedly more ambivalent than their migrant mothers
  (Madianou & Miller, *New Media & Society*, 2011).
- Polymedia: families layer channels, and the *choice among* them carries meaning.
- Video calls are choreographed across three generations — parent, child **and grandparent
  carer** (Gan, *JCMC*, 2023).

**On monitoring** — §1.1 in full.

**On detection feasibility** — §1.2 in full.

**Full sourcing** for the demographic and time-use figures:
[`research/parental-employment-and-childcare/`](../../research/parental-employment-and-childcare/README.md)
and its 171-row [`indicators.csv`](../../research/parental-employment-and-childcare/indicators.csv).

---

## 7 · Prototype plan

### 7.0 The rule that governs every test

> **The primary endpoint must be child-reported. Never parent-reported.**

The Madianou & Miller finding guarantees that the parent's experience improves under almost
any intervention in this category — that is the documented failure mode, not a success
signal. **If you measure parent satisfaction you will get a false positive on all three
concepts.** Child-reported felt-closeness, child-initiated contact rate, and child-reported
sense of being listened to are the real endpoints. Build the instrument for those before you
build anything else.

### 7.1 Build no hardware for six months

| # | Test | Method | Cost | Falsifiable claim |
|---|---|---|---|---|
| 1 | **Three Questions** | Wizard-of-Oz. 20 families, 2 weeks. A human listens to a voluntary end-of-day child voice note and writes three openers. No device, no ML. | Days | Do dinner conversations get longer and does the *child* report feeling more listened to, vs. a control given generic prompts? |
| 2 | **Asynchronous vs. scheduled** | Diary study. Distance-parent families alternate two weeks of scheduled video calls with two weeks of async voice notes. | Days | Does **child-initiated** contact rise under asynchrony? Does child-reported closeness? |
| 3 | **The Mirror** | Phone-only. On-device turn counting, weekly report. Recruit deliberately **below median** via a partner clinic — the population the LENA evidence says responds. | Weeks | Does turn count rise in below-median families, replicating the LENA subgroup result? Does it *not* rise in above-median families, as predicted? |
| 4 | **Veto rate** | Instrument test 1. | Free | What fraction of topics do children veto, and does the rate rise or fall over two weeks? Rising = trust falling. This is your single best leading indicator. |
| 5 | **Health alerting** | Partner (Hyfe/Swaasa-class API), don't build. Asthmatic children, parent-held phone. | Weeks | Does exacerbation pre-warning change care-seeking? Note this is a **medical device regulatory path** — scope it before, not after. |

Test 1 is the highest-information, lowest-cost experiment in the set and requires nothing but
a spreadsheet, consent forms, and someone willing to listen to voice notes for two weeks.

### 7.2 What would make you stop

- Test 1: conversation length rises but **child-reported** closeness doesn't → you built a
  parent-satisfaction product. Stop.
- Test 4: veto rate climbing → children experience it as surveillance despite the design. Stop
  and redesign, don't ship with a veto button as an excuse.
- Test 3: no effect below median → the Mirror's one supporting result failed to replicate, and
  the commercial story was already hard. Stop.
- Any test where a child asks whether their parent can hear what they said → you have already
  lost the framing. The answer has to be obviously, checkably *no*.

---

## 8 · Open questions

1. **The legal pivot.** Does on-device ambient feature extraction with sub-second audio
   destruction constitute "collection" under COPPA? This determines whether C1 is a product or
   a lawsuit. Needs counsel.
2. **Who pays for C2?** The buyer (parent) is not the beneficiary (child), and the highest-need
   users — migrant workers sending remittances — are the least able to pay. Employer-paid?
   Telecom-bundled? Remittance-operator-bundled? That last one is worth serious thought: the
   money is already flowing along exactly the same corridor as the separation.
3. **Does the Mirror survive contact with an above-median parent?** The evidence predicts no
   effect. Is a no-effect product still commercially viable if it is *felt* to work — and do
   you want to sell that?
4. **The grandparent as customer.** Is the third node a user, a buyer, or both? Nobody has
   tested willingness to pay here because nobody has asked.
5. **What is the failure mode at scale?** Every one of these becomes a surveillance product if
   a single feature request is granted. Which specific feature request is the point of no
   return, and can it be made architecturally impossible rather than merely declined?

---

*This brief argues against the most commercially obvious version of the product. That
position is derived from the evidence in §1 and §5, not from caution — the Monitor is
rejected because it does not work, not because it is uncomfortable.*

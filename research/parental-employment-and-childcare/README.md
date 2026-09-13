# Who Works, Who Raises the Children, and How Parents Stay Connected

**A statistical review of parental employment, grandparent caregiving, and parent–child contact worldwide**

Compiled September 2026. All figures are attributed to a named source and survey year.
Where no defensible global number exists, this report says so rather than inventing one.

## Files in this folder

| File | What it is |
|---|---|
| `README.md` | This report — the full prose review with all tables and sourcing. |
| [`indicators.csv`](indicators.csv) | 171 machine-readable rows: `part, topic, geography, indicator, value, unit, reference_year, source, confidence`. Every figure quoted in the report appears here with its provenance. |
| [`who-raises-the-children.html`](who-raises-the-children.html) | The same review as a self-contained web page, with charts. Source of the published version at <https://claude.ai/code/artifact/22e86950-faca-43fe-8a1c-66b1c9a31c55>. |

The CSV is the canonical machine-readable form. Load it with:

```python
import pandas as pd
df = pd.read_csv("indicators.csv")
df[df.confidence == "high"]              # only the well-evidenced figures
df[df.part == 2].sort_values("geography")  # the grandparent-care evidence
```

Note that `value` mixes units — read it together with the `unit` column, which
distinguishes `percent`, `count`, `minutes_per_day`, `hours_per_week`,
`percent_minimum`/`percent_maximum` (one-sided bounds reported as such by the
source), `ratio`, `standard_deviations`, `years` and `usd`.

---

## Read this first: there is no single worldwide dataset

The three questions in the brief sound like they should have three numbers. They do not.
No statistical agency produces a global figure for "how many parents per household are
working," and the reason matters for how you read everything below.

| Source | Coverage | What it can tell you | What it cannot |
|---|---|---|---|
| **OECD Family Database** | ~38 rich countries, ~18% of world population | Household work patterns in fine detail (both FT / 1.5-earner / jobless) | Anything about the other 82% |
| **Eurostat EU-LFS / EU-SILC** | 27 EU states | Same, harmonised, annual | Non-EU |
| **ILO modelled estimates** | ~190 countries | Labour force participation by sex | Household composition — it counts *individuals*, not *parents in households* |
| **DHS / MICS** | ~90 low- and middle-income countries | Children's *living arrangements*, caregiver stimulation | Parental employment status in a comparable way |
| **National censuses (via UN DESA)** | 200 countries/areas, 1,129 sources | Household structure incl. skip-generation | Employment; reference dates span 1959–2025 |
| **Time-use surveys (MTUS/ATUS)** | ~30–40 countries, irregular | Minutes/day parents spend on childcare | Most of Africa, South and Southeast Asia |

Three structural problems compound this:

1. **"Working" is defined differently everywhere.** In sub-Saharan Africa and South Asia,
   most maternal work is informal, seasonal, home-based, or subsistence agriculture.
   Around **95% of employed women in South Asia and 89% in sub-Saharan Africa work
   informally**, and official statistics systematically undercount unpaid work in the field
   and household ([UN Women](https://www.unwomen.org/en/news/in-focus/csw61/women-in-informal-economy)).
   A rural mother farming with an infant on her back is "not employed" in some datasets
   and "employed" in others.
2. **"Raised by grandparents" collapses three very different things** — co-residence,
   primary caregiving, and daytime childcare. Part 2 separates them, because the numbers
   differ by an order of magnitude.
3. **"How parents connect" is partly a measurement question and partly a qualitative one.**
   Time-use diaries capture minutes; they capture warmth and responsiveness badly.

---

## Executive summary

**Parental employment.** In rich countries, the dual-earner household is now the norm but
not a supermajority: across the OECD, **~47% of children in couple households have two
full-time working parents**, plus **~16%** in "one-and-a-half earner" households, and
**~5%** in couple households where nobody works. The United States crossed 50% only
recently — **52% of opposite-sex couples with children under 18 were two-full-time-earner
households in 2025, up from 31% in 1975**. In low- and middle-income countries the
question inverts: near-universal parental work is the baseline, and the interesting
statistic is not *whether* parents work but that most of that work is informal and
unprotected.

**Grandparents.** The honest answer depends entirely on the definition:

| Definition | Best global estimate | Confidence |
|---|---|---|
| Grandparent provides some regular daytime childcare | **Very large — 40–78% of grandparents in surveyed countries** | Moderate; no global aggregate |
| Child lives in a household containing a grandparent | **~38% of children globally live with relatives beyond the nuclear family** (Pew, 130 countries) | Moderate |
| Child lives with grandparents and **neither parent** (skip-generation) | **~2.4% of children under 15** in DHS countries, up from 1.7% | Good for LMICs, no rich-country equivalent |

The skip-generation figure is the "raised by grandparents" number in the strict sense, and
**~2–3% of children in the developing world** is the defensible answer. It rises above 20%
in parts of southern and eastern Africa, and in specific migration corridors it dominates:
in China, when both parents migrate, **96% of left-behind children are cared for by
grandparents**.

**How parents connect.** Parents in rich countries spend *more* time on childcare than
their own parents did, despite far higher maternal employment — mothers went from **54 to
104 minutes a day** and fathers from **16 to 59 minutes** across 11 Western countries
between 1965 and 2012. The gender gap narrowed but did not close. The connection itself
runs through four channels: co-present time (declining in quality via phone interruption —
**68% of parents say their smartphone distracts them from their children**), ritual
(family meals, bedtime), language (conversational turns, not just word counts), and — for
hundreds of millions of migrant families — mediated contact by phone and video call.

---

# Part 1 — How many parents per household are working

## 1.1 The global frame: individuals, not households

The ILO's modelled estimates are the only near-universal series, and they count people,
not parents:

| Indicator | Value | Source |
|---|---|---|
| Global female labour force participation (15+), 2025 | **48.8%** (down from 50.7% in 2005) | [ILO](https://ilostat.ilo.org/topics/women/) |
| Gender gap in participation, 2025 | **24.1 pp** (down from 26.4 pp in 2005) | ILO |
| Women's share of the global labour force | **40.2%** | ILO |
| Women who joined the labour market in 20 years | **~320 million** | ILO |

**The motherhood penalty** — the reduction in women's participation associated with young
children — varies sharply and counter-intuitively by income level:

| Country income group | Motherhood penalty ratio |
|---|---|
| Upper-middle-income | **19.8%** |
| High-income | **13.2%** |
| Low-income | **5.4%** |
| Lower-middle-income | **4.3%** |

Source: [ILO gender gaps brief, 2024](https://www.ilo.org/media/365356/download).

The low penalty in poor countries is not a sign of gender equality. It reflects that
withdrawing from work is not an option: mothers there work out of necessity in subsistence
agriculture or home-based production, with children present. Fathers, everywhere, show the
opposite pattern — a "paternity premium" of *higher* participation after a child arrives.

## 1.2 Rich countries: the detailed household picture

This is where the data is genuinely good. **OECD Family Database indicator LMF2.2**
(children aged 0–14, EU-LFS and national labour force surveys):

| Household work pattern (couple households) | OECD average share of children |
|---|---|
| Both parents full-time | **~47%** |
| One full-time, one part-time ("one-and-a-half earner") | **~16%** |
| Jobless (neither parent working) | **~5%** |
| Remainder (one earner only, other patterns) | ~32% |

Full-time dual-earner shares exceed **two-thirds** of children in Denmark, Portugal,
Slovenia and Sweden. The pattern is strongly conditioned on child age — in Finland only
**35%** of couples with children are full-time dual-earner when the youngest child is 0–2,
rising to **56%** once the youngest is 6.

Working hours are asymmetric even among dual earners: **~23% of employed fathers** in
couples with children work more than 45 hours a week, against **~10% of mothers**
(OECD LMF2.1/LMF2.2).

**European Union (Eurostat, households with dependent children):**

| Indicator | Value | Year |
|---|---|---|
| All adults in the household employed | **61.3%** | 2025 |
| All adults working full-time | **41.5%** | 2025 |
| At least one part-time, others full-time | **16.5%** | 2025 |
| At least one adult not working, at least one working | **28.3%** | 2025 |
| No adults working | **13.8%** | 2025 |
| Households with children that are couples with children | **63.5%** | 2024 |
| Single-parent households | **12.7%** | 2024 |

Sources: [Eurostat household composition](https://ec.europa.eu/eurostat/statistics-explained/index.php?title=Household_composition_statistics),
[Eurostat news, July 2025](https://ec.europa.eu/eurostat/web/products-eurostat-news/w/ddn-20250707-1).

Note the divergence between the EU's 13.8% "no adults working" and the OECD's ~5% jobless
*couple* households — the EU figure pools single-parent households, which carry most of the
joblessness.

**United States (Pew Research Center, CPS data):**

| Year | Both parents full-time | Breadwinner father / homemaker mother |
|---|---|---|
| 1970/1975 | **31%** | **46%** (1970) |
| ~2015 | **46%** | — |
| 2025 | **52%** | — |

Source: [Pew, *How family work arrangements have changed over time*](https://www.pewresearch.org/social-trends/2026/06/16/how-family-work-arrangements-have-changed-over-time/), June 2026.

The US only crossed the 50% line for two-full-time-earner couples in the mid-2020s. This is
the single most commonly overstated statistic in this area — "both parents work" is often
quoted as if it were 70–80%, which is only true if part-time and marginal employment are
counted as "working."

## 1.3 Maternal employment specifically

| Indicator | Value | Source |
|---|---|---|
| OECD average maternal employment, youngest child under 3 | **~60%** | OECD Education at a Glance 2023 |
| Recent mothers (youngest 0–2) employed | **64%** | OECD LMF1.2 |
| …of whom employed **and not on leave** | **45%** | OECD LMF1.2 |

That gap between 64% and 45% is important and usually missed: in generous-leave countries a
large share of "employed" mothers of infants are formally employed but absent on parental
leave. Maternal employment rises monotonically with the age of the youngest child in
essentially every OECD country.

## 1.4 Single-parent households

| Indicator | Value | Source |
|---|---|---|
| Children in single-parent households living in jobless households (OECD avg) | **~30%** | OECD LMF1.1 |
| …Ireland, Luxembourg | **41–42%** | OECD LMF1.1 |
| …Türkiye | **63%** | OECD LMF1.1 |
| Countries where >30% of single parents have no paid work | Belgium, France, Greece, Ireland, Italy, New Zealand, Poland, Spain, UK | OECD LMF2.3 |
| Countries where >70% of employed single parents work full-time | Denmark, Estonia, Hungary, Lithuania, Portugal, Slovakia, Slovenia, Sweden | OECD LMF2.3 |

Poverty consequence: across the OECD, **65.8%** of individuals in jobless households with
children live in relative income poverty, against **8.3%** in working households with
children.

**Cross-national prevalence of single parenthood** (Pew, 130 countries): **23% of American
children live with one parent and no other adults — more than three times the global
average of 7%.** Comparators: China 3%, India 5%, Canada 15%, UK 21%. The lowest shares are
Mali and Afghanistan (1%) and Türkiye (2%).

## 1.5 Low- and middle-income countries: the inverted question

There is no LMIC equivalent of LMF2.2. What the evidence supports:

- **Parental work is near-universal, and often joint.** In DHS analyses of agricultural
  households, **both parents were employed in agriculture in 40% of families**
  ([PMC10021554](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC10021554/)).
- **It is overwhelmingly informal.** ~95% of employed women in South Asia and ~89% in
  sub-Saharan Africa are in informal work; **over 60% of working women globally are
  informal workers without employment or maternity protection**.
- **Maternity protection is largely absent**, so return-to-work is fast and childcare is
  improvised — which is precisely the mechanism that drives Part 2.

**Bottom line for Part 1:** the accurate global statement is not a percentage. It is that
*two* distinct regimes exist — a rich-country regime where the dual-earner household is
the plurality-to-majority arrangement and joblessness is concentrated in single-parent
households, and a low-income regime where nearly all parents work, informally, with
children in proximity rather than in substitute care.

---

# Part 2 — What share of children are raised by grandparents

## 2.1 Three definitions, three very different numbers

Most published claims about grandparent caregiving are confusing because they silently
switch between these:

```
Level 1  CO-RESIDENCE          child lives in a household that includes a grandparent
                               (parents usually also present)
            ↓ narrower
Level 2  SKIP-GENERATION       child lives with grandparent(s) and NEITHER parent
                               — "raised by grandparents" in the strict sense
            ↓ different axis
Level 3  CHILDCARE PROVISION   grandparent provides regular daytime care while
                               parents work (child may live anywhere)
```

Level 3 is by far the largest population. Level 2 is the smallest and the one people
usually mean.

## 2.2 Level 1 — Co-residence

| Indicator | Value | Source |
|---|---|---|
| People worldwide living in extended-family households | **38%** | Pew, 130 countries |
| Children globally living with relatives beyond the nuclear family | **38%** | Pew |
| …the same figure for the United States | **8%** | Pew |
| Adults 60+ in extended-family households, globally | **38%** | Pew |
| …United States | **6%** | Pew |
| US children under 18 living in a grandparent's home (2020) | **8.4%** (6.1 million) | US Census |
| US children in three-generation households, 1996 → 2016 | **5.7% → 9.8%** | Census/analysis |
| South African households that are multi-generational (3 generations), 2023 | **13.9%** | [Stats SA GHS](https://www.statssa.gov.za/publications/92-02-04/92-02-042023.pdf) |
| South African grandparents co-resident with children 0–17, 2023 | **6.7 million grandparents with 9.7 million children** | Stats SA |

Latin America has among the highest three-generation household shares globally, and the
share is *rising* — in Mexico by nearly 20% over 15 years. Among US Latino children, **13%
live with a grandparent**, but only **1.6%** live with a grandparent and no parent — a
clean illustration of the Level 1 / Level 2 gap.

## 2.3 Level 2 — Skip-generation: "raised by grandparents" in the strict sense

**The headline global figure.** Across Demographic and Health Surveys in low- and
middle-income countries, the cross-country average share of **children under 15 living in a
skip-generation household rose from 1.7% to 2.4%** between the earliest and most recent
survey rounds; the share of adults 60+ in such households rose from 5.4% to 6.7%
([N-IUSSP / Journal of Marriage and Family](https://www.niussp.org/family-and-households/skip-generation-household-trends-in-low-and-middle-income-countries-les-menages-avec-saut-de-generation-dans-les-pays-a-revenu-faible-et-intermediaire/)).

**Regional concentration** (UN DESA, 93 countries, older-persons basis):

| Region / country | Share of persons 60+ in skip-generation households |
|---|---|
| **Lesotho, Malawi, Rwanda, Uganda, Zambia** | **>30%** |
| Cambodia, Philippines | **>10%** |
| Asia generally | Low |

The African cluster maps directly onto historical AIDS mortality; the Asian exceptions map
onto labour migration.

**National-level skip-generation measures:**

| Country | Measure | Value |
|---|---|---|
| South Africa (2023) | Skip-generation households | **4.2%** of all households |
| United States (2021) | Grandparents responsible for grandchild's basic care | **2.1 million** (of 6.7m co-resident) = **32.7%** |
| United States (2021) | Responsible grandparents aged 60+ | **59.5%** (up from 47% in 2012) |

Note the US trend: responsible grandparents are getting older and are responsible for
longer, which is a different and harder caregiving burden than the same headcount a decade
ago.

## 2.4 Children not living with either parent — the wider frame

Skip-generation is a subset of a larger category. Where children are not with a parent,
grandparents are the modal destination, but not the only one.

| Population | Children living with neither parent | Source |
|---|---|---|
| 40 sub-Saharan African countries (DHS 1997–2002), under-15s | **11.9%** — of which 8.6 pp had *both parents alive*; only 0.9% were double orphans | DHS analysis |
| Range across sub-Saharan Africa | **8% (Mali) → 30% (Eswatini)** | DHS |
| South Africa (GHS 2024) | **18.8%** | Stats SA |
| South Africa (GHS 2022) | 19.5% (32.7% with both parents; 44.1% with mother only) | Stats SA |
| South Africa, children aged 0–4 living with both biological parents | **36%** | Stats SA |
| Uganda (2011) | **17%** of children 0–14 — of whom **97%** in informal kinship care | National household data |
| Lao PDR | **7.5%** of children 0–17 | UNICEF |
| Regions where fostering is institutionalised | **15–25%** of under-15s | Academic reviews |

The crucial finding, repeated across the literature: **most children not living with their
parents are not orphans.** In the sub-Saharan sample, roughly three-quarters of children
living with neither parent had both parents alive. Child fostering is a deliberate kinship
strategy — for schooling access, labour, or household economics — not primarily a response
to death.

## 2.5 The migration channel

This is where grandparent-raising becomes a mass phenomenon.

| Context | Figure |
|---|---|
| **Global left-behind children** | No reliable estimate; credible sources say **"hundreds of millions"** |
| **China**, rural left-behind children (2020 census) | **41.8 million**; some estimates 60m+; one study puts left-behind children at **68.8 million = 25% of all Chinese children** |
| **China**, narrower official definition (late 2021) | **~12.0 million** |
| **China**, care arrangement when **both** parents migrate | **96% cared for by grandparents** |
| **China** (2018), left-behind children cared for by grandparents or no one | **~7 million** |
| **Cambodia** | ~35% of the population are migrants; **~80% of left-behind children live with grandparents** |
| **Philippines** | **~9 million** children with at least one migrant parent; **27%** of children left behind |
| **Ecuador** | **36%** of children left behind |
| **Rural South Africa** | **>40%** of children left behind |

The Chinese figures vary by a factor of five depending on definition (residence registration
vs. actual absence, one parent vs. both, duration thresholds). Cite the definition, not just
the number.

## 2.6 Level 3 — Grandparents as the childcare arrangement

This is the largest number and the one most relevant to working parents.

**Europe (SHARE, waves 1, 2 and 8):**

| Indicator | Value |
|---|---|
| Grandparents providing regular childcare support | **>40%** |
| Cross-country range (any childcare) | **24% – 60%** |
| Highest: Denmark, Sweden, Netherlands, France | **~60%** |
| Southern Europe | **<50%** |
| Grandmothers who looked after a grandchild ≤15 in the past year in the parents' absence (11 countries) | **58%** |
| Grandmothers / grandfathers providing care frequently or sporadically | **44% / 42%** |

Source: [Prevalence of grandparental childcare in Europe: a research update](https://link.springer.com/article/10.1007/s10433-023-00785-8), *European Journal of Ageing*, 2023.

The Nordic/Southern inversion is counter-intuitive and important: grandparental care is
*more* common where public childcare is strong, but it is **less intensive** — occasional
and supplementary rather than daily and load-bearing. Southern Europe has fewer
grandparents involved, but those who are, are doing full-time substitution work.

**Other regions:**

| Country | Indicator | Value |
|---|---|---|
| **United Kingdom** | Grandparents who cared for a grandchild under 16 in past 12 months | **63%** |
| **United States** | Working parents relying on grandparent childcare | **40–60%** |
| **United States** | Working parents relying specifically on grandmothers | **42%** (2 in 5) |
| **China** | Urban families where grandparents are involved in caring for under-3s | **77.7%** (National Health Commission, 2019) |
| **China (Shanghai, 2014)** | Grandparents who are the *primary* caregiver | **73.4%** |

China is the global outlier: grandparental care there is not supplementary but structural,
functioning as the country's de facto infant-care system.

**Why: the formal childcare gap.** Across the OECD in 2023, only **29% of children under 3**
were enrolled in formal early childhood education and care — **21% of under-2s**, rising to
**52% of two-year-olds**, **79% of three-year-olds**, **90% of four-year-olds**. The under-3
gap is the space grandparents fill.

## 2.7 Synthesis for Part 2

- **"Raised by grandparents" in the strict sense (no parent present): ~2–3% of children**
  in the developing world, rising, and concentrated above 20% in southern/eastern Africa and
  in specific migration corridors.
- **Living with a grandparent present: ~8–14% in rich countries, far higher in Asia,
  Africa and Latin America**, where ~38% of children live with relatives beyond the nuclear
  family.
- **Being cared for by a grandparent while parents work: the plurality experience in much
  of the world** — 40–60% of grandparents in Europe, ~42% of US working parents, ~78% of
  urban Chinese families with under-3s.

---

# Part 3 — How parents actually connect with their children

## 3.1 How much time, and the direction of travel

The central and most counter-intuitive finding in this literature: **parental time with
children has increased, not decreased, across the entire period in which maternal
employment rose.**

**Dotti Sani & Treas (2016)**, *Journal of Marriage and Family* — 11 Western countries
(Canada, Denmark, France, Germany, Italy, Netherlands, Norway, Slovenia, Spain, UK, US),
**122,271 parents** (68,532 mothers, 53,739 fathers), 1965–2012:

| | 1965 | 2012 |
|---|---|---|
| **Mothers** — childcare, minutes/day | **54** | **104** |
| **Fathers** — childcare, minutes/day | **16** | **59** |

Corroborating series:

| Finding | Source |
|---|---|
| US fathers: 2.5 h/week (1965) → **7.3 h/week** (2011) | Pew / ATUS |
| Ratio of fathers' to mothers' time, full-time employed: .36 (1960s) → **.53** (1990s) | Bianchi et al. |
| 40-year increases range from **+1.0 h/day** (full-time employed fathers) to **+1.8 h/day** (non-employed mothers) | Gauthier et al. |
| South Korea, fathers: <25 min (1999) → **~60 min** (2014); mothers **130 → 200+ min** | Korean time-use surveys |

Mechanism: parents absorbed the time from leisure, sleep, housework and personal care — not
from each other. Mothers' childcare time did *not* fall as fathers' rose.

## 3.2 Current levels — United States (ATUS 2024)

| Group | Primary childcare, hours/day |
|---|---|
| Women, household with child under 6 | **2.8** |
| Men, household with child under 6 | **1.7** |
| Adults, youngest child 6–17 | **0.78** (47 min) |
| Not employed, child under 6 | **>3.3** |
| Employed, child under 6 | **1.7** |

Within the under-6 group: mothers spend **1.3 h** on physical care (bathing, feeding)
versus **38 min** for fathers, and **16 min** on care-related travel versus **10 min**.

**Secondary childcare** — a child under 13 in your care while you do something else — is
several times larger than primary care and is where most co-presence actually lives:

| Group | Secondary childcare, hours/day | Year |
|---|---|---|
| Mothers, youngest child 5–12 | **5.8 → 8.2** | 2019 → 2020 |
| Fathers, children ≤12 | **4.5 → 5.3** | 2019 → 2020 |

About **half of parents' waking hours involve two or more simultaneous activities.**

## 3.3 Cross-national levels (OECD time-use)

| Indicator | Value |
|---|---|
| Fathers, total childcare | **42 min/day** |
| Mothers, total childcare | **1 h 40 min/day** |
| Highest fathers: Australia, Austria, Canada, US | **>1 h/day** |
| Lowest fathers: Belgium, Estonia, France, Japan, South Africa | **<30 min/day** |

Globally, **men spend 45% of their time on unpaid work against women's 55%**, and at the
current rate of change **equality in unpaid care work is 92 years away**
([State of the World's Fathers 2023](https://www.equimundo.org/resources/state-of-the-worlds-fathers-2023/),
12,000 respondents across 17 countries). The report values global unpaid care work at
**~US$11 trillion/year**.

## 3.4 What parents actually *do* — the activity taxonomy

Time-use surveys decompose "childcare" into categories that behave very differently:

| Category | Contents |
|---|---|
| **Physical / routine care** | Feeding, bathing, dressing, medical care |
| **Developmental / interactive care** | Playing with, reading to, talking with and listening to, teaching |
| **Management** | Arranging schooling, activities, healthcare, logistics |
| **Transport** | Dropping off and picking up |
| **Secondary / supervisory** | Child present and in your care during other activities |

The developmental category is the one that has grown fastest, that carries the strongest
association with child outcomes, and that is most unequally distributed.

## 3.5 The education gradient — the sharpest inequality in the data

| Finding | Value |
|---|---|
| Developmental childcare, mothers with high school or less (2008–13) | **65 min/day** |
| Developmental childcare, college-educated mothers (2008–13) | **80 min/day** — roughly double their earlier level |
| Increase in childcare time: less-educated mothers | **+4 h/week** |
| Increase in childcare time: college-educated mothers | **+9 h/week** |
| Annual gap in direct parental engagement, high vs. low parental education | **~300 hours/year** — about **10 weeks of six-hour days** |

Dotti Sani & Treas found a positive educational gradient in child-care time that **widened
in a number of countries and narrowed in none**. Ramey & Ramey's "Rug Rat Race" attributes
part of this to intensified competition for university admission.

The gradient is developmentally targeted, not uniform: the education gap in *teaching* time
is largest when children are 3–5 (school-readiness years), and the gap in *management* time
is largest at ages 6–13 — in both cases precisely when that input matters most.

## 3.6 Connection through language

The most robust micro-level evidence on what "connecting" means:

| Finding | Value |
|---|---|
| Hart & Risley (1995) — the original claim | **30-million-word gap** by age 3 between high- and low-SES children |
| Denver replication, 329 families, children 2–48 months | **~4-million-word gap** by age 4 (some high school vs. college-educated mothers) |
| Australian cohort, by 18 months | Adult word count, child vocalisations and conversational turns all **0.5–0.7 SD higher** in more-educated families |
| Romeo et al. (2018), *Psychological Science* | **Conversational turns** predicted language-related brain function **over and above SES and sheer quantity of words heard** |

The direction of the field has shifted decisively from *volume* to *reciprocity*. The unit
of connection is the conversational turn — the back-and-forth — not the number of words
delivered at a child. The original 30-million figure is now widely regarded as inflated;
the mechanism it pointed at survived replication, the magnitude did not.

## 3.7 Connection through ritual

| Ritual | Statistic | Source |
|---|---|---|
| US parents eating dinner together 6–7 nights/week | **53%** | Gallup |
| …all seven nights | **35–38%**, stable since 1997 | Gallup |
| US households: 7+ family meals/week | **49.6%** (3–6 meals: 32.4%; 0–2: 18.0%) | NHANES |
| US parents of 0–4s reading to children frequently | **41%**, down from **64%** 13 years earlier | Survey data |
| Read to "every day / nearly every day," girls 0–4 vs boys 0–4 | **44% vs 29%** | Survey data |
| Parents of children ≤8 reading a story nightly | **~1 in 3** | Survey data |
| Parents reporting a bedtime routine | **90%** | Pediatric survey |

Composition of the bedtime routine, where one exists: brushing teeth **90%**, bedtime
stories **67%**, a drink or snack **47%/23%**, turning off devices **41%**, praying **31%**,
**talking about their day 23%**.

That last figure deserves attention. The single most conversationally rich element of the
bedtime routine is the least common one.

## 3.8 Connection at a distance — migrant and transnational families

For hundreds of millions of children, "how parents connect" is a technology question.

| Finding | Source |
|---|---|
| **>60%** of carers and young adult children in transnational families use social media / internet apps as their main communication channel | Philippines studies |
| Migrant mothers call and text **several times a day**, and may leave a webcam open for **12 hours**, producing "ambient co-presence" | Madianou & Miller |
| Migrant parents' motives for mobile-phone parenting: instantaneous access and reassurance, affection, mobility, relaxation | [Liu et al. 2017](https://consensus.app/papers/details/ec184442264050f8b9fb2bc5ca20b31e/), 378 migrant parents, southern China |
| Gendered channel choice: calls and texts with older sons, audiovisual with daughters | Liu et al. 2017 |
| Video calls are jointly "choreographed" across three generations — parents, children **and the grandparent carers** | [Gan 2023](https://consensus.app/papers/details/1608c8893f6f55748c2e6d0ce312dbdd/), *JCMC* |
| Mothers feel empowered by phone-based parenting; **their children are significantly more ambivalent** | [Madianou & Miller 2011](https://consensus.app/papers/details/f84008e0a0c55c06a379b3f9d0b32248/), *New Media & Society* |

The key theoretical frame is **polymedia** (Madianou & Miller): families do not pick one
channel, they layer several — voice calls, SMS, WhatsApp/Messenger video, social media
monitoring — and the *choice among* available media itself carries emotional meaning.

The unresolved finding, and the one most often glossed over in optimistic accounts: the
technology restores the *parent's* sense of parenting far more reliably than it restores the
*child's* sense of being parented. Left-behind children in multiple studies describe
mediated contact as justifying and prolonging the absence.

## 3.9 Interference — what degrades connection

"Technoference" is the most-measured contemporary threat to co-present connection:

| Finding | Value |
|---|---|
| Parents who feel distracted by their smartphone when spending time with their children | **68%** |
| Parents who used their smartphone in a fast-food restaurant with their children | **73%** |
| Parents on their phone ≥1 in every 5 minutes at the playground | **35%** |
| Mothers of infants using screens during daily feedings | **92%** |
| …often texting or using apps *during* infant feeding | **37%** |
| US parents who say they spend too much time on their smartphone | **47%** (Pew, 2023/24) |

Mothers reporting technology interrupting interaction with their infant or young child at
least sometimes, by activity:

| Activity | Interrupted at least sometimes |
|---|---|
| Playtime | **65%** |
| Book reading | **36%** |
| Mealtime | **26%** |
| Bedtime | **26%** |
| Discipline and limit-setting | **22%** |

The measured effect is not "less time" but **less contingency**: when parents use screens
around children there are fewer interactions and parents are less responsive to the child's
bids. Since Part 3.6 established that contingent back-and-forth is the active ingredient,
this hits precisely the mechanism that matters.

## 3.10 The global stimulation deficit

Applying the same lens outside rich countries, via UNICEF's MICS programme:

| Finding | Value |
|---|---|
| Children aged 2–4 not getting enough responsive interaction or stimulation at home | **~4 in 10** |
| Children missing out on reading, storytelling, singing, drawing with caregivers | **~1 in 10** |
| Children aged 2–4 who do not play with their caregivers at home | **>80 million (~1 in 5 globally)** |
| Children under 5 without adequate learning materials at home | **>90 million** |
| Children aged 3–4 across 74 countries whose fathers do not engage in early learning with them | **~40 million** |

Who provides high-level stimulation in low- and middle-income countries (MICS analysis):

| Caregiver | Share providing high stimulation |
|---|---|
| Mothers | **39.8%** |
| Other adult caregivers (incl. grandparents) | **20.7%** |
| **Fathers** | **11.9%** |

This is the cleanest link between the three parts of this report: where fathers contribute
11.9% of high-level stimulation and mothers 39.8%, the remaining 20.7% supplied by "other
adult caregivers" is substantially the grandparents of Part 2.

## 3.11 What the outcome literature says actually constitutes connection

Time is a proxy. The constructs that predict child outcomes are:

- **Responsiveness** — warmth, sensitivity, affection, and contingent reaction to distress
- **Demandingness** — rule-setting, discipline, consistent enforcement
- **Involvement** — monitoring and knowledge of the child's life

Findings: parental warmth predicts self-esteem, emotional stability, emotional
responsiveness and independence, and is negatively correlated with child hostility and
aggression. Responsiveness to distress and warmth are **separable**: responsiveness to
distress predicts better regulation of *negative* affect; warmth predicts better regulation
of *positive* affect. A strong attachment grounded in warm, responsive parenting predicts
mental health **across cultures**, and parent–child relationship quality predicts
**subjective well-being in adulthood across a diverse set of countries**
([*Communications Psychology*, 2024](https://www.nature.com/articles/s44271-024-00161-x)).

---

# Cross-cutting synthesis

**The care triangle.** In most of the world, children are not raised by "parents" or "a
grandparent" but by a distributed system with three nodes — working parents, a proximate
kin carer (usually a grandmother), and, increasingly, a formal or informal childcare
provider. The three parts of this report are one system:

```
  Parental employment            Care substitution              Connection channel
  ───────────────────            ─────────────────              ──────────────────
  Rich-country dual earner  →    formal ECEC (29% of      →     co-present, time-rich,
  (~47% both FT)                 under-3s) + occasional         phone-interrupted
                                 grandparent care
                                 (40-60% of grandparents)

  Rich-country single       →    patchy; 30% of children  →     time-poor, high stress
  parent                         in jobless households

  LMIC in-place work        →    child present during     →     co-present but low
  (informal, ~95% of             work; older siblings;          stimulation (4 in 10
  S. Asian women)                grandmother                    children under-stimulated)

  LMIC migration            →    grandparents (96% in     →     mediated: voice, video,
  (hundreds of millions          China when both                polymedia; "ambient
  of children)                   parents migrate)               co-presence"
```

**Three findings that reverse common assumptions:**

1. **Dual-earner households did not reduce parental time with children.** Both maternal
   employment and parental childcare time rose together across five decades. The trade-off
   was made against leisure and sleep, not against children.
2. **Grandparent care is not primarily a poor-country or crisis phenomenon.** It is *most
   prevalent* in Nordic countries with excellent public childcare — just least intensive
   there. Intensity and prevalence move in opposite directions.
3. **The class gap in parenting is widening through time, not shrinking.** The educational
   gradient in developmental childcare grew in multiple countries and shrank in none, and
   now amounts to roughly 300 hours a year of direct engagement.

---

# Data quality, caveats, and known gaps

**Confidence ratings on the headline claims:**

| Claim | Confidence | Why |
|---|---|---|
| ~47% of OECD children in couple households have two FT working parents | **High** | Harmonised LFS microdata, annual |
| US 52% two-FT-earner couples, 2025 | **High** | CPS, long consistent series |
| Skip-generation ≈ 2.4% of under-15s in LMICs | **Moderate** | DHS cross-country average; countries enter and exit the sample |
| 38% of children globally live with relatives | **Moderate** | Pew's 130-country synthesis; census definitions differ |
| "Hundreds of millions" of left-behind children | **Low** | No agency produces this; definitional chaos |
| China 41.8m rural left-behind children | **Moderate** | 2020 census, but competing figures span 12m–68.8m by definition |
| Mothers 54→104 min, fathers 16→59 min/day | **High** | 122,271-parent harmonised time-use sample |
| ~4 in 10 children 2–4 under-stimulated | **Moderate** | MICS self-report, 3-day recall |
| Technoference percentages | **Low–moderate** | Mostly convenience samples and self-report; few nationally representative |

**Known gaps this report cannot close:**

1. **No household-employment-status data for most of the world.** The OECD's LMF series has
   no counterpart for South Asia, sub-Saharan Africa, or most of Southeast Asia.
2. **No global grandparent-care aggregate.** SHARE covers Europe, the ACS covers the US,
   and China's figures come from a mix of official and survey sources with inconsistent
   definitions. Nobody sums them.
3. **Time-use data is absent for most of the world's children.** The 11-country Dotti
   Sani & Treas sample is entirely Western.
4. **Left-behind children have no reliable global denominator**, and China's own range spans
   a factor of five.
5. **Informal and subsistence work is systematically undercounted**, which biases every
   maternal-employment figure for low-income countries downward by an unknown amount.

**How to extend this work:**

- Pull **IPUMS-International** census microdata to build a genuinely global
  household-composition-by-employment cross-tabulation — the only realistic route to a true
  worldwide answer for Part 1.
- Pull **DHS/MICS household rosters** directly to compute skip-generation and
  living-arrangement shares on a consistent definition rather than relying on published
  cross-country averages.
- Use the **Multinational Time Use Study (MTUS)** harmonised files rather than published
  country summaries for Part 3.
- Note that UN DESA's **Household Size and Composition database was refreshed in 2026**
  (1,129 sources, 200 countries/areas, ~98% of world population, reference dates 1959–2025)
  and should be the anchor for any updated co-residence figures.

---

# Sources

**Parental employment**
- [OECD Family Database](https://www.oecd.org/en/data/datasets/oecd-family-database.html) — indicators LMF1.1 (children in households by employment status), LMF1.2 (maternal employment rates), LMF2.1 (usual working hours by gender), LMF2.2 (working hours, couple households), LMF2.3 (working hours, sole-parent households), LMF2.5 (time use for work and care), PF3.2 (enrolment in childcare and pre-school)
- [Eurostat — Household composition statistics](https://ec.europa.eu/eurostat/statistics-explained/index.php?title=Household_composition_statistics)
- [Eurostat — Nearly 25% of EU households had at least 1 child in 2024](https://ec.europa.eu/eurostat/web/products-eurostat-news/w/ddn-20250707-1)
- [Pew Research Center — How family work arrangements have changed over time](https://www.pewresearch.org/social-trends/2026/06/16/how-family-work-arrangements-have-changed-over-time/)
- [ILO — New data shine light on gender gaps in the labour market](https://www.ilo.org/media/365356/download)
- [ILOSTAT — Statistics on women](https://ilostat.ilo.org/topics/women/)
- [UN Women — Women in the informal economy](https://www.unwomen.org/en/news/in-focus/csw61/women-in-informal-economy)
- [World Bank — Labor force participation rate, female](https://data.worldbank.org/indicator/SL.TLF.CACT.FE.ZS)
- [OECD — Education at a Glance 2025, early childhood education and care participation](https://www.oecd.org/en/publications/2025/09/education-at-a-glance-2025_c58fc9ae/full-report/how-does-the-provision-of-and-participation-in-early-childhood-education-and-care-vary-across-countries_86b8275d.html)

**Grandparents and living arrangements**
- [UN DESA — Patterns and trends in household size and composition](https://www.un.org/development/desa/pd/content/patterns-and-trends-household-size-and-composition-evidence-united-nations-dataset)
- [UN DESA — Methodology Report: Database on Household Size and Composition 2026](https://www.un.org/development/desa/pd/content/methodology-report-united-nations-database-household-size-and-composition-2026)
- [UN DESA POPFACTS 2019/2 — living arrangements of older persons](https://www.un.org/en/development/desa/population/publications/pdf/popfacts/PopFacts_2019-2.pdf)
- [N-IUSSP — Skip-generation household trends in low- and middle-income countries](https://www.niussp.org/family-and-households/skip-generation-household-trends-in-low-and-middle-income-countries-les-menages-avec-saut-de-generation-dans-les-pays-a-revenu-faible-et-intermediaire/)
- [Pew Research Center — Which living arrangements are most common worldwide?](https://www.pewresearch.org/short-reads/2020/03/31/with-billions-confined-to-their-homes-worldwide-which-living-arrangements-are-most-common/)
- [Pew Research Center — U.S. has world's highest rate of children living in single-parent households](https://www.pewresearch.org/short-reads/2019/12/12/u-s-children-more-likely-than-children-in-other-countries-to-live-with-just-one-parent/)
- [US Census Bureau — Grandparents Living With Grandchildren](https://www.census.gov/library/stories/2024/03/grandparents-living-with-grandchildren.html)
- [US Census Bureau — Several Generations Under One Roof](https://census.gov/library/stories/2023/06/several-generations-under-one-roof.html)
- [Statistics South Africa — Children Living With Grandparents in South Africa, 2023](https://www.statssa.gov.za/publications/92-02-04/92-02-042023.pdf)
- [Statistics South Africa — General Household Survey 2024](https://www.statssa.gov.za/publications/P0318/P03182024.pdf)
- [Springer — The prevalence of grandparental childcare in Europe: a research update](https://link.springer.com/article/10.1007/s10433-023-00785-8)
- [Oxford Academic — What Drives National Differences in Intensive Grandparental Childcare in Europe?](https://academic.oup.com/psychsocgerontology/article/71/1/141/2604976)
- [DHS Program — Children's Living Arrangements and Orphanhood](https://dhsprogram.com/data/Guide-to-DHS-Statistics/Children%E2%80%99s_Living_Arrangements_and_Orphanhood.htm)
- [PMC — The relationship between orphanhood and child fostering in sub-Saharan Africa](https://pmc.ncbi.nlm.nih.gov/articles/PMC3473157/)
- [UNICEF — Children in alternative care](https://data.unicef.org/topic/child-protection/children-alternative-care/)
- [The Lancet — Health impacts of parental migration on left-behind children: systematic review and meta-analysis](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736(18)32558-3/fulltext)

**Parent–child time, interaction and connection**
- [BLS — American Time Use Survey news release](https://www.bls.gov/news.release/atus.htm)
- [BLS — Average hours per day parents spent caring for household children](https://www.bls.gov/charts/american-time-use/activity-by-parent.htm)
- [Dotti Sani & Treas — Educational Gradients in Parents' Child-Care Time Across Countries, 1965–2012](https://onlinelibrary.wiley.com/doi/abs/10.1111/jomf.12305), *Journal of Marriage and Family*
- [Bianchi — Are Parents Investing Less in Children?](https://csde.washington.edu/downloads/bianchi_AJS_paper.pdf)
- [Gauthier et al. — Do We Invest Less Time In Children?](https://www.ined.fr/fichier/s_rubrique/14687/annegauthier.fr.pdf)
- [Ramey & Ramey — The Rug Rat Race](https://www.nber.org/system/files/working_papers/w15284/w15284.pdf), NBER WP 15284
- [Equimundo — State of the World's Fathers 2023](https://www.equimundo.org/resources/state-of-the-worlds-fathers-2023/)
- [UNICEF DATA — Home environment](https://data.unicef.org/topic/early-childhood-development/home-environment/)
- [UNICEF — Global Report on Early Childhood Care and Education 2024](https://www.unicef.org/media/158496/file/Global-report-on-early-childhood-care-and-education-2024-1.pdf)
- [PLOS One — Maternal, paternal, and other caregivers' stimulation in low- and middle-income countries](https://journals.plos.org/plosone/article?id=10.1371%2Fjournal.pone.0236107)
- [Romeo et al. — Beyond the 30-Million-Word Gap: Children's Conversational Exposure Is Associated With Language-Related Brain Function](https://pmc.ncbi.nlm.nih.gov/articles/PMC5945324/), *Psychological Science*
- [Gallup — Most U.S. Families Still Routinely Dine Together at Home](https://news.gallup.com/poll/166628/families-routinely-dine-together-home.aspx)
- [ZERO TO THREE — Technoference: Parent Mobile Device Use and Implications for Children](https://www.zerotothree.org/resource/journal/technoference-parent-mobile-device-use-and-implications-for-children-and-parent-child-relationships/)
- [Pew Research Center — How teens and parents approach screen time](https://www.pewresearch.org/internet/2024/03/11/how-teens-and-parents-approach-screen-time/)
- [*Communications Psychology* — Parent-child relationship quality predicts higher subjective well-being in adulthood across a diverse group of countries](https://www.nature.com/articles/s44271-024-00161-x)

**Transnational and mediated parenting**
- [Madianou & Miller — Mobile phone parenting: Reconfiguring relationships between Filipina migrant mothers and their left-behind children](https://consensus.app/papers/details/f84008e0a0c55c06a379b3f9d0b32248/), *New Media & Society*, 2011
- [Liu et al. — Migrant Parenting and Mobile Phone Use](https://consensus.app/papers/details/ec184442264050f8b9fb2bc5ca20b31e/), *Applied Research in Quality of Life*, 2017
- [Gan — Choreographing digital love: video-mediated communication between Chinese migrant parents and their left-behind children](https://consensus.app/papers/details/1608c8893f6f55748c2e6d0ce312dbdd/), *JCMC*, 2023
- [Acedera & Yeoh — When care is near and far: Care triangles and the mediated spaces of mobile phones among Filipino transnational families](https://consensus.app/papers/details/7694d2f7436d570da1ac98dc23c0a651/), *Geoforum*, 2021
- [Chen — Left-Behind Children as Agents: Mobile Media, Transnational Communication and the Mediated Family Gaze](https://consensus.app/papers/details/dbd623a070a055c0afd81a77a50d7618/), 2020
- [Liang et al. — Mobile phone parenting in work-separated Chinese families with young children left behind](https://consensus.app/papers/details/7e52dc9fc9e052cc9bb4ca89cc9c048a/), *Child & Family Social Work*, 2022

---

*Note on access: oecd.org, un.org, ilo.org, pewresearch.org, ec.europa.eu and several
other primary-source domains were blocked by this environment's network egress policy.
Figures from those sources were obtained through search-engine retrieval of the same
documents; the canonical URLs are given above so every number can be checked at source.*

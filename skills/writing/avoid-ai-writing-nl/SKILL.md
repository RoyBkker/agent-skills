---
name: avoid-ai-writing-nl
description: Use when auditing or rewriting DUTCH (Nederlandse) text for AI writing patterns — when asked to "haal de AI eruit", "maak dit menselijker", "klinkt dit als ChatGPT?", "AI-check deze tekst", "ontslop dit", or "remove AI-isms from Dutch text" — or when Dutch marketing copy, blogposts, e-mails, LinkedIn-posts or app-teksten sound machine-generated. For English text, use avoid-ai-writing instead.
version: 1.0.0
license: MIT
metadata:
  author: Roy Bakker
  based_on: "avoid-ai-writing v3.16.0 by Conor Bronsdon (MIT); multilingual method: jurigis/avoid-ai-writing-multilingual"
  language: nl
  sources: ./sources.md
  tags: writing editing dutch nederlands ai-writing humanizer
---

# Skill: AI-schrijfpatronen in Nederlandse teksten herkennen en verwijderen

Je bent redacteur voor Nederlandstalige teksten. Je taak: AI-typische schrijfpatronen ("AI-ismen") herkennen en wegwerken, zodat de tekst klinkt als geschreven door een mens die iets te zeggen heeft.

**Grondbeginsel:** dit is een kwaliteitsinstrument, geen oordeel. De patronen hieronder zijn *statistisch* vaker aanwezig in LLM-output, maar mensen onder deadline-druk, ambtenaren, en tweedetaalschrijvers produceren dezelfde vormen. Geen enkel patroon bewijst iets op zichzelf. Nederlandse universiteiten (VU, UvA, RUG, EUR) accepteren AI-detectors niet als bewijs, en terecht: detectie van Nederlandse AI-tekst is aantoonbaar moeilijker dan van Engelse (beste macro-accuratesse 0,75 vs. 0,85 in de CLIN33 shared task), en commerciële detectors halen tot 61% valse positieven op tekst van niet-moedertaalschrijvers (Liang e.a. 2023). Signalen, geen bewijs.

**Twee anti-tells** (fouten die mensen maken bij het beoordelen):
- *Onbeholpen Nederlands is géén AI-signaal.* AI-Nederlands is juist "keurig"; het klassieke rode vlaggetje "krom taalgebruik" is verdwenen (consensus nl.wikipedia-redacteuren).
- *Foutloos, gepolijst Nederlands is géén menselijk bewijs.* Gladde, grammaticaal perfecte tekst met weinig inhoud is juist verdacht.

**Houdbaarheid:** tells verouderen. Modelupdates verschuiven patronen — OpenAI onderdrukt sinds november 2025 bijvoorbeeld de em-dash. Weeg recente teksten dus anders dan oude, en leun nooit op één enkel signaal.

**Uitzondering:** geciteerde voorbeelden, code, en tekst die aan iemand anders wordt toegeschreven vallen buiten de controle. Alleen de eigen auteursproza wordt beoordeeld.

---

## Contextprofielen

Optioneel mee te geven bij aanroep. Zonder opgave: automatische herkenning.

| Profiel | Auto-herkenning | Werking |
|---|---|---|
| `social` | kort, hashtags, emoji, aankondigingstoon (X-posts, productupdates, community-berichten) | Energie, fragmenten en 1–2 emoji toegestaan; streng op vage lof, engagement-bait en hashtag-stuffing |
| `blog` | doorlopende tekst, tussenkoppen, SEO-signalen | Uitgebalanceerde strengheid; extra streng op lijstjes-inflatie, "Kortom"-sloten en betekenisinflatie |
| `email` | aanhef, afsluiting, ondertekening | Beleefdheidsformules toegestaan; streng op sycofantie, hedge-stapeling en overgestructureerde antwoorden. Let op aanspreekvorm: bepaal éérst je/u (zie stemprofielen) |
| `linkedin` | professioneel register, persoonlijke framing, hashtags | Fragmenten en één retorische vraag toegestaan; streng op emoji-regen, drieslag, valse tegenstellingen en euforische sloten |

---

## Stemprofielen (aanspreekvorm en toon)

Nederlands dwingt een keuze af die Engels niet kent: **je of u**. LLM-output wisselt hier stilzwijgend in, of kiest een register dat niet bij de afzender past. Bepaal vóór het herschrijven het stemprofiel (vraag ernaar als het niet blijkt uit de tekst of context):

| Profiel | Aanspreekvorm | Toon | Typisch gebruik |
|---|---|---|---|
| `zakelijk-u` | u | formeel maar niet stijf; "verheugd"/"derhalve"-register alsnog vermijden | officiële e-mail, offerte, klacht, overheid |
| `zakelijk-je` | je/jij | professioneel-direct, de norm in NL-marketing en tech | website-copy, blogs, B2B-mail |
| `informeel` | je/jij | spreektaal toegestaan, humor mag | social posts, community, persoonlijke mail |
| `technisch` | je of neutraal | precisie boven vlotheid; vaktermen zijn hier géén AI-tell | documentatie, changelogs, dev-blogs |

**Vaste regel:** één aanspreekvorm per tekst. Je/u-drift binnen dezelfde tekst is zelf een herschrijfsignaal (praktijkobservatie, geen corpusbevinding).

---

## Modi

### Rewrite-modus (standaard)
Flag AI-patronen en herschrijf de tekst. Een tweede doorgang controleert de herschrijving opnieuw (zie Uitvoerformat).

### Detect-modus (alleen flaggen)
Patronen markeren zonder herschrijven. Voor: teksten van anderen, gepubliceerd werk, of als de schrijver zelf wil beslissen. Trigger: "alleen checken", "alleen flaggen", "geen rewrite", "scan", "audit".

### Edit-modus (bestand ter plekke bewerken)
Als de schrijver naar een bestand wijst ("haal de AI uit `blog.md`"): bewerk het bestand direct met minimale, gerichte edits.
- Wijzig alleen geflagde passages; **alinea's zonder tells blijven onaangeroerd**.
- Citaten, codeblokken en andermans tekst: flaggen, niet herschrijven.
- Bij een groot bestand: eerst bevestigen welk deel bedoeld is.
- Na afloop het bestand herlezen en bevestigen dat de geflagde patronen weg zijn — en dat er geen nieuwe zijn ontstaan (tweede-doorgang-checklist).

---

## Ernstniveaus

- **P0 — Geloofwaardigheidskillers:** direct herkenbare AI-artefacten. Altijd verwijderen. (Chatbot-openers, samenvattingssloten, spookbronnen, hashtag-stuffing.)
- **P1 — Duidelijke AI-geur:** statistisch of per brede redactieconsensus oververtegenwoordigd in Nederlandse LLM-output. Vrijwel altijd aanpakken.
- **P2 — Stilistische afweging:** kan bewust zijn ingezet; in context beoordelen, niet reflexmatig schrappen.

---

## Vocabulaire (3-tier-systeem)

**Wat Tier 1 betekent:** deze woorden zijn in Nederlandstalige AI-output opvallend frequent — niet omdat ze fout Nederlands zijn, maar omdat modellen ze als "veilig" verkiezen waar mensen variëren. Bewijsbasis: de klasse van evaluatieve epitheta (type *cruciaal/krachtig/waardevol*) is voor het Nederlands statistisch bevestigd (Boer & Spoelstra 2026, p<.05); de individuele woordkeuzes steunen op brede, onderling onafhankelijke redactieconsensus (3–7 bronnen per woord; zie sources.md). Flag betekent: concretiseren of vervangen.

**Tier 1 — altijd flaggen (P1):**

| AI-woord | Concreet alternatief | Waarom flaggen |
|---|---|---|
| cruciaal | beslissend / nodig / (laat het feit het werk doen) | meest genoemde NL-AI-woord (7+ bronnen); evaluatief epitheton |
| essentieel | nodig / onmisbaar / (concretiseren waarom) | tweede meest genoemde; klinkt vertaald |
| naadloos | soepel / zonder gedoe / (beschrijf de overgang) | seamless-calque; "steevast top-5 AI-woord" |
| baanbrekend | nieuw / eerste die… / (concretiseren wat er nieuw is) | betekenisinflatie |
| transformatief | (beschrijf de verandering concreet) | betekenisinflatie |
| revolutioneren | ingrijpend veranderen / (concreet werkwoord) | claimt wat bewezen moet worden |
| innovatief | (beschrijf wát er nieuw is) | leeg zonder bewijs |
| faciliteren | mogelijk maken / regelen / helpen bij | beleidsjargon dat AI verkiest |
| gamechanger | (concretiseren wat er verandert) | recyclecliché |
| duiken in / "laten we erin duiken" | bekijken / uitzoeken / beginnen | dive/delve-calque, 5+ bronnen |
| landschap (metafoor) | markt / vakgebied / situatie | "het huidige landschap" = AI-frame |
| navigeren (metafoor) | omgaan met / je weg vinden in | navigate-calque |
| ontgrendelen / ontsluiten (potentieel) | vrijmaken / benutten / (concreet) | unlock-calque; "geen enkele normale mens zegt dit" |
| (breed) scala aan | veel / verschillende / (aantal noemen) | opsommingsaankondiging |
| naar een hoger niveau tillen | verbeteren / (concreet resultaat) | next-level-calque |
| verheugd | blij / (weglaten en gewoon zeggen wat er is) | "de grootste verrader" in informele context |
| robuust (buiten techniek) | stevig / betrouwbaar | in `technisch`-profiel toegestaan |
| hoogwaardig | goed / (kwaliteit concreet maken) | reclamejargon |
| krachtig (leeg-evaluatief) | (benoem wat het kán) | evaluatief epitheton (corpusbevestigde klasse) |
| toekomstbestendig | (concretiseren: houdbaar tot wanneer, waarom) | zegt niets |

**Tier 2 — flaggen bij opeenstapeling (P2, ≥2× in dezelfde tekst of ≥3 verschillende Tier-2-woorden):**

| Woord/frase | Alternatief | Opmerking |
|---|---|---|
| bovendien / daarnaast (als zinsopeners) | en / ook / gewoon doorschrijven | dé NL-overgangswoorden van AI; één keer is normaal Nederlands |
| echter (als zinsopener) | maar | "Echter, …" aan zinsbegin is schrijftaal-op-z'n-stijfst |
| kortom / ten slotte / uiteindelijk | (vaak schrapbaar) | zie ook patroon 41 (samenvattingssloten) |
| benutten / inzetten | gebruiken | leverage-vertaalgeur |
| optimaliseren | verbeteren / versnellen / goedkoper maken | concretiseren wát er beter wordt |
| stroomlijnen | vereenvoudigen / versnellen | streamline-calque |
| in kaart brengen | uitzoeken / opsommen / meten | beleidsjargon |
| ontzorgen | het werk uit handen nemen | marketingjargon (in dienstverlening soms bewust) |
| dynamisch | (weglaten of concretiseren) | "dynamisch team" = vacature-AI |
| efficiënt / effectief | sneller / goedkoper / (metriek noemen) | zonder cijfer betekenisloos |
| uniek | (bewijs het of laat weg) | reclamewoord |
| betekenisvol / waardevol / indrukwekkend | (benoem de waarde concreet) | evaluatieve epitheta |
| impact (maken) / waarde toevoegen | (wat verandert er precies voor wie?) | corporate-vaag |
| synergie / datagedreven / schaalbaar | (concretiseren) | buzzword-cluster |
| zou kunnen / mogelijk / kan bijdragen aan | (durf te zeggen wat er ís) | hedge-vocabulaire; één slag om de arm volstaat |
| moeiteloos / geavanceerd | makkelijk / (specificeren) | reclamejargon |
| verkennen | bekijken / uitproberen | explore-calque bij overuse |

**Tier 3 — frasen; flaggen bij dichtheid (≥2× dezelfde frase, of ≥3 verschillende Tier-3-frasen):**

| Frase | Probleem |
|---|---|
| "in de snel veranderende wereld van vandaag" | inhoudsloze opening, 5+ bronnen |
| "in een wereld waarin…" / "in een tijdperk…" | zelfde familie |
| "in het huidige (digitale) landschap" | AI-frame, zie Tier 1 landschap |
| "het is belangrijk om op te merken/te benadrukken/te onthouden dat" | 6+ bronnen; laat het feit voor zichzelf spreken |
| "het is belangrijker dan ooit om" | urgentie-inflatie |
| "Ben je klaar om…" | infomercial-opener |
| "Bij [merknaam] begrijpen we…" | corporate-AI-opener |
| "digitale transformatie" / "het verschil maken" / "best practices" | LinkedIn-clichécluster |
| "state-of-the-art" / "track record" (onvertaald) | anglicisme-vulling |
| "een wervelwind van emoties" / "een reis vol ups en downs" | opgeklopte clichémetaforen (nl-BE-bronnen) |
| "aan het eind van de dag" | at-the-end-of-the-day-calque |
| "sterker nog" (≥2×) | AI-lievelingsscharnier |

**Formeel-registercluster — contextafhankelijk (P1 in informele/sociale context, toegestaan in juridisch-formele tekst):** derhalve, desalniettemin, voorts, teneinde, bijgevolg, aldus, zodoende, niettemin, aangaande, betreffende, voornoemd. Deze woorden zijn correct Nederlands, maar hun opduiken in een LinkedIn-post of mailtje verraadt gegenereerd of opgepoetst schrijfwerk — mensen schakelen niet spontaan naar notarisregister.

---

## 47 patronen in het Nederlands

### Inhoudelijke patronen (wat er staat)

| # | Patroon | Ernst | Voorbeeld (fout) | Herstel |
|---|---|---|---|---|
| 1 | **Betekenis-/euforie-inflatie** | P1 | "een inspirerend verhaal met blijvende maatschappelijke impact" | concreet resultaat met getal of feit |
| 2 | **Vage autoriteitsclaims** | P1 | "onderzoek toont aan…", "volgens experts", "steeds meer organisaties" | bron + jaartal noemen, of claim schrappen |
| 3 | **Formulaïsche uitdagingen** | P1 | "De implementatie was niet zonder uitdagingen." | de échte tegenslag benoemen + wat eraan gedaan is |
| 4 | **Overdreven evenwichtigheid** | P1 | "er zijn voor- en nadelen", "het is verstandig professioneel advies in te winnen" | een standpunt innemen; nuance verdienen met argument |
| 5 | **Geen eigen ervaring of anekdote** | P1 | alles klopt, niets is meegemaakt | eigen waarneming, twijfel of fout toevoegen — AI-teksten bevatten meetbaar minder persoonlijke voornaamwoorden (Boer & Spoelstra 2026) |
| 6 | **Weinig getallen en eigennamen** | P2 | "veel klanten", "een groot bedrijf" | LLM-tekst bevat significant minder getallen en eigennamen dan menselijke (CLIN33, p<.01) — concretiseer |
| 7 | **Redundantie / tredmolen** | P1 | "24/7, ook buiten kantooruren" | zeg het één keer |
| 8 | **Holle deugdclaims** | P1 | "Privacy hebben we serieus genomen." | wát is er gedaan (toets, contract, maatregel) |
| 9 | **Performatieve kwetsbaarheid** | P1 | "Eerlijk gezegd vond ik het spannend om dit te delen." | de kwetsbaarheid tonen in feiten, niet aankondigen |
| 10 | **Dramatisering van trivialiteiten** | P2 | "Wat ik toen ontdekte, veranderde alles." | proportie herstellen |

### Taalkundige patronen (hoe het er staat)

| # | Patroon | Ernst | Voorbeeld (fout) | Herstel |
|---|---|---|---|---|
| 11 | **Tier-1-vocabulaire** | P1 | zie tabel | vervangen/concretiseren |
| 12 | **Tier-2-opeenstapeling** | P2 | zie tabel | terugsnoeien |
| 13 | **Tier-3-frasecluster** | P1 bij cluster | zie tabel | frames vervangen door inhoud |
| 14 | **Formeel register in casual context** | P1 | "Verheugd deel ik dat…" in een LinkedIn-post | registerbreuk herstellen: schrijf zoals de afzender praat |
| 15 | **Vertaald-Engels / calques** | P1 | "biedt" te pas en te onpas (offer), "AI-aangedreven" (AI-powered), "een testament aan" | Onze Taal: ChatGPT-Nederlands "klinkt soms als vertaald Engels"; idiomatisch herformuleren |
| 16 | **Onvertaalde Engelse chunks** | P2 | "meaningful work", "tone of voice" middenin NL-zin | vertalen tenzij ingeburgerde vakterm in het genre |
| 17 | **Oxford-komma** | P1 | "snel, betrouwbaar, en veilig" | komma voor "en/of" is on-Nederlands; weghalen |
| 18 | **Em-dash op z'n Engels** | P1* | "AI vervangt niet—het bevrijdt talent" | in NL: gedachtestreepjes gepaard mét spaties, of een punt/komma. *Signaal verzwakt sinds nov 2025 (OpenAI-fix); weeg mee met datering |
| 19 | **Overgangswoord-stapeling** | P1 | "Bovendien… Daarnaast… Echter… Tot slot…" | "een bijna wanhopige overvloed aan transitiewoorden" — schrappen; check of de logische relatie überhaupt klopt |
| 20 | **Valse tegenstelling / contrast-frames** | P1 | "Niet alleen X, maar ook Y", "Het is geen X, het is Y", "Niet X. Niet Y. Maar Z." | directe bewering; één contrast per tekst hooguit |
| 21 | **Drieslag-dwang** | P1 | "snel, eenvoudig en efficiënt" (en élke opsomming drie items) | tel wat er echt is: twee, vier, één |
| 22 | **Hedge-vocabulaire** | P2 | "zou mogelijk kunnen bijdragen aan" | één voorbehoud volstaat |
| 23 | **Booster-overdaad** | P2 | "ongetwijfeld", "zonder twijfel", "absoluut" | boosters overuse + hedges underuse is het AI-profiel (VU ALP-gids); zekerheid verdienen |
| 24 | **Weinig verledentijd** | P2 | alles in tegenwoordige tijd, ook het verhaal van vorig jaar | menselijke tekst bevat meer verleden tijd (CLIN33); vertel wat er gebeurd ís |
| 25 | **Staccato-fragmenten** | P2 | "Allemaal los. Klinkt diep. Is het niet." | nep-diepzinnige one-liners aaneenschrijven tot gewone zinnen |
| 26 | **Copula-vermijding** | P2 | "fungeert als", "dient als", "vormt een belangrijk onderdeel van" | is / heeft / doet (universeel patroon, niet NL-specifiek gedocumenteerd) |
| 27 | **Synonymketens** | P2 | "klanten… afnemers… opdrachtgevers… relaties" voor dezelfde groep | het heldere woord herhalen (universeel patroon) |

### Structuurpatronen

| # | Patroon | Ernst | Voorbeeld (fout) | Herstel |
|---|---|---|---|---|
| 28 | **Verplicht samenvattend slot / kopje "Conclusie"** | P0 | elk stuk eindigt met euforische conclusie | "Altijd een buitensporige conclusie. Echt altijd." (nl.wikipedia-consensus) — eindig op het laatste inhoudspunt |
| 29 | **Intro→kopjes→conclusie-sjabloon + FAQ-aanhangsel** | P1 | elk artikel exact: inleiding, 3–5 kopjes, conclusie, FAQ | structuur uit de inhoud laten volgen |
| 30 | **Bold/bullets-overdaad & inline-header-lijsten** | P1 | "**Snelheid:** het platform versnelt…" | doorlopende tekst; opsomming alleen als het écht een lijst is |
| 31 | **Title Case in koppen** | P1 | "Vijf Tips Voor Betere Klantenservice" | Nederlands kapitaliseert alleen het eerste woord |
| 32 | **Monotone zinslengte / lage burstiness** | P1 | alle zinnen 15–25 woorden, alle alinea's even lang | variatie in zinslengte binnen de alinea is de sterkste stilometrische discriminator (Desaire 2023); korte zinnen erin. Echt. |
| 33 | **Alinea-reshuffle-test** | P2 | alinea's zijn stuk voor stuk verwisselbaar | rode draad aanbrengen: elke alinea moet op de vorige bouwen |
| 34 | **Vraag?-Antwoord!-tic** | P1 | "Het resultaat? Een unieke klantbeleving!" | hooguit één keer, en alleen als het register het draagt |
| 35 | **Emoji-regen met vast palet** | P1 | 🚀💡✨🙌👉 bij elke alinea; post geopend én gesloten met emoji | max 1–2 emoji in `social`; emoji-omlijsting is vrijwel zeker AI |
| 36 | **Hashtag-stuffing + #Hashtags #Met #Hoofdletters** | P0 (social/linkedin) | 9 hashtags waarvan 3 irrelevant | 2–3 relevante tags, kleine letters |
| 37 | **Engagement-bait-slotvraag** | P2 (social) / P1 (elders) | "Wat vind jij? Deel het in de reacties! 👇" | alleen een vraag stellen die je echt beantwoord wilt zien |
| 38 | **Standaard-drietal in lijsten** | P2 | altijd precies 3 tips, 3 stappen, 3 redenen | lijstlengte laten bepalen door inhoud |

### Communicatiepatronen

| # | Patroon | Ernst | Voorbeeld (fout) | Herstel |
|---|---|---|---|---|
| 39 | **Chatbot-openers** | P0 | "Zeker!", "Natuurlijk!", "Goede vraag!", "Wat een mooie vraag!" | volledig verwijderen |
| 40 | **Artikel-aankondiging** | P0 | "In dit artikel bespreken we…", "In deze blog duiken we in…" | direct beginnen met de inhoud |
| 41 | **Samenvattingssloten** | P0 | "Kortom, …", "Concluderend…", "Samenvattend…", "In conclusie" (calque!), "Al met al…", "Hopelijk helpt dit je verder" | schrappen; het stuk was net af |
| 42 | **Sycofantie & bedank-loops** | P0 | "Bedankt voor deze interessante vraag!", "Daar heb je helemaal gelijk in!" | volledig verwijderen |
| 43 | **Kennisgrens-disclaimers** | P1 | "Voor zover mij bekend…", "Op het moment van schrijven…" (zonder reden) | bron zoeken of bewering schrappen |
| 44 | **Corporate-aankondigingscalques** | P1 | "We zijn enthousiast om aan te kondigen…", "Wij zijn trots te kunnen melden…", "Graag laat ik weten…" | zeg gewoon wat er is: "Vanaf maandag…" |

### Artefacten

| # | Patroon | Ernst | Voorbeeld (fout) | Herstel |
|---|---|---|---|---|
| 45 | **Spookbronnen** | P0 | plausibel ogende maar onbestaande referenties, dode DOI's | elke bron naslaan; in NL-wetenschap steeg het aandeel spookreferenties van 1/1400 (2023) naar 1/200 (2026) |
| 46 | **Technische resten** | P0 | `oaicite`, `turn0search`, `contentReference`, markdown-resten, `?utm_source=chatgpt.com` | verwijderen — dit is mechanisch bewijs van AI-herkomst |
| 47 | **Prompt-echo** | P0 | de opdrachtformulering lekt de tekst in ("een pakkende post van 200 woorden over…") | verwijderen |

---

## Vlaanderen-notitie (nl-BE)

Standaard-AI-Nederlands leest voor Vlaamse lezers als **Hollands-formeel**: het mist de spreektaal van Vlaamse ondernemers en klinkt afstandelijker dan bedoeld (De Copywriter.be; VAIA). Kalibratie bij Vlaamse doelgroepen:

- **u houdt langer stand** in Vlaanderen; te snel amicaal je/jij leest als "Hollandse" marketing.
- Vlaamse woordenschat (jobstudent, solden, goesting) ontbreekt in AI-output vrijwel volledig — het ontbreken ervan in een zogenaamd Vlaamse tekst is een signaal.
- Clichémetaforen ("een wervelwind van emoties") zijn in nl-BE-bronnen expliciet als AI-tell gedocumenteerd.
- Bij alle grote Vlaamse media worden koppen, intro's en bullets inmiddels AI-gedraft (VVJ-rapport 2025) — weeg dat mee bij het beoordelen van nieuwsachtige tekst.

---

## Tolerantiematrix

| Patroon | social | blog | email | linkedin |
|---|---|---|---|---|
| Chatbot-openers (P0) | nee | nee | nee | nee |
| Samenvattingssloten (P0) | nee | nee | nee | nee |
| Hashtag-stuffing (P0) | nee (max 2–3) | n.v.t. | n.v.t. | nee (max 2–3) |
| Tier-1-vocabulaire | streng | streng | middel | streng |
| Tier-2-vocabulaire | soepel | streng | middel | middel |
| Overgangswoord-stapeling | streng | streng | soepel | middel |
| Formeel register (derhalve-cluster) | nee | nee | alleen bij `zakelijk-u` | nee |
| Emoji | 1–2 oké | nee | nee | 1–2 oké |
| Drieslag | middel | streng | soepel | streng |
| Vraag?-Antwoord!-tic | 1× oké | streng | streng | 1× oké |
| Engagement-slotvraag | oké mits gemeend | streng | n.v.t. | 1× oké |
| Fragmenten/staccato | oké met mate | middel | middel | oké met mate |
| Monotone ritmiek | middel | streng | middel | middel |

---

## Herschrijf-vs-patch-drempel

Bij **5+ Tier-1-flags** ÉN **3+ verschillende patrooncategorieën** ÉN **monotone zinsritmiek**: adviseer een volledige herschrijving in plaats van plaatselijke patches, en benoem expliciet waarom patchen niet volstaat. Vraag bij een herschrijving altijd naar de feiten die de vaagheid moeten vervangen (getallen, namen, gebeurtenissen) — verzin ze niet.

---

## Uitvoerformat

### Rewrite-modus

```
### Gevonden problemen

[Patroonnaam — P0/P1/P2]
> "[geciteerde passage]"
Probleem: [één regel uitleg]

---

### Herschreven versie

[herschreven tekst, in het gekozen stemprofiel]

---

### Wat er is veranderd

- [concrete ingrepen: verwijderd / vervangen / geherstructureerd]

---

### Tweede doorgang

[controle van de herschrijving zelf]
Resultaat: "geen restproblemen" OF concrete rest-flags met citaat
```

**Tweede-doorgang-checklist** (de herschrijving introduceert vaak zélf nieuwe AI-geur):
- nieuwe Tier-1/2-woorden binnengeslopen?
- gerecyclede NL-clichés: "tijd om de balans op te maken", "de cijfers liegen er niet om", "en eerlijk? …", een nieuw slot-aforisme, een nieuwe retorische vraag?
- overlevende overgangswoorden of contrast-frames?
- je/u-drift ten opzichte van het stemprofiel?
- ritme: staan er nog drie gelijkvormige zinnen op rij?

### Detect-modus

```
### Gevonden problemen

**P0 — Geloofwaardigheidskillers**
- [patroon]: "[citaat]"

**P1 — Duidelijke AI-geur**
- [patroon]: "[citaat]"

**P2 — Stilistische afweging**
- [patroon]: "[citaat]"

---

### Weging

Duidelijke problemen: [lijst]
Verdedigbaar/mogelijk bewust: [lijst]
Advies: volledige herschrijving / gericht patchen / acceptabel in context
```

### Edit-modus
Als rewrite-modus, maar de wijzigingen gaan rechtstreeks het bestand in (minimale edits), en "Herschreven versie" wordt vervangen door een lijst van toegepaste edits. Sluit af met het resultaat van de tweede doorgang op het bewerkte bestand.

---

## Volledig voorbeeld

*Context: een Nederlandse LinkedIn-bedrijfspost — het genre waar AI-tekst in het Nederlands het dichtst en herkenbaarst voorkomt. De "voor"-tekst is authentieke, ongeredigeerde LLM-output (geen vertaald voorbeeld).*

**Voor (AI-gegenereerd):**

> AI heeft ons klantenservice-team een makeover gegeven 🚀
>
> Een jaar geleden startten we met het integreren van AI-tools in onze klantenservice. Eerlijk gezegd: ik was nieuwsgierig, maar ook voorzichtig. Nu kijk ik terug op een jaar vol positieve veranderingen die ik niet had verwacht.
>
> Het resultaat? Onze response time halveert. Routinevragen over facturering, account-instellingen en basisprobleemoplossing worden nu direct door AI afgehandeld. Onze support-team kan zich concentreren op wat ze echt goed doen: complexe problemen oplossen en echte klantenrelaties opbouwen.
>
> Maar de getallen vertellen slechts de helft van het verhaal. Het gaat ook om klanttevredenheid. Onze NPS-score is met 12 punten gestegen. Klanten waarderen snelle antwoorden 24/7, ook buiten kantooruren. En onze team? Die voelt zich meer gewaardeerd omdat ze eindelijk tijd hebben voor meaningful work.
>
> Natuurlijk was de implementatie niet zonder uitdagingen. Het kostte tijd om de AI goed te 'trainen' op onze specifieke processen en tone of voice. Privacy en data security hebben we serieus genomen. Maar het investeren hierin was het waard.
>
> Voor andere bedrijven die dit overwegen: start klein, meet nauwkeurig, en zorg dat je team meegaat in het proces. AI vervangt niet—het bevrijdt talent.
>
> Dit is pas het begin. Volgende stap: intelligente predictive support.
>
> #AI #CustomerService #CustomerExperience #SoftwareBedrijf #DigitaleTransformatie #Innovation #TeamWork #NLP #DutchTech

**Na (opgeschoond, stemprofiel `zakelijk-je`, concretiseringen illustratief):**

> Vorig jaar zijn we AI gaan inzetten in onze klantenservice. De reactietijd is sindsdien gehalveerd en de NPS steeg 12 punten.
>
> Het grootste verschil zit in de routinevragen. Facturen, accountinstellingen, simpele storingen: die handelt de bot nu direct af, ook 's avonds en in het weekend. Klanten wachten niet meer tot maandagochtend, en het supportteam houdt tijd over voor de gevallen waar je echt een mens voor nodig hebt.
>
> Wat tegenviel: de bot onze processen en schrijfstijl aanleren kostte maanden, veel langer dan gepland. En voor we live gingen hebben we eerst een privacytoets gedaan en de leverancierscontracten opnieuw laten beoordelen. Saai werk, wel nodig.
>
> Begin je hier zelf aan? Pak één vraagtype, meet vanaf dag één, en betrek je supportteam bij elke stap. Zij horen als eerste waar de bot de mist in gaat.
>
> Hierna gaan we voorspellen waarover klanten gaan bellen, vóórdat ze bellen. Over een halfjaar vertel ik of daar iets van terechtkwam.
>
> #klantenservice #AI

**Wat de skill vond:**

- P0 Hashtag-stuffing (#36): 9 hashtags, deels irrelevant (#NLP), gemengd EN/NL
- P0 Generieke toekomst-afsluiter (#41-familie): "Dit is pas het begin."
- P1 Emoji-hook + makeover-frame (#35, #1): "een makeover gegeven 🚀"
- P1 Performatieve kwetsbaarheid (#9): "Eerlijk gezegd: ik was nieuwsgierig, maar ook voorzichtig."
- P1 Betekenisinflatie zonder inhoud (#1): "een jaar vol positieve veranderingen die ik niet had verwacht"
- P1 Vraag?-Antwoord!-tic, 2× (#34): "Het resultaat?", "En onze team?"
- P1 Anglicismencluster (#16): response time, meaningful work, tone of voice, data security, predictive support
- P1 Vertaald-Engels-scharnier (#15): "de getallen vertellen slechts de helft van het verhaal" (cijfers!)
- P1 Redundantie (#7): "24/7, ook buiten kantooruren"
- P1 Formulaïsche uitdaging (#3): "was de implementatie niet zonder uitdagingen"
- P1 Holle deugdclaim (#8): "Privacy en data security hebben we serieus genomen."
- P1 Drieslag-advies (#21): "start klein, meet nauwkeurig, en zorg dat je team meegaat" (mét Oxford-komma, #17)
- P1 Em-dash-aforisme + valse tegenstelling (#18, #20): "AI vervangt niet—het bevrijdt talent."
- P2 "echt/echte"-inflatie (#10-familie): "wat ze echt goed doen", "echte klantenrelaties"
- P2 Congruentie-drift (vertaalgeur, #15): "Onze support-team… ze", "En onze team? Die…"
- P2 Slotcliché (#41-familie): "het investeren hierin was het waard"

Zestien markeringen in acht korte alinea's — het volledige sjabloon van de Nederlandse AI-LinkedIn-post: hook → "een jaar geleden" → cijfers → "maar cijfers zijn niet alles" → uitdagingen → advies-drieslag → toekomst-teaser → hashtagblok.

---

*v1.0.0 — bronverantwoording met citaten, bewijssterkte per patroon en bekende lacunes: zie [sources.md](./sources.md). Gebaseerd op avoid-ai-writing v3.16.0 van Conor Bronsdon (MIT) en de multilinguale methode van jurigis/avoid-ai-writing-multilingual; alle Nederlandse patronen onafhankelijk gebrond, niet vertaald.*

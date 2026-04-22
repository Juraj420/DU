Pracovný list — Claude Code & AI asistenti
Časť 1 — Setup a základy
1. CLI vs GUI
Čo znamená CLI?
Command Line Interface — rozhranie príkazového riadku, kde zadávame textové príkazy.
Cez čo komunikujeme s CLI nástrojom?
Cez terminál (príkazový riadok) — písaním textových príkazov.
Čo znamená GUI?
Graphical User Interface — grafické používateľské rozhranie s oknami, tlačidlami a myšou.
Ako sa CLI ľahko automatizuje?
CLI sa ľahko automatizuje — príkazy sa dajú zapisovať do skriptov a spúšťať automaticky bez zásahu človeka.
Cez čo funguje CLI vzdialene?
Cez SSH (Secure Shell) — vzdialené pripojenie k serveru cez sieť.
Na čo je CLI menej náročné?
Na systémové zdroje (pamäť, výkon) — CLI nespúšťa grafické rozhranie.
2. Sessions
Dva dôvody, prečo začať novú session:
•Kontext sa naplnil alebo je zmätený — AI stratila prehľad o projekte
•Začíname nový, nesúvisiaci úkol — nechceme, aby predchádzajúci kontext ovplyvňoval nové zadanie
Časť 2 — Base usage a IDE integrácia
3. Konfigurácia
Prečo lokálne nastavenia nie sú v Git repozitári?
Pretože lokálne nastavenia sú špecifické pre daného vývojára alebo stroj. Zdieľanie cez Git by spôsobilo konflikty medzi členmi tímu, ktorí majú rôzne cesty, prostredia a preferencie.
4. Context Window a Tokeny
Čo je compaction?
Compaction (zhusťovanie) je proces, pri ktorom AI automaticky zhrnie a skomprimuje starší kontext, keď sa context window plní — uvoľní miesto pre nové tokeny.
Aká je nevýhoda compaction?
Strata detailov — zhrnutý kontext neobsahuje všetky pôvodné informácie, môžu sa stratiť dôležité nuansy alebo konkrétne rozhodnutia.
5. IDE Integrácie
Prečo používať IDE integrácie?
IDE integrácie umožňujú, aby AI priamo pracovalo s kódom bez prepínania okien. Ľahšie sa odkazuje na súbory, funkcie a chyby — AI vidí rovnaký kontext ako vývojár.
Časť 3 — Advance Permissions Management
6. Permissions
Čo stále vyžaduje povolenie? (2 odpovede)
•Vykonanie príkazov, ktoré môžu meniť systém (inštalácia, mazanie)
•Operácie s vonkajšími službami alebo sieťové požiadavky (API volania, deploy)
7. Dangerous Mode
Čo môže AI urobiť s git históriou?
Prepísať git históriu — force push, rebase, amend commitov bez potvrdenia.
Čo môže AI urobiť so súbormi?
Mazať súbory bez potvrdenia — vrátane dôležitých konfiguračných alebo produkčných súborov.
Aké skripty môže AI spustiť?
Ľubovoľné skripty bez potvrdenia — vrátane potenciálne nebezpečných bash skriptov.
S akým prostredím sa dangerous mode kombinuje?
So sandboxom / izolovaným prostredím (kontajner, VM) — aby prípadné chyby neovplyvnili reálny systém.
8. Sandbox
Ako si predstaviť sandbox? (prirovnanie)
Sandbox je ako pieskovisko pre deti — dieťa (AI) môže robiť čo chce vo vnútri, ale piesok (zmeny) nevylezie von. Prípadné škody sú ohraničené na izolovaný priestor.
Časť 4 — Version Control a Undo
9. Vracanie zmien
Dva dôvody, prečo je Git dôležitý pri práci s AI:
•Možnosť vrátiť zmeny — ak AI urobí chybu, stačí git revert alebo git checkout
•Prehľad zmien — vieme presne čo AI zmenila, pomocou git diff
Čo je dobré urobiť pred väčšími zmenami?
Urobiť commit (alebo branch) — vytvoriť záchytný bod, ku ktorému sa dá vrátiť.
Časť 5 — Plan Mode
10. Plan Mode
Pri akých úlohách použiť Plan Mode?
Pri komplexných, viacstupňových úlohách — refaktoring, nová feature, architektúra systému.
Kedy si nie si istý výsledkom?
Plan Mode pomôže overiť smer pred tým, ako AI začne písať kód — predídeš zlému smeru implementácie.
Aké úlohy ovplyvňujú viacero miest?
Úlohy, ktoré ovplyvňujú viacero súborov alebo modulov — kde zmena v jednom mieste môže rozbehať iné časti.
Čomu predídeš zbytočným plánovaním?
Predídeš zbytočným iteráciám a opravám — plán odhalí problémy skôr, než vznikne chybný kód.
Kedy môžeš ovplyvniť riešenie?
Pred začiatkom implementácie — v Plan Mode môžeš korigovať prístup, kým ešte nič nie je napísané.
Čo AI lepšie pochopí?
AI lepšie pochopí kontext a zámer — plán umožní AI premyslieť si riešenie celostne.
Časť 6 — Context Engineering a projektové inštrukcie
11. SPEC.md
Prečo je lepšie odkazovať na SPEC.md z CLAUDE.md?
Aby CLAUDE.md zostal krátky a prehľadný. SPEC.md môže obsahovať detailné požiadavky projektu, ktoré sa menia — aktualizácia jedného súboru je jednoduchšia. Tiež sa SPEC.md dá zdieľať s inými nástrojmi.
12. Projektové inštrukcie
Súčasťou čoho sa stáva CLAUDE.md pri načítaní?
Súčasťou systémového promptu (system prompt) — inštrukcie sa automaticky vkladajú na začiatok každého rozhovoru.
Prečo má byť CLAUDE.md stručný?
Pretože každý token v CLAUDE.md spotrebuje miesto v context window — dlhý súbor zbytočne znižuje priestor pre skutočnú prácu.
13. Context Engineering
Aké informácie pridávať?
Iba relevantné informácie k aktuálnej úlohe — nie všetko, čo vieme o projekte.
Čo šetríme stručnosťou?
Šetríme tokeny (context window) — viac miesta pre skutočný kód a odpovede.
Prečo používať formátovanie?
Formátovanie (nadpisy, odrážky) uľahčuje AI orientáciu v texte — AI rýchlejšie nájde potrebnú informáciu.
Prečo sú XML tagy lepšie?
XML tagy jasne ohraničujú sekcie kontextu — AI presne vie, kde začína a kde končí každý typ informácie (napr. <instructions>, <code>).
Časť 7 — Nástroje a rozšírenia
15. Thinking Mode
Čo spotrebuje thinking mode viac?
Viac tokenov a času — AI generuje interné premýšľanie pred finálnou odpoveďou.
Aká je odpoveď s thinking mode?
Odpoveď je premyslenejšia a presnejšia — AI uvažuje krok po kroku, menej chýb pri komplexných problémoch.
Pri akých úlohách ho vypnúť?
Pri jednoduchých, rutinných úlohách — formátovanie kódu, jednoduché otázky, kde hlboké uvažovanie nepridáva hodnotu.
16. Práca s dokumentáciou
Čo šetrí Markdown dokumentácia?
Šetrí tokeny oproti HTML alebo PDF — Markdown je kompaktný, AI ho dobre parsuje.
Ako sa lepšie spracováva Markdown?
Dokumentácia sa lepšie spracováva a vyhľadáva v Markdowne — štruktúra nadpisov pomáha AI orientovať sa.
17. MCP
Čo umožňuje MCP server pre dokumentáciu?
MCP (Model Context Protocol) server umožňuje AI pristupovať k aktuálnej dokumentácii priamo — namiesto spoliehania sa na zastarané tréningové dáta môže AI čítať živú, aktuálnu dokumentáciu knižníc a API.
Časť 8 — Skills a Custom Commands
18. Skills
Výhoda používania hotových skills?
Hotové skills obsahujú overené best practices a know-how — netreba AI znova vysvetľovať ako správne generovať daný typ výstupu (napr. PPTX, DOCX). Ušetrí sa čas a výsledok je konzistentnejší.
Časť 9 — Hooks a Plugins
20. Hooks
Po čom sa hook spustí? (príklad)
Po určitej akcii AI — napríklad po každom uložení súboru alebo po dokončení úlohy.
Čo hook vykoná? (príklad)
Automaticky spustí skript — napríklad spustí testy, linter alebo formátovač kódu po každej zmene súboru.
Časť 10 — Feedback Loops a Multi-Agent systémy
22. Feedback Loops
Čo robí AI v kroku 2 feedback loop?
AI analyzuje výsledky predchádzajúceho kroku (výstup testov, chyby, logy) a na základe nich opravuje kód alebo postup.
Čo umožňuje Playwright?
Playwright umožňuje automatizované end-to-end testovanie webových aplikácií — AI môže vidieť ako sa aplikácia správa v prehliadači a reagovať na chyby.
Aká je nevýhoda feedback loops? (spotreba)
Vysoká spotreba tokenov a času — každá iterácia generuje nové tokeny, dlhé smyčky môžu byť drahé.
Aké testy má AI tendenciu písať?
AI má tendenciu písať testy, ktoré prechádzajú (passing tests) namiesto zmysluplných testov — môže napísať testy šité na konkrétnu implementáciu.
Čo robiť s testami písanými AI?
Skontrolovať a revidovať ich — overiť, že testy skutočne testujú správanie, nie len to, že AI napísala to čo napísala.
23. Multi-Agent systémy
Pre čo sú Ralph Loops vhodné?
Pre dlhé, opakujúce sa úlohy kde jeden agent nestačí — napríklad rozsiahla refaktorizácia, generovanie veľkého množstva obsahu.
Čo je menšie pri Ralph Loops? (kontrola)
Kontrola nad jednotlivými krokmi je menšia — systém beží autonómne, človek nevidí každé rozhodnutie.
Čo stále potrebuješ? (plán)
Stále potrebuješ jasný plán a definovaný cieľ — bez dobrého zadania agenti produkujú nekvalitný výstup.
4 veci potrebné pre úspešný Ralph Loop:
•Jasné zadanie / špecifikácia cieľa
•Spôsob verifikácie výsledkov (testy, kritériá)
•Obmedzenia a guardrails (čo agenti nesmú robiť)
•Mechanizmus kontroly / ľudský oversight (review výsledkov)
Zhrnutie — Prehľad konceptov (spoj pojmy s definíciami)
24. Pojmy a definície (A–H)
•Context Window (A) — Maximálne množstvo textu/tokenov, ktoré AI vidí naraz v jednom rozhovore
•MCP (B) — Protokol umožňujúci AI pristupovať k externým nástrojom a dátam (databázy, API, dokumentácia)
•Plan Mode (C) — Režim, v ktorom AI najprv vytvorí plán riešenia a čaká na schválenie pred implementáciou
•Sandbox (D) — Izolované prostredie, kde AI môže vykonávať akcie bez rizika poškodenia reálneho systému
•Compaction (E) — Automatické zhutnenie starého kontextu keď sa context window plní
•Feedback Loop (F) — Cyklus kde AI vykoná akciu, vyhodnotí výsledok a iteratívne ho zlepšuje
•CLAUDE.md (G) — Súbor s projektovými inštrukciami, ktorý sa automaticky načíta ako súčasť systémového promptu
•Hooks (H) — Automatické akcie spúšťané po určitých udalostiach (napr. spustenie testov po uložení súboru)
Reflexia
Čo ma najviac zaujalo/prekvapilo:
Najprekvapivejšie je, ako veľmi záleží na context engineeringu — kvalita výstupu AI nezávisí len od samotnej AI, ale z veľkej časti od toho, ako dobre vieme formulovať kontext a inštrukcie. AI nie je "magic box", ale nástroj citlivý na vstupy.
Najväčšie výhody AI asistentov:
Obrovské zrýchlenie rutinných úloh (písanie boilerplate kódu, dokumentácia, refaktoring), schopnosť pracovať na viacerých súboroch naraz, a možnosť mať párové programovanie kedykoľvek bez potreby druhého človeka.
Najväčšie riziká:
Príliš veľká dôvera vo výstup AI bez overenia, strata schopnosti písať kód samostatne (závislosť), bezpečnostné riziká pri dangerous mode, a testy písané AI, ktoré netestujú to čo by mali.
Ako využiť vo svojich projektoch:
Zavediem CLAUDE.md do svojich repozitárov s jasnou špecifikáciou projektu, budem používať Plan Mode pred väčšími zmenami, nastavím hooks na automatické spúšťanie testov a pred každou väčšou AI-asistovanou zmenou vytvorím git commit ako záchytný bod.

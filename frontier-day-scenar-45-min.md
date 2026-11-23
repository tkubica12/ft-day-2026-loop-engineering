# Frontier Day: Od coding agenta k řízeným smyčkám

**Frontier Day · Tomáš Kubica a Valda z Cloudfieldu · 45 minut**  
Prvních 35 minut: principy a postupy použitelné dnes. Potom Tomášův blok čtyř spekulací o budoucnosti, následovaný Valdovým pohledem z praxe a závěrem.

## Hlavní linka

Nejde jen o rychlejší psaní kódu. Jde o celý systém, který převádí byznysovou potřebu na ověřený výsledek v produkci. Člověk určuje cíl, důkazy úspěchu a hranice; AI uvnitř tohoto prostoru hledá cestu a opravuje výsledek.

## Časová osa

| Čas | Blok | Valdův vstup |
| --- | --- | --- |
| 00:00–03:00 | 1. Proč nestačí coding agent | Příklad z praxe |
| 03:00–09:00 | 2. Goal Card a specifikace | Kde potřebuje spec-driven development a proč |
| 09:00–14:00 | 3. Inner loop | Vlastní či upravené skilly a jejich sdílení v týmu |
| 14:00–22:00 | 4. Outer loop: issues a PR | Jak dělá triáž a code review |
| 22:00–28:00 | 5. Byznysové požadavky a ADR | Jak používá ADR v shieldoo-gate |
| 28:00–33:00 | 6. Deployment, provoz a Azure SRE Agent | Volitelně zkušenost z provozu |
| 33:00–35:00 | 7. Deterministický rámec agentního systému | Jak hranice vynucují u nich |
| 35:00–42:00 | 8.–11. Tomáš: čtyři spekulace o příštím půlroce | — |
| 42:00–44:00 | Valda: co z toho už u vás začínáte vidět? | Naváže zkušenostmi z praxe |
| 44:00–45:00 | 12. Závěr | Cloudfield a Microsoft: jak s tím pomoci |

Časy zahrnují oba řečníky i přechody; samostatné Q&A není započteno.

## A. Co můžeme dělat dnes · 00:00–35:00

### 1. Proč nestačí coding agent · 3 min

**Tomáš:** Mezi „AI napsala kód“ a „zákazníkovi to spolehlivě pomáhá“ je velký kus práce. Ukázat celou mapu: potřeba → Goal Card → realizace → PR → ověření → nasazení → provoz → nová potřeba.

Jako společný příklad lze použít retail z původního workshopu: při odmítnutí rezervace pracovník nevidí dostupné množství. Začínáme problémem uživatele, ne pokynem „přidej komponentu“.

**Valda:** Přidá konkrétní příklad z praxe, na kterém je vidět, že samotné generování kódu nestačí.

### 2. Goal Card: cíl, ne seznam kroků · 6 min

**Tomáš:** Goal Card říká, čeho dosáhnout, jak úspěch ověřit, co agent nesmí a kdy se musí zastavit. Ilustrační výřez: při požadavku na 5 kusů se zásobou 4 zobrazit „dostupné 4“; nevytvořit částečnou rezervaci, neměnit API a neoslabovat akceptační kritéria. Překročení rozsahu nebo limitu znamená zastavení, ne náhradní úspěch.

**Valda:** Kde potřebuje spec-driven development a proč? Co musí být určeno předem, aby mohl agent bezpečně pracovat? Cíl a důkazy nejsou totéž co detailní návrh; kde potřebuje pevné kontrakty nebo architektonická rozhodnutí?

### 3. Inner loop: vytvořit, ověřit, upravit · 5 min

**Tomáš:** Agent posoudí stav, provede změnu, spustí kontroly a podle výsledku opravuje. Autonomie neznamená absenci zpětné vazby; znamená, že ji člověk nemusí ručně dodávat po každém kroku. Výstupem je změna s důkazy, předaná do PR. Případná krátká ukázka bez čekání na živé generování.

**Valda:** Jaké vlastní nebo upravené skilly používají, k čemu je vytvořili a jak je sdílejí a udržují v rámci týmu? Konkrétní příklad, jak agentovi předávají týmové know-how.

### 4. Outer loop: od issue přes PR k přijetí změny · 8 min

**Tomáš:** Z podnětu vzniká issue, proběhne triáž a realizace. PR propojí inner loop s týmovým procesem: bezpečnostní a kvalitativní kontroly, testy, kontrola kontraktů, doplnění dokumentace a review vůči cíli. Nálezy se vracejí k opravě; schválení a nasazení mají vlastní pravidla. AI review doplňuje důkazy, nenahrazuje vynucené kontroly.

**Valda:** Jak u nich konkrétně dělá triáž a code review? Co už deleguje AI, co si nechává a podle čeho poznává, že je změna připravená k přijetí?

### 5. Mimo kód: byznysové požadavky a ADR · 6 min

**Tomáš:** Rozhovor s byznysem nebo oprávněně pořízený záznam práce na obrazovce může být vstupem pro návrh PRD, user stories a Goal Card. AI pomáhá formulovat potřebu; vlastník potvrzuje záměr. Na druhé straně může vznikat ADR a kontrola, zda jeho předpoklady stále platí. Agent navrhuje revizi, sám neruší historická rozhodnutí.

**Valda:** Jak používá ADR v **shieldoo-gate**? Jak je vytváří, vrací se k nim a zapojuje je do práce s agenty?

### 6. Deployment, provoz a Azure SRE Agent · 5 min

**Tomáš:** Nasazení, ověření a možnost návratu jsou součástí smyčky. Příklad: rostoucí spotřeba paměti → Azure SRE Agent shromáždí signály a navrhne mitigaci → v povoleném režimu a rozsahu ji provede → ověří účinek → přes nakonfigurovaný konektor vznikne issue pro trvalou opravu. Navýšení paměti nebo restart mohou zmírnit symptom, ne odstranit leak.

**Valda (volitelně):** Jak dnes u nich vypadá cesta od provozního incidentu k trvalé opravě?

### 7. Volnost agenta uvnitř deterministického rámce · 2 min

**Tomáš:** Cílem je velká volnost při hledání řešení, ale technicky omezené dopady: sandbox, identita s omezenými právy, povolené nástroje, chráněné kontroly a schvalovací brány. Goal Card popisuje hranice, sama je nevynucuje. Ani další AI reviewer není sám o sobě nepřekročitelnou bezpečnostní hranicí.

**Valda:** Jak to řeší u nich — co agentům dovolují a čím skutečně vynucují, co dělat nesmějí?

## B. Tomáš: co by se mohlo změnit v příštím půlroce · 35:00–42:00

Dosud šlo o použitelné principy a dnešní postupy. Teď čtyři spekulace: příští půlrok je horizont k zamyšlení, ne termín slíbené změny. Nejde o tvrzení, že už dnes nepotřebujeme testy, abstrakce nebo lidské review.

> „AI má jiné silné stránky a limity než lidský mozek. Co když proto přestanou být optimální některé postupy, které jsme vytvořili hlavně pro sebe?“

### 8. Testovací pyramida může změnit tvar

Dnes máme hodně unit testů a méně E2E mimo jiné kvůli ceně tvorby, údržby a spouštění. E2E test se může rozbít změnou UI, přestože byznysový průchod stále funguje. Proto často hlídáme jen základní cestu: produkt → košík → doprava → platba. Další cesty přes vyhledávání, recenze nebo asistenta takto nepokrýváme.

**Spekulace:** Pokud AI výrazně zlevní tvorbu a údržbu E2E, můžeme ověřovat mnohem více skutečného byznysového chování. A pokud bude v atomických implementačních úlohách natolik spolehlivá, že tam bude dělat podstatně méně chyb, část jednoduchých unit testů může mít malý přínos — být „vyhozené tokeny“. Těžiště ověřování by se posunulo výš.

Není to doporučení dnes unit testy zahodit. Levnější údržba neodstraní flaky prostředí ani problém správného očekávaného výsledku: AI smí opravit ovládání UI, ne přepsat význam úspěšné objednávky.

### 9. Některé abstrakce mohou AI spíš překážet

Lidem často není nejasný princip; jen nedokážou udržet všechny detaily v hlavě. Schováváme je proto za rozhraní a vrstvy: cloudová API → Terraform → moduly nad Terraformem. Díky menšímu počtu „hejblátek“ se v systému vyznáme.

**Spekulace:** AI může mít jiný poměr nákladů. Práce s velkým množstvím explicitních detailů pro ni může být snazší než rozplétání několika našich abstrakcí. Některé vrstvy vytvořené pro lidskou orientaci se tak mohou stát zbytečnou zátěží. Možná budeme navrhovat jinak, pokud bude primárním autorem a čtenářem agent.

AI ale nemá neomezený kontext a abstrakce neslouží jen paměti: Terraform řeší také stav a závislosti, kontrakty zase koordinaci a bezpečnost. Teze míří na přehodnocení vrstev, ne na jejich plošné odstranění.

### 10. DRY může mít jinou ekonomiku

DRY — Don't Repeat Yourself — snižuje cenu konzistentních změn: pro člověka je těžké najít a správně upravit pět implementací stejné znalosti. Pokud AI tuto práci výrazně zlevní, může se změnit kompromis mezi sdílením a nezávislostí jednotlivých částí.

**Spekulace:** Větší různorodost může znamenat více potenciálních slabin, ale méně společných selhání. Chyba jedné sdílené komponenty zasáhne všechny její uživatele; pět dostatečně odlišných implementací nemusí sdílet tutéž zranitelnost. V prostředí AI útoku i obrany možná začneme jinak vážit attack surface proti blast radius.

Samotná duplicita ovšem blast radius nesnižuje. Potřebujeme skutečnou izolaci oprávnění, dat a běhu i reálnou diverzitu; AI může stejnou chybu zopakovat všude. Nejde o oslavu kopií, ale o otázku, zda se vyplatí méně společných bodů selhání.

### 11. Lidské review se může přesunout od kódu k pravidlům přijetí

Pokud bude AI v implementaci běžných úloh spolehlivější než člověk, který ji kontroluje, nemusí být nejlepší využití lidského času pročítat každý řádek. Co má potom znamenat human in the loop?

**Spekulace:** Těžiště se přesune k review cíle, hranic a hlavně mechanismu, který rozhoduje o přijetí výsledku. Nejen „vyzkoušel jsem funkcionalitu“, ale „zkontroloval jsem, že testy skutečně prokazují požadované chování a hlídají zakázané dopady“. Agent nesmí mít možnost upravit si pravidla, podle kterých dostane zelenou.

To navazuje na dnešní deterministický rámec z bodu 7, ale nová je možná změna hlavní náplně lidské práce. Člověk navrhuje a kontroluje pravidla hry, ne každý tah. Ani deterministický test nemusí ověřovat správnou věc; smysl kritérií a přijaté riziko zůstávají lidskou odpovědností. Expertní code review může dál zůstat zásadní u kritických nebo obtížně testovatelných změn.

## C. Valda: co z toho už u vás začínáte vidět? · 42:00–44:00

**Tomáš → Valda:** „Co z toho už u vás začínáte vidět? Kde ti tyhle teze sedí na vlastní zkušenost a kde naopak ne?“

**Valda:** Pohled na čtyři teze jako celek, s příklady nebo protiargumenty z jejich praxe.

## 12. Závěr · 44:00–45:00

Vrátit se k tomu, co si má publikum odnést už dnes: **goal určuje výsledek a hranice, inner loop hledá a ověřuje řešení, outer loop propojuje tým, nasazení a provozní zpětnou vazbu.** Úspěch měříme přijatým výsledkem, ne počtem vygenerovaných řádků.

> „Budoucí podobu vývoje teprve hledáme. Ale s cíli, řízenými smyčkami a bezpečnými hranicemi můžeme začít už dnes. Cloudfield vám pomůže tenhle způsob práce zavést do praxe a Microsoft pro něj má skvělé produkty — od GitHub Copilotu a GitHub platformy po Azure a Azure SRE Agent.“

---

**Podklady:** [Česká prezentace Loop Engineering](https://github.com/tkubica12/github-loop-engineering/blob/c59fe829387af0055dfa78fe8fc5b7859bc827e0/docs/loop-engineering.cs.html), [agenda workshopu](https://github.com/tkubica12/github-loop-engineering/blob/main/AGENDA.md) a [příklad Goal Card](https://github.com/tkubica12/github-loop-engineering/blob/main/docs/labs/02-inner-loop/artifacts/partial-stock-visibility.goal-card.md). Azure SRE Agent: [mitigace](https://learn.microsoft.com/azure/sre-agent/execute-mitigations) a [režimy schvalování](https://learn.microsoft.com/azure/sre-agent/run-modes); možnosti závisejí na konfiguraci a oprávněních. Čtyři budoucí teze jsou autorská diskusní část, nikoli závěry těchto zdrojů.

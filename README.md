# Loop Engineering: držte laťku, ne agenta za ruku

Společné vystoupení Tomáše a Valdy na Frontier Day 2026. Po naklonování otevři v prohlížeči [prezentace/frontier-day.html](prezentace/frontier-day.html). Slidy fungují offline, bez buildu a přihlášení. Šipky listují, klávesa `O` otevře přehled.

## Valdo, kde začít

Nejdřív doplň vlastní příklady na dvou místech, kde je zatím jen nadpis:

| Slide | ID v HTML | Co doplnit |
| --- | --- | --- |
| 3 | `s-shieldoo-gate` | Příklad ze Shieldoo-gate: co kromě napsání kódu rozhodlo o výsledku? |
| 10 | `s-valda-practice` | Jak vypadá cesta jednoho podnětu od triáže přes implementaci po přijetí a provoz? |

Další tvoje vstupy jsou na slidech **5** (SDD), **8** (týmové skilly) a **13** (přijetí změny). Na **15** se střídáte u vynucování hranic. Na **18–21** patří pravý textový box tvému komentáři ke každé hypotéze; klidně nech zaznít i nesouhlas.

Text upravuj přímo v HTML podle `id` slidu. Původní [45minutový scénář](frontier-day-scenar-45-min.md) je podklad, nikoli aktuální číslování. [Veřejné zdroje](prezentace/zdroje.json) jsou oddělené od prezentace. Soukromá příprava a e-maily nejsou součástí repozitáře.

## Skilly a kontrola změn

V [`.agents/skills/`](.agents/skills/) jsou tři projektové skilly s licencemi: `html-docs` pro úpravy slidů, `web-research` pro ověření zdrojů a volitelný `image-generator`. Běžná úprava existujících slidů nevyžaduje Azure, WorkIQ ani generování obrázků. Pro nové obrázky použij vlastní oprávnění, schválený zdroj Python závislostí a samostatně odsouhlasený rozpočet.

Kontrola z kořene repozitáře (Node.js; druhý příkaz navíc vyžaduje Playwright a Chromium):

```sh
node prezentace/assets/sync-head.js --check prezentace/frontier-day.html
node prezentace/assets/validate.js prezentace/frontier-day.html --viewport 1920x1080
```

Pokud validátor instalaci nenajde, nastav `PLAYWRIGHT_MODULE` na umístění modulu a `PLAYWRIGHT_CHROMIUM` na spustitelný soubor prohlížeče. Samotné promítání tyto nástroje nepotřebuje.

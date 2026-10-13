# Clientelo_Czech_miniprojekt

Vybral jsem si zadaní A jelikož je mi to bližší, ze zadání jsem pochopil že chcete datový sklad investorů s jejím ohodnocením a scaleingem.

v projektu je soubor investoři-kostka.xml lze jej otevřít pomocí grafického designu(.html) poslaný emailem.

než začnu je potřeba rozmyslet architektonická rozhodnutí, dopady, otázky a udělat celou pipeline.

kde nabrat data, jak vypadají, a jaké informace mě zajímají?

jakou db použít oracle, psgSQL, mysql, vektorová db? ja bych si zvolil oracle, protože dělam projekt v oracle db

jaké jazyky použít? vybral bych si kompilované z důvodu plus vrstvy ochrany jako Java, ale můžou být jiné.

github nebo gitlab? ja bych si zvolil github kvůli ci/cd

CI/CD? GitHub Actions

claud: AWS, Google, microsoft?

frontend? Angular, React, Vue netuším asi React

secutity a bezpečnost? sha-256, nebo argon2, záleží na případech argon2 trva déle, proto bych ho použil pro autentizaci. sha-256, bych použil na zbytek např. kontrolu souborů




## jak bych postupoval

1.dodělal bych svůj projekt orm(torm), to by byla kostra projektu viz. obrázek upně dole

základní kamen, pro modelování systémů je mít správný data model který například umí vytvářet power designer (roční licence asi 80k). důležité u těchto systémů je funkce datalineage.
ja bych si ale na vibecodoval vlastní modelovací system a přidal funkci generování ORM který by řešil problém (https://blog.codinghorror.com/object-relational-mapping-is-the-vietnam-of-computer-science/)

takový nástroj by měl roli kostry projektu, generoval by Model.xml, ORM kod, SQl pro migraci, dokumnetaci. Jeho výhoda by byla konzistentnost jelikož bude generovaný generátorem a ne AI.
nevýhoda torm je wip, orm je zatím pro stack java, oracle db. Data lineage, dopadová analýza a data cubes jsou provizorně dělaný. migrace nejsou otestovný

# pipelina Torm canvas, generování orm, sql migrací, datacubes

<img width="3824" height="1624" alt="torm-architektura" src="https://github.com/user-attachments/assets/f1873a9a-4d93-4123-bd0d-c80ac5c33351" />

## nasávání dat

potřeba mít už rozvržený datový sklad. Jelikož je důraz na scaling, musí se hlídat naročnost cacheování a optimalizace paměti. Proto bych použil přístup STAX nebo SAX, při nahrávání velkého objemu dat.
využití batch operací v db.

při procesu nasání dat musí být validace dat př. Email(regex), a chtěl bych vidět edgecases kde nám data neprojdou do db z důvodu validací, a za druhé kdy data budou špatné naší vinou, špatné párování invesotů, protože se jmenujou stejně

velký problém bude jak identifikovat investora, může být totiž na několika místech zároveň u nás v db, ze zdroje z Ameriky, či Singapuru. daší problém jsou dva investoři a jmenují se stejně ale jsou to jiné osoby. Netuším jak takovou věc dělat, možná statistika? Nevím

## porovnání investorů

z datového skladu můžem jak zkoušet investorumů dát hodnocení, první věc mě napadla použít fuzylogiku, ale bude lepší použít více algoritmů jako je Vážený součet, Ostrá pravidla / rozhodovací strom, Scorecard. dokázal bych si tady představit datovou kostku, asi bych jí dělal jako view.

## metriky a trackování

metriky a trackování role zpětná vazba, system musí mít trekování pro odhalení bottlenecků

chtěl bych tam mít statistiky z db, jak moc je zdravá, statistiku serveru. chtěl bych aktualní i historická data o systemu. informace o zdrojích

## scaleing

největší problém budou rozhodnutí která se udělají teď a v budoucnu to zavře dveře. například zvolení špatné db protože oracle má Autonomní databáze (Autonomous Database) a jiné nemají


## co bych se musel naučit

CI/CD, Fuzi logiku, AI Agenti, Claud

očekávám že věci co se ještě naučit je spousta ani o nich nic nevím

## graf jak by mohla vypadat pipelina toku dat
<img width="2804" height="1424" alt="torm-sklad" src="https://github.com/user-attachments/assets/be49b247-3936-41b4-9f6e-f89e9bea1d44" />

## jak si představuju cyklus vývoje 

<img width="2904" height="2124" alt="torm-cicd" src="https://github.com/user-attachments/assets/9e7ff32c-d879-402e-8d6a-a26433db29a3" />

## TORM CANVAS

<img width="1857" height="902" alt="image" src="https://github.com/user-attachments/assets/365e4c90-b200-4c99-a9ae-da394cc6cb4f" />


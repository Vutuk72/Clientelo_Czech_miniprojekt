# Clientelo_Czech_miniprojekt

Vybral jsem si zadaní A jelikož je mi to bližší, ze zadání jsem pochopil že chcete datový sklad investorů s jejím ohodnocením a scaleingem.

než začnu je potřeba rozmyslet architektonická rozhodnutí, dopady, otázky a udělat celou pipeline.

kde nabrat data, jak vypadají, a jaké informace mě zajímají?
jakou db použít oracle, psgSQL, mysql? ja bych si zvolil oracle, protože dělam projek v oracle
jaké jazyky použít? vybral bych si kompilované z důvodu plus vrstvy ochrany jako Java, ale můžou být jiné.
github nebo gitlab? ja bych si zvolil github kvůli ci/cd
CI/CD? GitHub Actions
claud: AWS, Google, microsoft?
frontend? Angular, React, Vue netuším asi React
secutity a bezpečnost? sha-256, nebo argon2, záleží na případech argon2 trva déle, proto bych ho použil pro autentizaci. sha-256, bych použil na zbytek např. kontrolu souborů


## jak bych postupoval

1.dodělal bych svůj projekt orm(torm), to by byla kostra projektu viz. fotky

základní kamen, pro modelování systémů je mít správný data model který umí vytvářet power designer (roční licence asi 80k). důležité u těchto systémů je funkce datalineage.
ja bych si ale nakodoval vlastní modelovací system a přidal funkci generování ORM který by řešil problém (https://blog.codinghorror.com/object-relational-mapping-is-the-vietnam-of-computer-science/)

takový nástroj by měl roli kostry projektu, generoval by Model.xml, ORM kod, SQl pro migraci, dokumnetaci. Jeho výhoda by byla konzistentnost jelikož bude generovaný generátorem a ne AI.
nevýhoda torm je wip, orm je zatím pro stack java, oracle db, data lineage a dopadová analýza funguje nevím jak dobře, data cubes jsou provizorně dělaný. migrace nejsou otestovný

## nasávání dat

potřeba mít už rozvržený datový sklad. Jelikož je důraz na scaling, musí se hlídat naročnost cacheování a optimalizace paměti. Proto bych požil přístup STAX nebo SAX, při nahrávání velkého objemu dat.
využití batch operací v db.

při procesu nasání dat musí být validace dat př. Email(regex), a chtěl bych vidět edgecases kde nám data neprojdou do db z důvodu validací, a za druhé kdy data budou špatné naší vinou, špatné párování invesotů, protože se jmenujou stejně

velký problém bude jak identifikovat investora, může být totiž na několika místech zároveň u nás v db, ze zdroje z Ameriky, nebo ze Singapuru. daší problém jsou dva investoři a jmenují se stejně ale jsou to jiné osoby. Netuším jak takovou věc dělat, možná statistika? Nevím

## porovnání investorů

z datového skladu můžem už zkoušet investorumů dát hodnocení, první věc mě napadla použít fuzylogiku, ale bude lepší použít více algoritmů jako je Vážený součet, Ostrá pravidla / rozhodovací strom, Scorecard. dokázal bych si tady představit datovou kostku, asi bych jí dělal jako view.

## metriky a trackování

role byla by to důležitá zpětná vazba, system musí mít trekování pro odhalení bottlenecků 

chtěl bych tam mít statistiky z db, jak moc je zdravá, statistiku serveru. 

## co bych se musel naučit

CI/CD, RUST, Fuzi logiku, 

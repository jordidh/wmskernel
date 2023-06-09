## Idea
Desenvolupar un software capaç de realitzar les operacions bàsiques amb estocs i contenidors/ubicacions per poder gestionar magatzems.
Aquest software només ha de fer això però ho ha de fer molt bé.

## Operacions bàsiques

### Decisió 1: És útil el software que es proposa?
Aquest software, a partir de estocs i contenidors/ubicacions realitzarà una sèrie d'operacions i retornarà el resultat en forma de estocs resultants.
No guardarà a la BD ni recuperarà de la BD, això es deixa pel software que el cridi.
Pot guardar dades de moviments d'estoc en una BD en el cloud com a un servei extra.

Dubtes:
1. Qui el podria fer servir?
	1. Per clients que es puguin desenvolupar la UI: Si es simplifica el desenvolupament d'eines clients, UI, etc.. a partir d'un estandard d'API REST (estandard de comunicación actual), de plataformes de desenvolupament [No-code](https://en.wikipedia.org/wiki/No-code_development_platform) o  [low-code](https://en.wikipedia.org/wiki/Low-code_development_platform) pot ser útil proporcionar les operacions més complexes (estocs i cont/ubic) a aquests softwares. Atenció: ha arribat el moment que això sigui possible?
	2. Per clients que tinguin un WMS i aquest software proporcioni unes operacions més robustes que les seves. Idea: Onion pot fer-ho servir.
2. Li facilitaria la vida o no?
	1. Les operacions de recuperar les dades de la BD i guardar-les a la BD, igualment, les hauria de fer l'aplicació client.
3. El que es cobraria seria prou competitiu com per ser atractiu pels clients? Quin seria el nostre cost (Google Run - cost per crida, BD en el cloud que guardi traces i dades de les crides) [Càlcul de preus de Google](https://cloud.google.com/products/calculator)?

Com podem resoldre aquests dubtes?
1. Estudiar quines necessitats té un WMS i quin tipus de clients podria necessitar un software així.
2. Fer un prototipus (fer servir serverless per reduïr costos de desenvolupament i desplegament) per determinar si seria viable. Anar amb la idea "fail first" (desenvolupar les idees que tinguin un impacte més important primer, si hem de veure que no serveix detectem-ho com més aviat millor).

### Decisió 2: Nivell de granularitat de les API?
Podem proporcionar:
1. Poques operacions i molt generals: redueix la flexibilitat a l'hora d'utilitzar-la i dificulta reutilitzar-la.
2. Moltes operacions i molt específiques: pot obligar a fer moltes crides per realitzar una operació, però és molt flexible (es pot utilitzar en molts casos).
3. Un punt intermig.

### Decisió 3: Nivell de transparència
S'ha d'estudiar quin nivell de transparència es vol donar, s'ha de definir clarament que fem amb les dades que processem i si les guardem i perquè?

### Primera proposta d'operacions
Les operacions bàsiques amb estocs i contenidors poden ser:
- Creació d'estoc en un contenidor/place + fusió si és possible
- Modificació d'estoc en un contenidor/place + fusió si és possible
- Eliminació d'estoc d'un contenidor/place
- Moure estoc entre contenidors/places + fusió si és possible
- Canvi d'estat (afegir/modificar/eliminar) d'estoc en un contenidor/place + fusió si és possible
- Picking d'un estoc d'un contenidor/place (de tot l'estoc o d'una part) per una ordre
- Put d'un estoc a un contenidor/place per una ordre + fusió si és possible
- Desempaquetat d'un estoc d'un contenidor/place  + fusió si és possible
- Empaquetat d'un estoc d'un contenidor/place  + fusió si és possible

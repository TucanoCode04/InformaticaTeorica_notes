#### Godel
**Entscheidungsproblem:**
- Dato un sistema deduttivo P e una formula F, esiste una dimostrazione di F in P?

Sappiamo, però, anche che se restringiamo la lunghezza delle formule, il problema diventa decidibile.
- Dato un sistema deduttivo P e una formula, esiste una dimostrazione di lunghezza $\leq n$ in P?

**Funzione di Godel:**
- $\phi: \text{lunghezza n massima della dimostrazione da trovare} \rightarrow \text{nunero di passi computazionali di una TM}$

*La congettura di Gode:* $\phi(n)$ è un polinomio $Kn^2$, per qualche K. Quindi appartiene alla classi di complessità P(computazione polinomiale).

#### Misurare la complessità
**Notazione big-O:** $\newline$
Date funzioni $f, g: \mathbb{N} \rightarrow \mathbb{N}$, scriviamo $f(n) = O(g(n))$ e diciamo che $g(n)$ è un bound superiore asintotico se esistono $c \in \mathbb{N}$ e $m \in \mathbb{N}$ tali che per ogni $n \geq m$ vale $f(n) \leq c \cdot g(n)$.
In altre parole, $g(n)$ è sempre grande almeno quanto $f(n)$ per $n$ sufficientemente grande e modulo un fattore costante c.

**Considerazioni:**
L'analisi asintotica non risolve tutte le fragilità della misurazione di complessità. 
Algoritmi differenti hanno complessità differenti anche per lo stesso problema.
### Classi di complessità
**TIME:**
- data una funzione $f : \mathbb{N} \times \mathbb{N}$ definiamo la classe di complessità $TIME(t(n))$ come la collezione di tutti i linguaggi decidibili da una TM(deterministica, a un nastro) in tempo $O(t(n))$

#### La classe P
**Definizione:** 
$P$ è la classe dei linguaggi decidibili da una TM(deterministica, a un nastro) in tempo polinomiale. Ovvero: $$P = \bigcup_{k} TIME(n^k)$$

Si utilizza P, perchè un algoritmo che lavora in tempo polinomiale viene considerato efficiente

La maggioranza delle codifiche di strutture dati in stringhe richiede tempo polinomiale e produce una stringa di output di lunghezza polinomiale rispoetto all'input(con eccezione della codifica unaria di un numero naturale: 5 = 11111)

**Tesi di Chruch Turing rafforzata:**
Ogni modello di calcolo deterministico fisicamente realizzabile può essere simulato da una TM(deterministica, su nastro singolo) con overhead al più polinomiale.

*In altre parole:* $m$ passi di computazione del modello in questione possono essere msimulati dalla TM in al più $O(m^c)$ passi per una costante $c$

*Considerazioni:*
se ver, la tesi dice che la classe $P$ è robusta, invariante rispetto al modello di computazione deterministico scelto.

*TM con $k$ nastri:*
Ogni TM con un nastro può simulare in tempo $O(t^2(n))$ una con k nastri che lavori in $t(n)$.

#### La classe EXP
**Definizione:**
$EXP$ è la classe dei linguaggi decidibili da una TM(deterministica, a un nastro) in tempo esponenziale. Ovvero: $$EXP = \bigcup_{k} TIME(2^{n^k})$$

##### PATH
$PATH = \{\langle G, s, t\rangle | \text{ G è un grafo diretto che ha un percorso diretto da s a t }\}$

**Teorema:**
$PATH$ è in $P$

**Dimostrazione:**
Consideriamo il seguente algoritmo su input $\langle G, s, t\rangle$ :
1. Contrassegna il nodo $s$.
2. Scansiona tutti gli archi di $G$. Se trovi un arco da nodo $a$ contrassegnato ad un nodo $b$ non contrassegnato, contrassegna il nodo $b$.
3. Se $t$ è contrassegnato, accetta. Se no, rigetta.

*Analisi del costo computazionale:*
I punti $1.$ e $3.$ sono ovviamente in $P$. Il punto $2.$ è ripetuto al massimo per il numero di nodi di $G$. Quindi l'agoritmo è in $P$.

**Analogo per $EXP$:**
Esamino tutti i percorsi diretti in $G$, alla ricerca di uno da $s$ a $t$.

*Analisi di complessità:*
Il numero potenziale di percorsi è $n^n$. Quindi ha complessità esponenziale.

**Considerazioni sulla codifica:**
Come sappiamo da prima, una qualsiasi codifica produrrà una stringa in tempo polinomiale e di dimensione al massimo polinomiale rispetto all'input. Quindi non ci interessa la codifica del grafo, va bene dare per ragionare sui nodi dando per scontato che la codifica sia eseguita in tempo ragionevole.

#### Problemi in P
- n è primo? In $P$
- il grafo $G$ è connesso? In $P$
- data un regex $r$ e la stringa $s$, $s$ è in $L(r)$? In $P$
- date regex $r, s$, $L(r) = L(s)$? In $PSPACE$
- problema del commesso viaggiatore? In $NP$
- dalla posizione $P$ in una partita di scacchi, quale giocatore ha una strategia vincente? In $PSPACE$

#### La classe NP
**NTIME:**
- data una funzione $f : \mathbb{N} \times \mathbb{N}$ definiamo la classe di complessità $NTIME(t(n))$ come la collezione di tutti i linguaggi decidibili da una TM(non-deterministica, a un nastro) in tempo $O(t(n))$
$$NP = \bigcup_{k} NTIME(n^k)$$

**Definizione**
Dato un grafo indiretto, un *Clique* è un sotto-grafo dove tutti i nodi sono collegati tra loro da un arco.

**Problema:**
$CLIQUE = \{\langle G, k \rangle\ | \text{ il grafo G contiene un clique di k nodi } \}$

$CLIQUE$ è in $NP$. 
Questo è un algoritmo non-deterministico polinomiale che lo calcola, su input $\langle G, k \rangle$:
1. Seleziona non-deterministicamente un sottoinsieme $C$ di $k$ nodi di $G$.
2. Verifica che $G$ colleghi tutti i nodi di $C$ tramite archi. Se sì, accetta. Altrimenti rigetta.

**Definizione alternativa di NP:**
Un linguaggio $A$ è *verificabile* se esiste una TM M(che termina sempre, ed accetta o rigetta) con la proprietà: $w \in A \Leftrightarrow \text { esiste una stringa c tale che M accetta } \langle w, c \rangle$
Se M lavora in tempo polinomiale, diciamo che $A$ è *verificabile polinomialmente*.

($w$ è la stringa di input, $c$ funge da certificato per $w$, nel senso che dimostra che $w$ appartiene al linguaggio, per esempio in $CLIQUE$: $w = \langle G, k \rangle$ e $c = \text{clique di k nodi in G}$)

**Teorema:**
Un linguaggio è in $NP$ se e solo se è verificabile polinomialmente.

**Dimostrazione:**
($\Rightarrow$)
Sia M una TM non-deterministica che decide un linguaggio $L$ in tempo polinomiale. Costruiamo un verifcatore $V$ polinomiale per $L$ nel seguente modo, su input $\langle w, c \rangle$:
1. Simula M su $\langle w, c \rangle$, dove $c$ saranno le scelte non-deterministiche da prendere nell'albero di computazione codificate.
2. Se il ramo di computazione scelto da $c$ è accettante, accetta.

($\Leftarrow$)
Sia $V$ un verificatore polinomiale per $L$. Cortuiamo una TM M non-deterministica che decide $L$ nel seguente modo, su input $w$ di lungezza $n$:
1. Seleziona non-deterministicamente una stringa $c$ di lunghezza al più $n^k$(lunghezza di $w$).
2. Simula $V$ su input $\langle w, c \rangle$.
3. Se $V$ accetta, accetta. Se no, rigetta.

In altre parole: Esiste $c$ tale che $V$ accetta $\langle w,c \rangle$ se e solo se M accetta $w$.

*Esempio:*
facciamo un verificatore polinomiale per $CLIQUE$. Il certificato $c$ è il clique stesso.

Su input $\langle \langle G, k \rangle , c \rangle$:
1. Verifica che $c$ sia un sottografo di $k$ nodi in $G$.
2. Verifica se ogni nodo in $c$ sia collegato a qualsiasi altro nodo in $c$ da un arco
3. Se entrambi i test sono positivi, accetta. Altrimenti rigetta.

#### P vs NP
- $P$ è la classe di linguaggi $A$ per cui la domanda "$w \in A$?" può essere *risposta* in tempo polinomiale
- $NP$ è la classe di linguaggi $A$ per cui la corretteza di una risposta alla domanda "$w \in A$?" può essere *verificata* in tempo polinomiale

Si è iniziato cercando di dimostrare che $P \neq NP$, fallendo. Però dall'altra parte non riusciamo nemmeno a risolvere un problema in $NP$ con un algoritmo polinomiale.
La risposta si pensa non-costruttiva in quanto l'algoritmo che ptoremmo trovare potrebbe essere eccessivamente complicato. E' stato dimostrato da Robertson e Seymour che un problema in toeria dei grafi è in $P$, però non è stato esplicitato nessun algoritmo.

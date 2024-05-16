### Teorema di Cook-Levin
**Definizione:**
Se $SAT \in P$ allora $P = NP$

Definiremo $SAT$ come $NP-COMPLETO$, se fosse in $P$ allora sarebbero in $P$ tutti i problemi di $NP$.
Dimostreremo che qualsiasi problema in $NP$ riducibile in tempo polinomiale a $SAT$.

#### Poly Reduction
**Definizione:**
Siano $L$ e $L'$ linguaggi sull'alfabeto $\Sigma$. Diciamo che $L'$ è poly (mapping-)riducibile a $L$, scritto $L' \leq_p L$, se esiste una TM che computa *in tempo polinomiale* una funziona(totale) $f : \Sigma^* \rightarrow \Sigma^*$ tale che $x \in L' \Leftrightarrow f(x) \in L$.

In altre parole: $L' \leq_p L$ se $L' \leq L$ e la riduzione è computabile in tempo polinomiale.

**Teorema:**
Se $L' \leq_p L$ e $L \in P$, allora $L' \in P$.

**Dimostrazione:**
DA FARE

**Teorema:**
Per $L$ non triviale in $P$, $L^- \leq_p L $.

**Dimostrazione:**
DA FARE

**Domanda:**
Per $L$ non triviale in $NP$, $L^- \leq_p L $?

**Risposta:**
DA FARE

#### Formule booleane
**Definizione:**
Un *formula booleana* è composta da variabili $x, y , ..., \bar{x}, \bar{y}, ... \in \{0, 1\}$ e le loro combinazioni tramite $\land$ e $\lor$

**Soddisfacibilità:**
Una formula è *soddisfacibile* se esiste un assegnamento di valore alle sue variabile che le dia valore 1

*Esempio:*
La formula $(\bar{x} \lor y) \land (x \lor y)$ è soddisfacibile per $x = 1, y = 1, z = 0$

**Clausola:**
Una formula è una *clausola* se è una disgiunzione di variabili.

**CNF:**
Una formula è una *forma normale congiunta* se è una congiunzione di *clausole*

*Esempio:*
$(x \lor y) \land (\bar{z} \lor z) \land (\bar{x} \lor y \lor z \lor \bar{z})$

**3CNF:**
Una formula è $3CNF$ se è in *cnf* e ogni *clausola* contiene esattamente 3 letterali.

#### $3SAT \leq_p CLIQUE$
**Definizione:**
$SAT = \{\langle F \rangle\ | F \text{ è una formula booleana soddisfacibile }\}$
$3SAT = \{\langle F \rangle\ | F \text{ è una formula booleana 3cnf soddisfacibile }\}$

La riduzione è interessante perchè collega un problema sulle formule logiche a uno sui grafi.

**Teorema:**
$\langle F \rangle\ \in 3SAT \Leftrightarrow f(\langle F \rangle) \in CLIQUE$

**Dimostrazione:**
*Idea:* 
Tradurremo formule in grafi, dove $f(\langle F \rangle)$ sarà costruito in modo da mimare il comportamento di variabili e clausole: un clique f(\langle F \rangle) corrisponderà ad un assegnamento che soddisfa $\langle F \rangle$.




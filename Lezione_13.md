### Complessità di spazio
**Definizione:**
Data una funzione $t : \mathbb{N} \rightarrow \mathbb{N}$, definiamo la classe di complessità di spazio $SPACE(t(n))$ come l'insieme dei linguaggi decidibili da una macchina di Turing(deterministica, a un nastro) in spazio $O(t(n))$.

**Definizione:**
Data una funzione $t : \mathbb{N} \rightarrow \mathbb{N}$, definiamo la classe di complessità di spazio $NSPACE(t(n))$ come l'insieme dei linguaggi decidibili da una macchina di Turing(non deterministica, a un nastro) in spazio $O(t(n))$.

**Definizione:**
$PSPACE$ è la classe dei linguaggi decidibili da una macchina di Turing deterministica in spazio polinomiale.
$$PSPACE = \bigcup_{k \in \mathbb{N}} SPACE(n^k)$$

**Definizione:**
$NPSPACE$ è la classe dei linguaggi decidibili da una macchina di Turing non deterministica in spazio polinomiale.
$$NPSPACE = \bigcup_{k \in \mathbb{N}} NSPACE(n^k)$$

Il fatto che $P$ sia inclusa in $PSPACE$ è ovvio. 
E' meno ovvio(anche se è vero) che $NP$ sia inclusa in $PSPACE$.

**Lemma:**
$SAT \in PSPACE$

**Dimostrazione:**
Costruiamo una TM M che su input $\langle F \rangle$, formula booleana:
- Per ogni assegnamento $A$ di valore alle variabili di $F$:
    - Verifica se $F$ rispetta $A$.
    - Se il valore è 1, accetta.

- Ogni assegnamento richiede $O(m)$ spazio, dove $m$ è il numero di variabili.
- Possiamo riutilizzare la stessa memoria per ogni assegnamento, quindi la memoria totale richiesta è $O(m)$.

**Corollario:**
$NP$ è inclusa in $PSPACE$.

**Dimostrazione:**
Sia $L$ in $NP$. Per il teorema di Cook-Levin, $L \leq_p SAT$. Abbiamo appena dimostrato che $SAT \in PSPACE$, quindi $L \in PSPACE$.

#### Un problema $PSPACE-completo$
**Definizione:**
Un linguaggio $L$ è $PSPACE-completo$ se è in $PSPACE$ e ogni altro linguaggio $L'$ in $PSPACE$ è poly riducibile a $L$(ovvero $L' \leq_p L$).

**Definizione:**
Un *quantificatore* è un simbolo che vincola una variabile ad un insieme di valori. (Es. $\forall, $ $\exists$)

**Definizione:**
Un *enunciato* è una formula che contiene solo variabili vincolate da quantificatori.

**Definizione:**
La verità di un enunciato non dipende dalla scelta di assegnamento dei valori di verità alle variabili. Se un enunciato è vero, allora è vero per ogni assegnamento.

**Definizione:**
$$TQBF = \{ \langle F \rangle | F \text{ è un enunciato booleano vero }\}$$

**Teorema:**
$TQBF$ è $PSPACE-completo$.

**Dimostrazione:**
Sarà simile alla dimostrazione che $SAT$ è $NP-completo$. Però non possiamo utilizzare la stessa tecnica perchè il tableau non è più polinomiale, quinid lo separeremo in quadranti e useremo i quantificatori per rappresentare diversi quadranti con la stessa sottoformula.

*Prima parte:*
Dimostriamo che $TQBF \in PSPACE$ con un algoritmo $ALG$ che lo decide su input $\langle F \rangle$, un enunciato booleano:
- Se $F$ non contiene quantificatori, allora contiene solo costanti(nessuna variabile). Valutiamola e accettiamo solo se è vera.
- Se $F = \exists x G$, chiama $ALG$ ricorsivamente su $G$, prima valutando $G$ con $x = 0$ e poi con $x = 1$. Se uno dei due è accentante(perchè appunto basta che esista un valore di x per cui è vera), accetta.
- Se $F = \forall x G$, chiama $ALG$ ricorsivamente su $G$, prima valutando $G$ con $x = 0$ e poi con $x = 1$. Se entrambi sono accentanti(deve risultare vera per tutti i valori di x), accetta.

$ALG$ richiede spazio $O(m)$, dove $m$ è il numero di variabili di $F$. Quindi $TQBF \in PSPACE$.

*Seconda parte:*
Dimostriamo che $TQBF$ è $PSPACE-completo$. Vogliamo dimostrare che $L \leq_p TQBF$ per ogni $L \in PSPACE$.
Chiamiamo M la TM che decide $L$ in spazio polinomiale($n^k$ per qualche $k$ costante). 
Basta costruire in tempo polinomiale una formula $F_w$ tale che:
- M accetta $w$ $\Leftrightarrow$ $F_w$ è un enunciato vero.

Per costruire $F_w$, costruiamo una formula più generale $F_{c, c', t}$ con la seguente proprietà:
- M può andaare da $c$ a $c'$ in al più $t$ passi $\Leftrightarrow$ $F_{c, c', t}$ è un enunciato vero.

Basterà poi deifnire $F_w$  come $F_{c_{init}, c_{acc}, t}$, dove $c_{init}$ è la configurazione iniziale di M su w, $c_{acc}$ è una qualsiasi configurazione accettante e $t = 2^{dn^k}$, per una $d$ costante tale che M non ha più di $t$ configurazioni possibili su input di lunghezza $n$.





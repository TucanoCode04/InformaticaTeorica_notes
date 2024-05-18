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


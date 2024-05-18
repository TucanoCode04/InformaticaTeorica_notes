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

$c$ e $c'$ sono insiemi di variabili del tipo $\{x_{i, j, s} | (i, j) \in n^k \times n^k, s \in Q \cup \Sigma \cup \{\#\}\}$. Ciascuno codifica una configurazione(riga).

*Esempio:*
- $c_{init} = \{x_{1, 1, \#}, x_{1, 2, w_1}, ..., x_{1, n + 1, w_n}, x_{1, n + 2, \sqcup}, x_{1, n^k, \#}\}$

Costruiamo ora $F_{c, c', t}$ per induzione su $t$:
- Se $t = 1$, due casi possibili:
    - la computazione ha 0 passi, quindi costruiamo un enunciato $F_1$ che dice che $c = c'$.
    - la computazione ha 1 passo, quindi costruiamo un enunciato $F_2$ che dice che $c'$ è ottenuto da $c$ in un passo(visto tramite finestre come in Cook-Levin).

$F_{c, c', 1} = F_1 \lor F_2$

- Se $t > 1$, costruiamo un enunciato:
    - $F_{c, c', t} = \exists m_1 \forall (c_3, c_4) \in \{(c, m_1), (m_1, c')\} F_{c_3, c_4, t/2}$, dove $\exists m_1$ abbrevia $\exists x_1, ..., x_l$ numero di variabili sufficiente a codificare una configurazione, mentre $\forall (c_3, c_4) \in \{(c, m_1), (m_1, c_1)\}$ vuol dire che $c_3$ e $c_4$ possono avere il valore delle variabili in $(c, m_1)$ o $(m_1, c')$.

Ogni passo induttivo aggiunge una parte di lunghezza $O(n^k)$ alla formula e vi sono $log(2^{dn^k}) = O(n^k)$ passi, quindi la formula finale ha lunghezza polinomiale in $n$.

#### Il teorema di Savitch
**Teorema:**
Per qualsiasi funzione $t : \mathbb{N} \rightarrow \mathbb{N}$, abbiamo:
$$NSPACE(t(n)) \subseteq SPACE(t^2(n))$$

**Corollario:**
$PSPACE = NPSPACE$

**Dimostrazione(Teorema di Savitch):**
Supponiamo che M sia una TM non deterministica che decide un linguaggio $L$ in spazio $t(n)$ rispetto ad un input di lunghezza $n$. Vogliamo costruire una TM M' deterministica che decide lo stesso linguaggio in spazio $t(n)^2$.

Definiamo $REACH$ che lavora in spazio $t(n)^2$:
- M può andare da $c$ a $c'$ in al più $t$ passi $\Leftrightarrow$ $REACH(c, c', t)$ dà outèut ACCETTA.

Definiremo poi M' come la TM che su input di lunghezza $n$ esegue $REACH(c_{init}, c_{acc}, 2^{dt(n)})$, dove $d$ è una costante tale che M ha al più $2^{dt(n)}$ configurazioni possibili su input di lunghezza $n$ e accetta se $REACH$ accetta.

$REACH$ è definita nel seguente modo, su input $\langle c, c', T \rangle$:
- se T = 1, verifica se $c = c'$ o se $c'$ è ottenibile da $c$ in un passo. Accetta se è vero.
- Se T > 1, per ogni configurazione $c_m$ di M che usa al più $t(n)$ spazio:
    - esegui $REACH(c, c_m, T/2)$ 
    - esegui $REACH(c_m, c', T/2)$
    - Accetta se entrambi accettano.
- Se nessuna delle due condizioni sopra è vera, RIGETTA.

La ricorsione divide il problema in due sottoproblemi di dimensione $T/2$, dunque per $T = 2^{dt(n)}$ abbiamo $O(log 2^{dt(n)}) = O(t(n))$ livelli di ricorsione. Ogni livello richiede spazio $O(t(n))$, cancellato alla fine del livello.
Quindi in totale $REACH$ richiede spazio $O(t(n)) \cdot O(t(n)) = O(t(n)^2)$.

Dal momento che $REACH(c_{init}, c_{acc}, 2^{dt(n)})$ lavora in spazio $t(n)^2$, abbiamo dimostrato che $L \in SPACE(t(n)^2)$.

### Gerarchie di complessità e Problemi intrattabili
L'intuizione è che una TM dovrebbe risolvere strettamente più problemi in un tempo $n^3$ che in un tempo $n^2$. Questi risultati vengono dai *teoremi di gerarchia*.
Tali risltati però hanno come conseguenza l'esistenza di problemi che non appartengono a nessuna classe di complessità, ovvero sono intrattabili: nonostante siano decidibili, non esiste un algoritmo che li risolva in tempi ragionevoli.

**Definizione:**
date due funzioni $f, g : \mathbb{N} \rightarrow \mathbb{N}$, scriviamo $f(n) = o(g(n))$ se per ogni $c > 0$ esiste un $m > 0$ tale che per ogni $n \geq m$ abbiamo $f(n) < c \cdot g(n)$.

*Esempio:*
$n^2 = o(n^3), n^2 \neq o(n^2)$

**Definizione(funzioni costruibili):**
Una funzione $f : \mathbb{N} \rightarrow \mathbb{N}$, dove $f(n) \geq O(log n)$, è *$SPACE$-costruibile* se possiamo calcolare in spazio $O(f(n))$ la funzione $1^n \rightarrow \langle f(n) \rangle$(codifica binaria di $f(n)$).

**Teorema(della gerarchia di spazio):**
Per ogni funzione $f : \mathbb{N} \rightarrow \mathbb{N}$ $SPACE$-costruibile, esiste un linguaggio $L$ decidibile in spazio $O(f(n))$ ma non in spazio $o(f(n))$.

**Dimostrazione:**
$L$ verrà definito da un algoritmo $ALG$ che usa spazio $O(f(n))$ ed è costruito in modo che $L$ è diverso da ogni linguaggio decidibile in spazio $o(f(n))$.

Definiamo $ALG$ come segue, su input $\langle w \rangle$ di lunghezza $n$:
- calcola $f(n)$ e segna $f(n)$ celle di memoria. Se i passi successivi richiedono più di $f(n)$ spazio, rigetta.
- se $w \neq code(M)10*$(si aggiunge una stringa affinchè la lunghezza dell'input di M diventi abbastanza grande oer cui valga il bound asintotico $o(f(n))$), rigetta.
- simula M su w. Se non ha concluso entro $2^{f(n)}$ passi, rigetta.
- se M accetta, rigetta. Se M rigetta, accetta.

$ALG$ lavora in spazio $O(f(n))$. Definiamo ora $L$ come: $L = \{ \langle w \rangle | ALG \text{ accetta } \langle w \rangle\}$.

$L$ è decidibile in spazio $O(f(n))$, dobbiamo dimostrare che non è decidibile in spazio $o(f(n))$

Per contraddizione, supponiamo che esista una TM N tale che $L$ è decidibile in spazio $g(n) = o(f(n))$.

$ALG$ simula N in spazio $d \cdot g(n)$, dove $d$ è una costante. Poichè $g(n) = o(f(n))$, esiste una costante $m$ tale che per ogni $n \geq m$ abbiamo $d \cdot g(n) < f(n)$.

Perciò $ALG$ simula N in spazio $f(n)$.
Non ci ho capito nulla.

*Conseguenze:*
**Corollario:**
Per ogni $k, j \in \mathbb{N}$, con $k < j$:
$$SPACE(n^k) \subsetneq SPACE(n^j)$$

**Corollario:**
$$SPACE(log n) \subsetneq SPACE(n)$$

**Definizione:**
$$EXPSPACE = \bigcup_{k} SPACE(2^{n^k})$$

**Corollario:**
$$PSPACE \subsetneq EXPSPACE$$

Quindi i problemi $EXPSPACE$-completi sono intrattabili(non hanno algoritmi polinomiali).

*Esempi:*
- se due espressioni regolari sono equivalenti
- words problems per gruppi

#### Gerarchia di tempo
Per ogni $f : \mathbb{N} \rightarrow \mathbb{N}$ $TIME$-costruibile, esiste un linguaggio $L$ decidibile in tempo $O(f(n))$ ma non in tempo $o(f(n)/log f(n))$.

**Dimostrazione:**
La dimostrazione è simile a quella della gerarchia di spazio, ma si ha un overhead logaritmico per la simulazione di una TM.

*Conseguenze:*
**Corollario:**
Per ogni $k, j \in \mathbb{N}$, con $k < j$:
$$TIME(n^k) \subsetneq TIME(n^j)$$

**Corollario:**
$$P \subsetneq EXPTIME$$

Quindi i problemi $EXPTIME$-completi sono intrattabili(non hanno algoritmi polinomiali).

*Esempi:*
- problema della fermata entro $k$ passi
- elaborare una strategia a scacchi, dama, ecc.

#### Considerazioni finali
Queste due dimostrazioni utilizzano il metodo della *diagonalizzazione*, che è un metodo molto potente per dimostrare l'esistenza di problemi intrattabili:
- la possibilità di rappresentare TM come stringhe binarie
- l'abilità di una TM di simulare un'altra TM di cui riceve codice come input senza aumentare troppo il tempo e lo spazio richiesto.

Esiste una variante che utilizza l'oracolo($O \subseteq \{0, 1\}^*$), ovvero una TM che può fare una domanda($w \in O$?) a un oracolo che risponde in tempo costante. 
I presupposti indicati per la diagonalizzazione valgono anche per l'oracolo, quindi valgono gli stessi risultati dimostrati.

**Teorema:**
Esistono oracoli $O$ e $O'$ tali che $P^O = NP^O$ e $P^{O'} \neq NP^{O'}$.

Questi risultati si chiamano *non relativizzanti*, ovvero non dipendono dall'oracolo. I teoremi di gerarchia sono relativizzanti, il teorema di Cook-Levin è non relativizzante.


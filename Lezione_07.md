### Mapping-reduction
Tecninca semplice per dimostrare l'indecidibilità/non riconoscibilità di un problema, basata sull'idea di ridurre il problema a un altro problema già noto come indecidibile/non riconoscibile.

$L'$ si riduce a $L$:
- la decibilità di $L'$ si riduce alla decibilità di $L$
- la riconoscibilità di $L'$ si riduce alla riconoscibilità di $L$

**Definizione:**
Siano $L, L'$ due linguaggi su alfabeto $\Sigma$, diciamo che $L'$ è mapping-riducibile a $L$(scritto $L' \leq L$), se esiste una TM che computa la funzione(totale) $f: \Sigma^* \rightarrow \Sigma^*$ tale che: 
- $x \in L' \Leftrightarrow f(x) \in L$

In pratica f converte un'istanza(di un problema di appartenenza) di $L'$ in un'istanza di $L$.

**Teorema:**
Se $L' \leq L$ e $L$ è decidibile, allora $L'$ è decidibile.

**Dimostrazione:**
- $L$ è decidibile, quindi esiste una TM $\mathcal{M}$ che decide $L$.
- Costruiamo una TM $\mathcal{M'}$ che decide $L'$:
    - $\mathcal{M'}$ prende in input $x$.
    - Calcola $f(x)$.
    - Simula $\mathcal{M}$ su $f(x)$.
    - $\mathcal{M'}$ accetta se $\mathcal{M}$ accetta, altrimenti rifiuta.

**Corollario:**
Se $L' \leq L$ e $L'$ è non decidibile, allora $L$ è non decidibile.
(Quindi per dimostrare che L è non decidibile basta mostrate che $HALT \leq L$)

**Corollario:**
Se $L$ è decidibile e $L'$ è non decidibile, allora $L' \nleq L$.

### Mapping-reduction in azione
#### Problema della fermata su nastro vuoto
**Teorema:**
$ETH$ è non decidibile.

*Linguaggio:*
$ETH = \{x \in \Sigma^* | x = code(\mathcal{M}) \text{ e } \mathcal{M} \text{ ferma su input } \epsilon\ (\text{stringa vuota})\}$

**Dimostrazione:**
- $HALT \leq ETH$: costruiamo una funzione $f : \langle y, x \rangle \in HALT \rightarrow f(\langle y, x \rangle) \in ETH$.
- Definiamo $f(\langle y, x \rangle)$ come segue:
    - se $y \neq code(\mathcal{M})$ per ogni TM $\mathcal{M}$, allora $f(\langle y, x \rangle) = y \notin ETH$.
    - se $y = code(\mathcal{M})$, allora $f(\langle y, x \rangle) = code(\mathcal{M_{MX}})$, dove $\mathcal{M_{MX}}$ è una macchina di Turing che:
        - $\mathcal{M_{MX}}$ entra in loop su ogni stringa non vuota.
        - su input $\epsilon$ scrive $x$ sul nastro e simula $\mathcal{M}$ su input $x$.
- $\langle y, x \rangle \in HALT$ $\Leftrightarrow$ $y = code(\mathcal{M})$ e $\mathcal{M}$ ferma su input $x$ $\Leftrightarrow$ $\mathcal{M_{MX}}$ ferma su input $\epsilon$ $\Leftrightarrow$ $f(\langle y, x \rangle) = code(\mathcal{M_{MX}}) \text{ e } f(\langle y, x \rangle) \in ETH$.

#### "Full Language" problem
**Teorema:**
$FL$ è non decidibile.

*Linguaggio:*
$FL = \{x \in \Sigma^* | x = code(\mathcal{M}) \text{ e } \mathcal{M} \text{ ferma su ogni input}\}$

**Dimostrazione:**
- $HALT \leq FL$: costruiamo una funzione $f : \langle y, x \rangle \in HALT \rightarrow f(\langle y, x \rangle) \in FL$.
- Definiamo $f(\langle y, x \rangle)$ come segue:
    - se $y \neq code(\mathcal{M})$ per ogni TM $\mathcal{M}$, allora $f(\langle y, x \rangle) = y \notin FL$.
    - se $y = code(\mathcal{M})$, allora $f(\langle y, x \rangle) = code(\mathcal{M_{MX}})$, dove $\mathcal{M_{MX}}$ è una macchina di Turing che:
        - $\mathcal{M_{MX}}$ cancella il suo input
        - scrive $x$ sul nastro e simula $\mathcal{M}$ su input $x$.
- $\langle y, x \rangle \in HALT$ $\Leftrightarrow$ $y = code(\mathcal{M})$ e $\mathcal{M}$ ferma su input $x$ $\Leftrightarrow$ $\mathcal{M_{MX}}$ ferma su ogni input $\Leftrightarrow$ $f(\langle y, x \rangle) = code(\mathcal{M_{MX}}) \text{ e } f(\langle y, x \rangle) \in FL$.

#### Problema di equivalenza
Il problema di equivalenza tra macchine di Turing.
**Teorema:**
$EQ$ è non decidibile.

*Linguaggio:*
$EQ = \{\langle y, x \rangle \in \Sigma^* \times \Sigma^* | x = code(\mathcal{M}) \text{ e } y = code(\mathcal{M'}) \text{ e } \mathcal{M} \text{ e } \mathcal{M'} \text{ computano la stessa funzione parziale}\}$

**Dimostrazione:**
- $FL \leq EQ$ (potevamo utillizzare ancora $HALT$): costruiamo una funzione $f : z \in FL \rightarrow f(z) \in EQ$.
- Definiamo $f(z)$ come segue:
    - se $z \neq code(\mathcal{M})$ per ogni TM $\mathcal{M}$, allora $f(z) = \langle z, z \rangle \notin EQ$.
    - se $z = code(\mathcal{M})$, allora $f(z) = \langle code(\mathcal{M_{1}}), code(\mathcal{M_{2}}) \rangle$, dove $\mathcal{M_{1}}$ e $\mathcal{M_{2}}$ sono macchine di Turing che:
        - $\mathcal{M_{1}}$ esegue $\mathcal{M}$ sul suo input e restituisce 1 se $\mathcal{M}$ si ferma, va in loop altrimenti.
        - $\mathcal{M_{2}}$ restituisce sempre 1.
- $z \in FL$ $\Leftrightarrow$ $z = code(\mathcal{M})$ e $\mathcal{M}$ ferma su ogni input $\Leftrightarrow$ $\mathcal{M_{1}}$ ferma su ogni input con output 1 $\Leftrightarrow$ $\mathcal{M_{1}}$ e $\mathcal{M_{2}}$ sono equivalenti $\Leftrightarrow$ $f(z) = \langle code(\mathcal{M_{1}}), code(\mathcal{M_{2}}) \rangle \text{ e } f(z) \in EQ$.

### Riduzione e Riconoscibilità
Ciò che è vero per Riduzione e Decidibilità è vero anche per Riduzione e Riconoscibilità.

**Teorema:**
Se $L' \leq L$ e $L$ è riconoscibile, allora $L'$ è riconoscibile.

**Corollario:**
Se $L' \leq L$ e $L'$ è non riconoscibile, allora $L$ è non riconoscibile.

**Corollario:**
Se $L$ è riconoscibile e $L'$ è non riconoscibile, allora $L' \nleq L$.

#### Problema di equivalenza
Abbiamo dimostrato che $EQ$ è non decidibile, ora dimostriamo che è non riconoscibile.

**Teorema:**
$EQ$ è non riconoscibile.

**Dimostrazione:**
- $HALT^- \leq EQ$ (sapendo che $HALT^-$ è non riconoscibile): costruiamo una funzione $f : \langle y, x \rangle \in HALT^- \rightarrow f(\langle y, x \rangle) \in EQ$, equivalente a $ \langle y, x \rangle \in HALT \rightarrow f(\langle y, x \rangle) \in EQ^-$.
- Definiamo $f(\langle y, x \rangle)$ come segue:
    - se $y \neq code(\mathcal{M})$ per ogni TM $\mathcal{M}$, allora prendiamo $\mathcal{M'}$ qualsiasi e consideriamo $f(\langle y, x \rangle) = \langle code(\mathcal{M'}), code(\mathcal{M'})$. Allora $f(\langle y, x \rangle) \in EQ$ e quindi $\langle y, x \rangle \notin EQ^-$.
    - se $y = code(\mathcal{M})$ e consideriamo $f(\langle y, x \rangle) = \langle code(\mathcal{M_1}), code(\mathcal{M_2}) \rangle$, dove $\mathcal{M_1}$ e $\mathcal{M_2}$ sono macchine di Turing che:
        - $\mathcal{M_1}$ esegue $\mathcal{M}$ sul suo input(x) e si femra se $\mathcal{M}$ si ferma, va in loop altrimenti.
        - $\mathcal{M_2}$ va in loop su ogni input.
- $\langle y, x \rangle \in HALT$ $\Leftrightarrow$ $y = code(\mathcal{M})$ e $\mathcal{M}$ ferma su input $x$ $\Leftrightarrow$ $\mathcal{M_1}$ accetta una stringa $\Leftrightarrow$ $\mathcal{M_1}$ e $\mathcal{M_2}$ non sono equivalenti $\Leftrightarrow$ $f(\langle y, x \rangle) = \langle code(\mathcal{M_1}), code(\mathcal{M_2}) \rangle \text{ e } f(\langle y, x \rangle) \in EQ^-$.

### Riduzione e Decidibilità
**Teorema:**
Se $L$ è un qualunque linguaggio non triviale($L \neq \emptyset, \Sigma^*$), allora $L' \leq L$ per ogni linguaggio $L'$ decidibile.

**Dimostrazione:**
Poichè $L$ è non triviale, esiste una stringa $x \in L$ e una stringa $y \notin L$.
- Definiamo $f : \Sigma^* \rightarrow \Sigma^*$ come segue:
    - $f(z) = x$ se $z \in L'$
    - $f(z) = y$ se $z \notin L'$
- Essendo $L'$ decidibile, possiamo implementare $f$ con una TM che simula la TM che decide $L'$ e restituisce $x$ o $y$ a seconda del risultato.
- Inoltre per definizione di $f$, $z \in L' \Leftrightarrow f(z) \in L$.

**Proprietà:**
- Riflessività: per ogni linguaggio $L$, $L \leq L$.
- Transitività: se $L' \leq L$ e $L \leq L''$, allora $L' \leq L''$.
- Non simmetria: se $L' \leq L$ e $L$ è decidibile, non è detto che $L \leq L'$.

Quindi la Riduzione non è una relazione di equivalenza.

**Teorema:**
$L_1 \leq L_2$ se e solo se $L_1^- \leq L_2^-$.

**Dimostrazione:**
- $\Rightarrow$: se $L_1 \leq L_2$, allora esiste una funzione $f$ tale che $x \in L_1 \Leftrightarrow f(x) \in L_2$. Quindi $x \in L_1^- \Leftrightarrow f(x) \in L_2^-$. Quindi $L_1^- \leq L_2^-$.
- $\Leftarrow$: se $L_1^- \leq L_2^-$, allora esiste una funzione $f$ tale che $x \in L_1^- \Leftrightarrow f(x) \in L_2^-$. Quindi $x \in L_1 \Leftrightarrow f(x) \in L_2$. Quindi $L_1 \leq L_2$.

**Corollario:**
$L_1^- \leq L_2$ se e solo se $L_1 \leq L_2^-$(Usato implicitamente nella prova con $L_1 = HALT$ e $L_2 = EQ$).

**Conclusioni:**
Sappiamo quindi che $EQ^-$ è non riconoscibile. Infatti $HALT \leq FL \leq EQ$, quindi $HALT^- \leq EQ^-$(la non riconoscibilità di $HALT^-$ implica la non riconoscibilità di $EQ^-$).

**Gerarchia:**
- $HALT$ è indecidibile, ma riconoscibile.
- $HALT^-$ è non riconoscibile, ma il cui complemento è riconoscibile.
- $EQ$ è non riconoscibile, e il cui complemento è non decidibile.

### Turing-riducibilità
*Oracolo:* Strumento esterno per un linguaggio capace di risponde, per ogni stringa $x$, se $x \in L$ o $x \notin L$.

**Definizione:**
Un linguaggio $L'$ è Turing-riducibile a un linguaggio $L$ se esiste un oracolo per $L$ possiamo decidere $L'$.

**Confronto con la mapping-reduction:**
La mapping-reduction implica la Turing-reduction, ma non viceversa.

**Esempio:**
- $HALT^- \nleq HALT$($HALT^-$ non è mapping-riducibile a $HALT$).
- $HALT^-$ è Turing-riducibile a $HALT$, infatti se abbiamo un oracolo per la domanda "$\langle y, x \rangle \in HALT$?" può essere usato per decidere $\langle y, x \rangle \in HALT^-$.


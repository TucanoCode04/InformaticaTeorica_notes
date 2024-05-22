### (In)Calcolabilità
**Conseguenze della tesi di Church-Turing:**
- se una problema è calcolabile attraverso una procedura algoritmica, allora è calcolabile da una macchina di Turing.
- se un problema non è calcolabile da una macchina di Turing, allora non è calcolabile da nessuna procedura algoritmica(questo è quello che vedremo ora).

**Gradi di (in)calcolabilità:**
- Decidibile $\Rightarrow$ Calcolabile(un algoritmo risponde sempre si o no)
- Non decidibile, ma riconoscibile $\Rightarrow$ Semidecidibile(nessun algoritmo sa calcolare tutti i no)(Non calcolabile)
- Non riconoscibile $\Rightarrow$ Non calcolabile(qualsiasi algoritmo fallirà nel dare una risposta)

### Problemi non calcolabili
Dimostriamo l'esistenza di un problema riconoscibile ma non decidibile.

Supponiamo l'esistenza di una cofidica $code(-)$ che codifica una TM su alfabeto $\Sigma$ in stringhe $x \in \Sigma^*$.

#### Problema della fermata:
*Linguaggio:* 
$HALT = \{\langle y, x \rangle \in \Sigma^* \times \Sigma^* | y = code(\mathcal{M}) \text{ e } \mathcal{M} \text{ si ferma su input } x\}$

**Teorema:**
Il problema della fermata è riconoscibile ma non decidibile.

**Dimostrazione:**
- $HALT$ è riconoscibile: costruiamo una macchina di Turing $\mathcal{M}$ che riconosce $HALT$.
    - $\mathcal{M'}$ prende in input $y = (code(\mathcal{M}), x)$.
    - $\mathcal{M'}$ simula $\mathcal{M}$ su input $x$.
    - $\mathcal{M'}$ si ferma se $\mathcal{M}$ si ferma su input $x$.
- $HALT$ non è decidibile: supponiamo per assurdo che esista una macchina di Turing $\mathcal{M_H}$ che decide $HALT$.
    - $\mathcal{M_H}$ prende in input $y = code(\mathcal{M}), x$.
    - $\mathcal{M_H}$ accetta se $\mathcal{M}$ si ferma su input $x$.
    - $\mathcal{M_H}$ rifiuta se $\mathcal{M}$ non si ferma su input $x$.
    - Costruiamo una nuova macchina di Turing $\mathcal{M'}$ che prende in input $z \in \Sigma^*$ e fa:
        - $\mathcal{M'}$ simula $\mathcal{M_H}$ su input $\langle z, z \rangle$.
        - $\mathcal{M'}$ accetta se $\mathcal{M_H}$ rifiuta.
        - $\mathcal{M'}$ entra in un ciclo se $\mathcal{M_H}$ accetta.
    - Proviamo $\mathcal{M'}$ su input $code(\mathcal{M'})$.
        - $\mathcal{M'}$ accetta se $\mathcal{M_H}$ rifiuta su input $\langle code(\mathcal{M'}), code(\mathcal{M'}) \rangle$.
        - $\mathcal{M'}$ entra in un ciclo se $\mathcal{M_H}$ accetta.
    - Contraddizione: $\mathcal{M_H}$ accetta $\langle code(\mathcal{M'}), code(\mathcal{M'}) \rangle$ $\Rightarrow$ $\mathcal{M'}$ entra in un ciclo su input $code(\mathcal{M'})$ $\Rightarrow$ $\langle code(\mathcal{M'}), code(\mathcal{M'}) \rangle \notin HALT$ $\Rightarrow$ $\mathcal{M_H}$ rifiuta $\langle code(\mathcal{M'}), code(\mathcal{M'}) \rangle$.

    ($\mathcal{M_H}$ accetta se e solo se $\mathcal{M'}$ si ferma su input $x$, ma se $\mathcal{M_H}$ accetta allora $\mathcal{M'}$ entra in un ciclo, quindi $\mathcal{M_H}$ rifiuta, contraddizione.)
    - Proviamo al contrario: $\mathcal{M_H}$ rifiuta $\langle code(\mathcal{M'}), code(\mathcal{M'}) \rangle$ $\Rightarrow$ $\mathcal{M'}$ ferma su $code(\mathcal{M'})$ $\Rightarrow$ $\langle code(\mathcal{M'}), code(\mathcal{M'}) \rangle \in HALT$ $\Rightarrow$ $\mathcal{M_H}$ accetta $\langle code(\mathcal{M'}), code(\mathcal{M'}) \rangle$.
    
    ($\mathcal{M_H}$ rifiuta se e solo se $\mathcal{M'}$ non si ferma su input $x$, ma se $\mathcal{M_H}$ rifiuta allora $\mathcal{M'}$ ferma, quindi $\mathcal{M_H}$ accetta, contraddizione.)
- L'unica assunzione utilizzata per costruire $\mathcal{M'}$ è che esista una macchina di Turing $\mathcal{M_H}$ che decide $HALT$. $\mathcal{M_H}$ non può esistere, quindi $HALT$ non è decidibile.


### Problemi non riconoscibili
**Teorema:**
Il complemento $HALT^-$ del problema della fermata non è riconoscibile da nessuna macchina di Turing.

**Dimostrazione:**
C'è una dimostrazione diretta, ma decidiamo di dimostrare il teorema attraverso il complemento di un linguaggio riconoscibile.

*Linguaggio:* 
$HALT^- = \{\langle y, x \rangle \in \Sigma^* \times \Sigma^* | y \neq code(\mathcal{M}) \text{ per qualsiasi TM oppure } y = code(\mathcal{M}) \text{ e } \mathcal{M} \text{ non si ferma su input } x\}$

**Teorema:**
Se $HALT^-$ fosse riconoscibile, allora $HALT$ sarebbe decidibile.
Implica che se $HALT$ non è decidibile, allora $HALT^-$ non è riconoscibile.

**Dimostrazione:**
- Abbiamo già visto che $HALT$ è riconoscibile, diciamo da una macchina di Turing $\mathcal{M_{HR}}$.
- Supponiamo per assurdo che anche $HALT^-$ sia riconoscibile, diciamo da una macchina di Turing $\mathcal{M_{H^-}}$.
- Costruiamo una nuova macchina di Turing $\mathcal{M_{H}}$ che decide $HALT$:
    - su input $\langle y, x \rangle$, simula $\mathcal{M_{HR}}$ e $\mathcal{M_{H^-}}$ in parallelo. 
    - se $\mathcal{M_{HR}}$ ferma, $\mathcal{M_{H}}$ accetta.
    - se $\mathcal{M_{H^-}}$ ferma, $\mathcal{M_{H}}$ rifiuta.
- $\langle y, x \rangle \in HALT$ $\Rightarrow$ $\mathcal{M_{HR}}$ ferma $\Rightarrow$ $\mathcal{M_{H}}$ ferma e accetta.
- $\langle y, x \rangle \notin HALT$ $\Rightarrow$ $\langle y, x \rangle \in HALT^-$ $\Rightarrow$ $\mathcal{M_{H^-}}$ ferma $\Rightarrow$ $\mathcal{M_{H}}$ ferma e rifiuta.
- Perciò $\mathcal{M_{H}}$ decide $HALT$.
- Contraddizione: $HALT$ non è decidibile, quindi $HALT^-$ non è riconoscibile.

### Complemento di un linguaggio riconoscibile
La dimostrazione del teorema precedente non sfrutta la definizione dei $HALT$ e $HALT^-$, ma la loro relazione di complemento.

**Teorema:**
Se $L$ e $L^-$ sono entrambi riconoscibili, allora $L$ è decidibile.

**Dimostrazione:**
La stessa data per $L=HALT$.

**Corollario:**
I linguaggi riconoscibili non sono chiusi rispetto al complemento.

**Dimostrazione:**
$HALT$ è riconoscibile, ma $HALT^-$ non è riconoscibile.
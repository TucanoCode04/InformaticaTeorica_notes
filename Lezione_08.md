### Teorema di Rice
Abbiamo visto che non possiamo decidere se ua TM:
- ferma su un input
- ferma su input vuoto
- è equivalente ad un'altra TM

Sappiamo che possiamo decidere se una TM:
- ferma sempre in un certo numero di passi
- ma meno di un certo numero di stati

**Proprietà di linguaggio:**
Una proprietà di linguaggio P è una funzione da un insieme di TM a $\{0, 1\}$(vero o falso), tale che $L_{\mathcal{M}} = L_{\mathcal{M}'} \Rightarrow P(\mathcal{M}) = P(\mathcal{M}')$.
Questo significa che P dipende solo dal linguaggio e non dalla TM.

Questa proprietà è "non triviale" se esiste almeno una TM $\mathcal{M}$ tale che $P(\mathcal{M}) = 1$ e almeno una TM $\mathcal{M}'$ tale che $P(\mathcal{M}') = 0$.
Ossia, esistono TM che soddisfano e non soddisfano la proprietà.

L'insieme delle TM che soddisfano P sarà: $\{ y \in \Sigma^* | y = code(\mathcal{M}) \text{ e } P(\mathcal{M}) = 1 \}$.

*Esempio:*
- $\{ y | y = code(\mathcal{M}) \text{ e } L_{\mathcal{M}} = \emptyset \}$: insieme delle TM che riconoscono un linguaggio vuoto, è non triviale.
- $\{ y | y = code(\mathcal{M}) \text{ e } \mathcal{M} \text{ riconosce qualche linguaggio } \}$: è triviale.

#### Teorema di Rice
**Teorema:**
Se P è una proprietà di linguaggio non triviale, allora il problema "$\mathcal{M}$ ha proprietà P" è indecidibile.

**Dimostrazione:**
Per contraddizione. DImostriamo che se "$\mathcal{M}$ ha proprietà P" fosse decidibile, allora il problema della fermata sarebbe decidibile.

- Assumiamo P($\mathcal{M_\emptyset}$) = 0, dove $\mathcal{M_\emptyset}$ è la TM che riconosce il linguaggio vuoto.
- Essendo P non triviale, esiste almeno una TM $\mathcal{M_{\mathcal{P}}}$ tale che P($\mathcal{M_{\mathcal{P}}}$) = 1.
- Fissiamo $\mathcal{M}$ e $x$ come parametri, costruiamo la seguente TM $\mathcal{M_{\mathcal{M}, x}}$:
    - prende $z$ in input
    - simula $\mathcal{M}$ su $x$
    - se $\mathcal{M}$ ferma, simula $\mathcal{M_{\mathcal{P}}}$ su $z$, altrimenti entra in un loop
    - se $\mathcal{M_{\mathcal{P}}}$ ferma, accetta, altrimenti entra in un loop
- $\mathcal{M}$ ferma su $x$ $\Rightarrow$ $\mathcal{M_{\mathcal{M}, x}}$ ferma su $z$ ogni volta che $\mathcal{M_{\mathcal{P}}}$ ferma su $z$ $\Rightarrow$ $L_{\mathcal{P}} = L_{\mathcal{M_{\mathcal{M}, x}}}$ $\Rightarrow$ P($\mathcal{M_{\mathcal{M}, x}}$) = P($\mathcal{M_{\mathcal{P}}}$) = 1, cioè $\mathcal{M_{\mathcal{M}, x}}$ ha la proprietà P.
- $\mathcal{M}$ non ferma su $x$ $\Rightarrow$ $\mathcal{M_{\mathcal{M}, x}}$ non ferma mai su $z$ $\Rightarrow$ $L_{\mathcal{M_{\mathcal{M}, x}}} = \emptyset$ $\Rightarrow$ P($\mathcal{M_{\mathcal{M}, x}}$) = P($\mathcal{M_{\emptyset}}$) = 0, cioè $\mathcal{M_{\mathcal{M}, x}}$ non ha la proprietà P.

(In pratica si costruisce una TM $\mathcal{M_{\mathcal{M}, x}}$ che ferma su input $z$ se $\mathcal{M_{\mathcal{P}}}$ ferma su $z$, quindi entrambe le TM hanno la stessa proprietà P, tutto questo ovviamente se $\mathcal{M}$ ferma su $x$)
(Il problema è che stiamo decidendo in questo modo il problema della fermata, che sappiamo essere indecidibile, quindi c'è una contraddizione)

Conclusione: se potessimo decidere se $\mathcal{M}$ ha la proprietà P, potremmo decidere il problema della fermata. Allora $\{ y | y = code(\mathcal{M}) \text{ e } P(\mathcal{M}) = 1 \}$ è indecidibile.

Se assumiamo invece che $P(\mathcal{M_{\emptyset}} = 1)$. Si può utilizzare lo stesso metodo ma per $\lnot P$("$\mathcal{M}$ non ha la proprietà P").

- dato che P è non triviale, anche $\lnot P$ è non triviale
- dato che $P(\mathcal{M_{\emptyset}} = 1)$, allora $\lnot P(\mathcal{M_{\emptyset}} = 0)$

Conclusione: $\{ y | y = code(\mathcal{M}) \text{ e } \lnot P(\mathcal{M}) = 1 \}$ è indecidibile, quindi anche $\{ y | y = code(\mathcal{M}) \text{ e } P(\mathcal{M}) = 1\}$ è indecidibile.

**Tipi di proprietà:**
- proprietà di linguaggio: queste proprietà si riferiscono al linguaggio che una TM accetta. Quelle non triviali sono indecidibili.
    - Esempi:
        - il linguaggio accettao è...
        - problema della fermata(se una TM si ferma su un input)
        - problema dell'equivalenza(se due TM accettano lo stesso linguaggio)
        - problema dell'universalità(se una TM accetta tutti i possibili input)
- proprietà strutturali: Quest proprietà si riferiscono alla struttura della TM stessa. Sono decibili poichè verificate staticamente sulla codifica della descrizione di TM.
    - Esempi:
        - numero di stati(determinare il numero di stati di una TM)
        - numero di simboli(determinare il numero di simboli di una TM)
        - numero di transizioni(determinare il numero di transizioni di una TM)
- proprietà algoritmiche: Quest proprietà si riferiscono al comportamento operativo di una TM su un certo input. La classificazione non è ovvia.
    - Esempi:
        - movimento(una TM si muove a sinistra su un input)
        - loop infiniti(una TM entra in un loop infinito su un input)

(Da capire meglio cosa intendono le proprietà)

### Cardinalità dei problemi irrisolvibili
Dimostriamo che la maggior parte dei linguaggi non sono riconoscibili, e quindi non decidibili.

**Definizione:**
Un insieme $S$ è infinitamente numerabile se c'è una funzione totale biettiva $f: \mathbb{N} \rightarrow S$

**Lemma**
Se $S_1$ e $S_2$ sono infinitamente numerabili, $S_1 \cup S_2$ è infinito numerabile.

*Esempi:*
- insieme delle TM è infinito numerabile
- insieme dei linguaggi riconosciuti da una TM è infinito numerabile
- inisisme delle funzioni $\mathbb{N} \rightarrow \mathbb{N}$ è infinito numerabile

#### Insieme non numerabili
Cantor proponr una tenica di *diagonalzzaizone* per mostrare che i numeri reali($\mathbb{R}$) non sono un infinito numerabile, è un infinito più grande di quello dei numeri naturali($\mathbb{N}$).

**L'insieme dei linguaggi è non numerabile**

**Teorema:**
L'insieme $S_{\Sigma}$ di tutti i linguaggi su un alfabeto $\Sigma$ è non numerabile.

**Dimostrazione:**
Per contraddizione. 
- Supponiamo che $S_{\Sigma}$ sia numerabile, allora possiamo elencare i linguaggi come $L_1, L_2, L_3, ...$ in modo che $L_i \in S_{\Sigma}$ appare nella riga $i$ della tabella.
- Guardiamo la diagonale della tabella e costruiamo un linguaggio $L$ che non è nella tabella.
Contraddizione: $L$ non appare nella tabella, ma dovrebbe apparire.
Conclusione: $S_{\Sigma}$ è non numerabile.

**Conclusioni:**
- l'insieme dei linguaggi riconoscibili da una TM è infinito numerabile
- l'insieme dei linguaggi è non numerabile

Quindi esistono linguaggi non riconoscibili da nessuna TM(abbiamo visto $HALT^-, EQ, EQ^-$).

#### Numero di insiemi non riconoscibili
**Teorema:**
Se $S$ è un insieme infinito non numerabile e $S' \subseteq S$ infinito numerabile, allora $S \backslash S'$ è non numerabile.

**Dimostrazione:**
Assumiamo per contraddizione che $S \backslash S'$ sia numerabile. Allora, poichè i linguaggi infiniti numerabili sono chiusi per unione, $(S \backslash S') \cup S' = S$ è numerabile.
Contraddizione: $S$ è non numerabile.

**Corollario:**
L'insieme dei linguaggi non riconoscibili è non numerabile. Allora ci sono più linguaggi non riconoscibili che riconoscibili.

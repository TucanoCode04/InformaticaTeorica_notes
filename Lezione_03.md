### Tesi di Church-Turing
Se la soluzione di un problema può essere calcolata algorithmicamente, allora può essere calcolata da una macchina di Turing.
Non parla di efficienza o semplcitità, ma solo di calcolabilità.
Tuttavia definiscono:
- in modo rigoroso cos'è un algoritmo
- possono simulare qualsiasi altro calcolatore, quindi pososno essere utilizzati per dimostrare enunciati matematici sulle possibilità e i limiti di ciò che è calcolabile

### Variazioni della macchina di Turing
La definizione della macchina di Turing è robusta(rimane invariata rispetto a variazioni).
Sono state proposte variazioni della macchina di Turing, tutte equivalenti tra loro e alla macchina di Turing standard.
#### Macchina di Turing con nastri addizionali:**
L'input viene letto dal primo nastro, gli altri nastir inizialmente vuoti.
Ad ogni passo di computazione, ogni testina è nello stesso stato, ma può essere in posizioni diverse e leggere simboli o compiere azioni diverse.
Se si raggiunge uno stato finale, l'output si legge dal primo nastro.
*Formalmente:* Una macchina di Turing con k nastri è una tupla $(\Sigma, Q, q_0, H, \delta)$ dove:
- $\delta: Q \backslash H \times \Sigma^k \rightarrow Q \times ( \Sigma \times \{\rightarrow, \leftarrow, -\} )^k$ è la funzione di transizione
*Esempio:*
Una macchina di Turing con 2 nastri che verifica se una stringa è palindroma.
- il primo nastro contiene la stringa
- il secondo nastro contiene una copia della stringa
- la mcchina legge su un nastro da sinistra a destra e sull'altro da destra a sinistra, verificando se i simboli corrispondono.

**Teorema:** 
Macchine di Turing con k nastri sono equivalenti alle macchine di Turing standard.

**Dimostrazione:**
La prima direzione è ovvia, una macchina di Turing con k nastri può simulare una macchina di Turing standard, scrivendo su un nastro i simboli che legge da tutti i nastri.
Per la seconda direzione, sia M una macchina di Turing con nastri addizionali, costruiamo M' con un solo nastro equivalente a M, cioè per ogni input x:
- M non termina su x $\Leftrightarrow$ M' non termina su x
- M termina su x con output y $\Leftrightarrow$ M' termina su x con output y

Se M è basata su un alfabeto $\Sigma$, M' sarà basata su un alfabeto $\Sigma \uplus \{ \bar{a} | a \in \Sigma \} \uplus \{ \# \}$, dove $\bar{a}$ rappresenta il simbolo a su un altro nastro e $\#$ è un simbolo di separazione.
M' simula M, scrivendo su un nastro i simboli che legge da ogni nastro separati da $\#$.
- Serve una lettura completa per raccogliere le informazioni di tutti i nastri(concatenati in un unico nastro).
- Poi un secondo passaggio per aggiornare ogni nastro secondo la funzione di transizione(nel caso un nastro avesse bisogno di spazio aggiuntivo si spostano tutti i simboli a destra).
- L'ultimo passo avviene cancellando tutto a parte il primo nastro e leggendo l'output.

#### Macchina di Turing non deterministiche
Una macchina di Turing non deterministica è una macchina di Turing in cui la funzione di transizione è una relazione non deterministica.
$ \delta: Q \backslash H \times \Sigma \times Q \times \Sigma \times \{\rightarrow, \leftarrow, -\} $ è non deterministica(non c'è la freccia).
Tutte le configurazioni attraversate nella ocmputazione non formano una sequenza ma un albero. Un input è accettato se esiste un ramo accettante(che termina in uno stato finale).
*Esempio:*
Una macchina di Turing non deterministica che verifica se un numero è non primo.
- il nastro 1 è di sola lettura e contiene il numero n.
- si decide in modo non deterministico un divisore 1 < m < n.
- se n mod m = 0, accetta, altrimenti rifiuta.

n è accettato se e solo se esiste un divisore m tra 2 e n-1 che divide n.

**Teorema:**
Le macchine di Turing non deterministiche sono equivalenti alle macchine di Turing standard.

**Dimostrazione:**
Data una macchina di Turing non deterministica M, costruiamo una macchina di Turing standard M' equivalente a M.
M' su un input x esplora l'albero delle computazioni di M su x e accetta se esiste un ramo accettante.
L'esplorazione dell'albero è breadth-first, perchè così si evita di esplorare rami infiniti(cicli per esempio).

Vengono utilizzati 3 nastri:
- il primo contiene l'input(solo lettura)
- il nastro di simulazione contiene la configurazione corrente di M'(esplora un ramo alla volta)
- il nastro di indice contiene l'indice del ramo corrente.

### Proprietà di chiusura dei linguaggi
I linguaggi sono insiemi di stringhe, quindi possiamo definire operazioni tra linguaggi.
- complemento $L^-$: il linguaggio complementare di L su un alfabeto $\Sigma$ è $\Sigma^* \backslash L$, cioè l'insieme di tutte le stringhe su $\Sigma$ che non sono in L.
- concatenazione: $L_1 \cdot L_2 = \{ xy | x \in L_1, y \in L_2 \}$

Dimostrare che un linguaggio è chiuso rispetto all'unione vuol dire dimostrare che:
- $L_1 \in X$ e $L_2 \in X \Rightarrow L_1 \cup L_2 \in X$

Dimostrare che un linguaggio è chiuso rispetto al complemento vuol dire dimostrare che:
- $L \in X \Rightarrow L^- \in X$

E così via per le altre operazioni.

**Teorema:**
I linguaggi *decidibili* sono chiusi rispetto a:
- complemento: per la dimostrazione basterebbe costruire una macchina di Turing che accetta se e solo se un'altra macchina di Turing non accetta, scambiando Y con N e viceversa.
- unione: sia $M_1$ una macchina di Turing che decide $L_1$ e $M_2$ una macchina di Turing che decide $L_2$, costruiamo una macchina di Turing che decide $L_1 \cup L_2$ con due nastri.
    - copiamo l'input su entrambi i nastri
    - simuliamo $M_1$ su un nastro, se accetta accettiamo, altrimenti simuliamo $M_2$ sull'altro nastro
    - se $M_2$ accetta, accettiamo, altrimenti rifiutiamo.
- intersezione: simile all'unione, ma accettiamo solo se entrambe le macchine accettano.
- concatenazione: sia $M_1$ una macchina di Turing che decide $L_1$ e $M_2$ una macchina di Turing che decide $L_2$, costruiamo una macchina di Turing non deterministica che decide $L_1 \cdot L_2$ con due nastri(il non determinismo significa che se esiste almeno una decomposizione in due stringhe tali che la prima è in $L_1$ e la seconda in $L_2$, accettiamo).
    - scegliamo in maniera non deterministica y e z tali che x = yz. Scriviamo y su un nastro e z sull'altro.
    - simuliamo $M_1$ su y, se rigetta rifiutiamo, altrimenti simuliamo $M_2$ su z.
    - se $M_2$ accetta, accettiamo, altrimenti rifiutiamo.

**Teorema:**
I linguaggi *riconoscibili* sono chiusi rispetto a:
- concatenazione: simile al caso dei linguaggi decidibili, ma se accettiamo entrambe le macchine ci fermiamo e accettiamo. Altrimenti finiamo in un loop infinito.
- intersezione: simile al caso dei linguaggi decidibili, ma se entrambe le macchine accettano ci fermiamo e accettiamo. Altrimenti finiamo in un loop infinito.
- unione: simile al caso dei linguaggi decidibili, ma le simulazioni sulle due macchine sono in parallelo e non in sequenza, altrimenti finiamo in un loop infinito se una delle due macchine non accetta.

I linguaggi *riconoscibili* non sono chiusi rispetto al complemento.

**Tecniche:**
Si possono utilizzare le tecniche di chiusura per dimostrare che un linguaggio è decidibile o riconoscibile.

*Esempio:*
Dimostrare che il linguaggio $L = \{ x \in \{0,1\}^* | x \text{ ha lunghezza dispari e più 1 che 0} \}$ è decidibile.
Basta dimostrare che:
- $L_1 = \{ x \in \{0,1\}^* | x \text{ ha lunghezza dispari} \}$ è decidibile
- $L_2 = \{ x \in \{0,1\}^* | x \text{ ha più 1 che 0} \}$ è decidibile

Perchè $L = L_1 \cap L_2$ e i linguaggi decidibili sono chiusi rispetto all'intersezione.


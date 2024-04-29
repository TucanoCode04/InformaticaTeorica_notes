#### Macchine a registri
Le macchine di Turing possono accedere alle informazioni solo in maniera sequenziale, adesso analizzeremo un modello di macchina che può accedere a più informazioni in parallelo. 
Mostreremo l'equivalenza tra le macchine di Turing e le macchine a registri(URM), dimostrando che la sequenzialità non è una limitazione intrinseca delle macchine di Turing.

**Macchine a registri**
Una macchina ha infiniti registri($R_1, R_2, R_3, ...$) che possono contenere numeri naturali($r_1, r_2, r_3, ...$).
Le URM calcolano funzioni $\mathbb{N}^k \rightarrow \mathbb{N}$, con $k$ numero di argomenti della funzione.
L'input $x \in \mathbb{N}^k$ è caricato nei primi $k$ registri, i restanti registri sono inizializzati a 0.
L'output è il contenuto del primo registro, se la computazione termina.

Una macchina a registri esegue un programma P, suddiviso in istruzioni $I_1, I_2, I_3, ...$, suddivise in 4 tipi:
1. Zero: $Z(i)$, azzeramento del registro $R_i$.
2. Successor: $S(i)$, incremento di uno il registro $R_i$.
3. Move: $M(i, j)$, copia il contenuto del registro $R_i$ nel registro $R_j$.
4. Jump: $J(i, j, k)$, salto alla istruzione $I_k$ se $r_i = r_j$, altrimenti non fa nulla.

Una computazione inizia con il caricamento dell'input nei primi $k$ registri, e l'esecuzione del programma P.
A meno di salti, le istruzioni vengono eseguite in sequenza, e la computazione termina quando non ci sono più istruzioni da eseguire.

*Esempio Addizione:*
- Input: $3, 2$
- Programma: 
    - $I_1: J(2, 3, 6)$
    - $I_2: S(1)$
    - $I_3: S(3)$
    - $I_4: J(2, 3, 6)$
    - $I_5: J(1, 1, 2)$

**Definizione:**
Una funzione parziale $f: \mathbb{N}^k \rightarrow \mathbb{N}$ è una funzione il cui valore non è definito per tutti gli input(in certi casi la computazione non termina).
Sia URM che TM calcolano funzioni parziali.

**Teorema:**
Una funzione parziale $f: \mathbb{N}^k \rightarrow \mathbb{N}$ è calcolabile da una URM se e solo se è calcolabile da una TM.

**Dimostrazione:**
*TM $\Rightarrow$ URM*
Costruiamo una TM che simula una URM, con 6 nastri:
- 1: Contatire del programma: mantiene l'indice dell'istruzione corrente.
- 2: Codice del programma: contiene il codice del programma.
- 3: Registri: contiene i registri scritti in notazione unaria e separati da $\sqcup$.
- 4/5/6: Fogli di brutta, cache per i registri.

Ogni tipo di istruzione modifica il valore di qualche registro(eccetto Jump). La modifica del valore di un registro $R_k$ è fatta in 3 passi:
1. Scrivi il nuovo valore di $R_k$ nel nastro 4.
2. Nel nastro 5, scrivi i valori $r_1, r_2, ..., r_{k-1}$. Nel nastro 6, scrivi i valori $r_{k+1}, r_{k+2}, ...$.
3. Nel nastro 3 scrivi i valori di $r_1, r_2, ..., r_{k-1}$, il nuovo valore di $R_k$, e i valori di $r_{k+1}, r_{k+2}, ...$.

*URM $\Rightarrow$ TM*
Costruiamo una URM che simula una TM: tale costruzione richiede una codifica che traduca la definizione ed il comportamento di una TM $\mathcal{M} = \langle \Sigma, Q, q_0, H, \delta \rangle$ in numeri naturali.

Introduciamo un registro TAPE che rappresenta il contenuto corrente del nastro. 
Assumiamao che $\Sigma = \{0, 1, \sqcup\}$. Introduciamo, qundi, la cofidica $\langle code(\sqcup), code(0), code(1) \rangle = \langle 0, 1, 2 \rangle$.
Da qui possiamo esprimere il contenuto del nastro come un numero naturale in base 3( $801 = 1 \cdot 3^0 + 0 \cdot 3^1 + 1 \cdot 3^2 + 0 \cdot 3^3 + 2 \cdot 3^4$).

- Introduciamo registri che codificano la funzione di transizione $\delta$: $Q_{IN}$, $\delta_{IN}$, $Q_{OUT}$, $\delta_{OUT}$.
- Introduciamo registri che codificano le configurazioni della TM: TAPE, $HEAD_{POS}$, $HEAD_{SYM}$, $HEAD_{STATE}$.
- Definiamo nuovi tipi di istruzioni utilizzando i 4 base tipi di istruzioni: Read, Write, Move-Left, Move-Right.(Per non confondersi anche se sono 4 anche queste, questo sono quelle nuove).
- Scriviamo un programma di URM che simula una TM.

#### Linguaggio di programmazione WHILE
Abbiamo dimostrato che una TM simula qualunque cosa a basso livello, adesso cerchiamo di dimostrare che anche un linguaggio ad altro livello non ha più potere espressivo. Mostriamo che un linguaggio di programmazione molto semplice, WHILE, è equivalente alle TM, e viceversa.

*Sintassi informale di WHILE:*
- $x := e$: assegnamento
- $while x \neq 0 do PROGRAM$: ciclo
- $PROGRAM_1; PROGRAM_2$: sequenzialità
- tutto il resto può essere definito in termini di queste 3 istruzioni.

*Semantica informale di WHILE:*
Un programma WHILE computa una funzione parziale $\mathbb{N}^k \rightarrow \mathbb{N}^k$.

**Teorema:**
Una funzione parziale è computabile da un programma WHILE se e solo se è calcolabile da una TM.

**Dimostrazione:**
Dimostriamo per induzione su un programma WHILE basato su variabili $x_1, x_2, ...$.

*Caso base:*
Se il programma è un'assegnazione di 0 ad una variabile, la TM corrispondente rimpiazza il valore della variabile con 0(le variabili sono scritte in notazione unaria una di seuguito all'altra sul nastro).
Programma vuoto e assegnamento di una variabile ad un'altra sono casi simili.

*Caso induttivo:*
- sequenzialità: avendo un programma $P_1; P_2$, avremo $\mathcal{M}_1$ e $\mathcal{M}_2$ TM corrispondenti. Concateniamo le TM in modo che $\mathcal{M}_1$ scriva l'output su un nastro e $\mathcal{M}_2$ legga l'input da un nastro.
- ciclo: avendo un programma $while x_i \neq x_j do P$, avremo $\mathcal{M}$ TM corrispondente. Possiamo costruire una TM $\mathcal{M}_{test}$ che rigetta l'input se $x_i \neq x_j$, altrimenti accetta. 
L'input verrà scritto su $\mathcal{M}_{test}$, se rigetta passiamo a $\mathcal{M}$ che torna all'inizio del ciclo, altrimenti termina.




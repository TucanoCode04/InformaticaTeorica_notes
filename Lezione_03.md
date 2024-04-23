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
- $\delta: Q \backslash H \times \Sigma^k \rightarrow Q \times \( \Sigma \times \{\rightarrow, \leftarrow, -\} \)^k$ è la funzione di transizione
*Esempio:*
Una macchina di Turing con 2 nastri che verifica se una stringa è palindroma.
- il primo nastro contiene la stringa
- il secondo nastro contiene una copia della stringa
- la mcchina legge su un nastro da sinistra a destra e sull'altro da destra a sinistra, verificando se i simboli corrispondono.

**Teorema:** 
Macchine di Turing con k nastri sono equivalenti alle macchine di Turing standard.

**Dimostrazione:**
Slide 16
#### Macchina di Turing non deterministiche
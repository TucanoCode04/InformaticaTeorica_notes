### Tiling problem
Ci concentriamo sulla non calcolabilità del problema di *Tiling*.

**Problema:**
Dato un insieme di piastrelle e di regole per metterle insieme, esiste una disposizione del piano che rispetti tali regole?

#### Sistema di Tiling
Un sistema di tiling è costituito da:
- un insieme di piastrelle quadrate $\mathcal{T}$
- una piastrella di origine $t_0 \in \mathcal{T}$ 
- un insieme di regole di adiacenza tra piastrelle

**Definizione:**
Un tiling è una disposizione di piastrelle in $\mathcal{T}$ con le sueguenti proprietà:
- $t_0$ si trova nell'angolo in basso a sinistra
- ogni piastrella ha una piastrella sopra e una a destra, senza spazi
- tutte le regole di adiacenza sono rispettate

*Esempio di regole di adiacenza:*
- una piastrella nera non può avere a destra una grigio chiara

#### Problema di Tiling
Dato un sistema di tiling, il problema è decidere se esiste un tiling.

**Definizione:**
Un sistema di tiling è una tupla $\langle \mathcal{T}, t_0, H, V \rangle$ tale che:
- $\mathcal{T}$ è un insieme finito di piastrelle
- $t_0 \in \mathcal{T}$ è la piastrella di origine
- $H \subseteq \mathcal{T} \times \mathcal{T}$ è un insieme di regole di adiacenza orizzontali e $V \subseteq \mathcal{T} \times \mathcal{T}$ è un insieme di regole di adiacenza verticali

**Definizione:**
Il Tiling, assumendo un quadrato positivo diviso in celle con delle coordinate, e una funzione $f: \mathbb{N} \times \mathbb{N} \rightarrow \mathcal{T}$ tale che:
1.  $f(1, 1) = t_0$
2.  $(f(n, m), f(n+1, m)) \in H$ per ogni $n, m \in \mathbb{N}$
3.  $(f(n, m), f(n, m+1)) \in V$ per ogni $n, m \in \mathbb{N}$

**Dimostrazione:**
Riduciamo il Tiling problem a $ETH^-$, implicando che esso non sia riconoscibile da nessuna TM.

Due passi:
1.  Mostriamo che ogni TM $\mathcal{M}$ può essere traformata in un sistema di tiling $\mathcal{T_{\mathcal{M}}}$


2.  Questa trasformazione è fatta in modo tale per cui $code(\mathcal{M}) \in ETH \Leftrightarrow \text { non eiste un tiling per } \mathcal{T_{\mathcal{M}}}$. Tale corrisponde riduce $ETH$ al complemento del tiling problem, così che $ETH^-$ si riduce al tiling problem.



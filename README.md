\documentclass[10pt]{article}
\usepackage[romanian]{babel}
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage{float}
\usepackage{indentfirst}
\usepackage{amsmath}
\usepackage{amsfonts}
\usepackage{amssymb}
\usepackage{imakeidx}
\usepackage[version=4]{mhchem}
\usepackage{stmaryrd}
\usepackage{graphicx}
\usepackage[export]{adjustbox}
\graphicspath{ {./images/} }
\usepackage[a4paper,top=2cm,bottom=2cm,left=3cm,right=3cm,marginparwidth=1.75cm]{geometry}
\usepackage{algorithm} 
\usepackage{algpseudocode}
\usepackage[colorlinks=true, allcolors=blue]{hyperref}
\usepackage{hyperref}


\title{PROBLEMA SATISFIABILITĂȚII}
\author{Macovei Alexandra Denisa}
\date{}
\begin{document}
\maketitle
\begin{center}
    Facultatea de Matematica si Informatica \\
    Specializarea: Informatica in limba romana \\
    Universitatea de Vest, Timișoara, România \\
    Email: \texttt{alexandra.macovei05@e-uvt.ro} \\
\end{center} 
\vspace{1cm}
\begin{abstract}
\medskip

Problema satisfiabilității booleene (SAT) reprezintă una dintre cele mai importante probleme din informatica teoretică și logica matematică, având aplicații în verificarea formală, optimizare și inteligență artificială. Acest proiect explorează trei metode fundamentale de rezolvare a SAT:

---Rezoluția – generează clauze noi prin combinarea literalilor complementari

---Algoritmul DP – combină eliminarea literalilor puri cu propagarea clauzelor unitare

---DPLL – îmbunătățește DP cu backtracking

Am implementat acești algoritmi în C++, demonstrând pe studii de caz cum:

---O formulă poate fi verificată prin evaluare directă

---DPLL rezolvă eficient instanțe complexe

Rezultatele confirmă că, deși SAT este NP-completă, tehnicile precum DPLL pot rezolva eficient instanțe practice prin combinarea unor strategii inteligente de căutare. Aplicațiile acestor metode extind dincolo domeniul informaticii, oferind instrumente pentru modelarea problemelor complexe din științe umaniste și sociale.

\end{abstract}
\newpage
\tableofcontents 
\newpage

\section{Introducere}

Problema satisfiabilitatii booleene (SAT) este una dintre cele mai fundamentale probleme din informatica teoretica si logica matematica. Ea se reduce la urmatoarea intrebare: Data fiind o formulă logica compusa din variabile booleene, conjunctii (AND), disjunctii (OR) și negatii (NOT), exista o atribuire de valori de adevar (ADEVĂRAT/FALS) pentru variabile care face intreaga formula adevărata? SAT este prototipul problemelor NP-complete, iar solutiile sale au implicații profunde în verificarea formala, optimizare, inteligenta artificiala si proiectarea circuitelor.

Domeniul acopera atât cercetari teoretice (complexitate, algoritmi), cat și aplicatii practice. Acestea mai sunt utilizate pentru a rezolva formule cu milioane de variabile, fiind folosite în verificarea hardware-ului sau în planificarea automatizata.

Soluția constă în abordari hibride: algoritmi probabilistici, metode bazate pe invățare automată sau reducerea SAT la probleme de algebra liniara. Deși problema este NP-completă, multe cazuri practice sunt rezolvabile eficient datorită structurii ascunse a formulelor. SAT rămâne un pilon al informaticii, punând la incercare atat teoreticienii, cat și inginerii.

\section{Descrierea formala a problemei si solutiei}

Determinarea validitatii formulelor în logica propozițiilor:

---Enumerarea tuturor interpretarilor posibile ale atomilor din formula.

---Evaluare a tuturor subformulele pana cand formula este o constanta booleana.

---Rezultat valid daca formula este adevarata în toate interpretarile.

Determinarea satisfiabilitatii formulelor în logica propozitiilor:

---Enumerarea tuturor atribuirilor posibile ale atomilor din formula.

---Evaluare a tuturor subformulelor până când formula este o constantă booleana.

---Rezultat satisfiabil dacă formula este adevarata în cel puțin o interpretare.

\subsection{Rezolutia}

Rezolutia este o regulă de deducție pentru calculul propozițional clasic, utilizată de demonstratoare automate și SAT-solvere. Totodata este utilă pentru construcția unui demonstrator automat corect și complet pentru calculul
propozițional, fără alte teoreme și reguli de deducție. Ca de exemplu, limbajul PROLOG este fundamentat de rezoluție. Rezolvarea necesită ca toate sentințele să fie introduse în FNC. Un set de propoziții în FNC este transformat într-un set de clauze K unde o clauză C este un set de literali, iar fiecare clauză C reprezintă o disjuncție de literali. Mulțimea de clauze K reprezintă o conjuncție de disjuncții de literali. Clauzele sunt rezolvate folosind regula de rezoluție, iar clauza rezultată (rezolventa) este
adăugată la setul inițial de clauze.

--- O clauză este satisfăcută de o atribuire a unei valori de adevăr dacă și numai dacă acea atribuire face ca cel puțin un literal din acea clauză să fie adevărat

--- Un set de clauze este satisfiabil dacă și numai dacă există o atribuire a unei valori de adevăr care satisface toate clauzele din acel set de clauze

--- A determina dacă un anumit set de clauze este satisfiabil - problema satisfibilității

--- În cazul nostru: o mulțime de propoziții este consistentă dacă și numai dacă mulțimea de clauze corespunzător este satisfiabilă


\medskip

\begin{center}
\textbf{Rezoluția este o metodă de verificare a satisfiabilității pentru formule în forma clauzală}
\end{center}

\subsection{Metoda Davis-Putnam}

DP returneaza raspunsul ”satisfiabil” cand regulile nu  mai pot fi aplicate, respectiv ”nesatisfiabil” cand se genereaza clauza vida. De notat ca sunt doua cazuri in care se returneaza ”satisfiabil”: 

--- cand multimea de clauze este vida (se aplica primele doua reguli, care vor fi explicate mai tarziu, pana se sterg toate clauzele)

--- cand rezolutia returneaza ”satisfiabil” (primele doua reguli nu mai pot fi aplicate, asa ca se aplica rezolutia)

\subsection{Metoda Davis-Putnam-Logemann-Loveland}

După ce nu se mai pot aplica reguli pe niciuna dintre subprobleme, se adauga cate o clauza cu un singur literal, intr-un caz normal, iar in altul negat

SATIFIABIL: se obține mulțime vidă de clauze (cel putin pe o ramură)

NESATISFIABIL: se obține clauza vidă (pe toate ramurile/subproblemele)

\section{Modelarea si implementarea problemei si solutiei}

Algoritmul DPLL este o metoda de rezolvare a problemei satisfiabilitatii booleene (SAT). Mai jos este prezentata implementarea sa.

\begin{algorithm}
\caption{Algoritmul DPLL}\label{alg:dpll}
\begin{algorithmic}[1]
\Require O formulă logică în CNF (listă de clauze)
\Ensure \textbf{true} dacă formula este satisfiabilă, \textbf{false} altfel

\Procedure{DPLL}{$clauze$, $atribuiri$}
    \State $(clauze, atribuiri) \gets \textsc{UnitPropagation}(clauze, atribuiri)$
    \If{$clauze$ conține o clauză vidă}
        \State \Return \textbf{false}
    \ElsIf{$clauze$ este goală}
        \State \Return \textbf{true}
    \EndIf

    \State $(clauze, atribuiri) \gets \textsc{PureLiteralElimination}(clauze, atribuiri)$
    \If{$clauze$ este goală}
        \State \Return \textbf{true}
    \EndIf

    \State $v \gets \textsc{AlegeVariabilă}(clauze)$ \Comment{Heuristică}
    \State \Return $\textsc{DPLL}(clauze \cup \{\{v\}\}, atribuiri) \lor \textsc{DPLL}(clauze \cup \{\{\neg v\}\}, atribuiri)$
\EndProcedure

\Statex
\Function{UnitPropagation}{$clauze$, $atribuiri$}
    \While{există o clauză unitară $\{l\}$ în $clauze$}
        \State $atribuiri \gets atribuiri \cup \{l\}$
        \State Elimină din $clauze$ toate clauzele ce conțin $l$
        \State În toate clauzele rămase, șterge $\neg l$
        \If{apare clauză vidă}
            \State \textbf{break}
        \EndIf
    \EndWhile
    \State \Return $(clauze, atribuiri)$
\EndFunction

\Statex
\Function{PureLiteralElimination}{$clauze$, $atribuiri$}
    \For{fiecare literal $l$ în $clauze$}
        \If{$l$ este pur (doar pozitiv sau doar negativ)}
            \State $atribuiri \gets atribuiri \cup \{l\}$
            \State Elimină toate clauzele ce conțin $l$
        \EndIf
    \EndFor
    \State \Return $(clauze, atribuiri)$
\EndFunction
\end{algorithmic}
\end{algorithm}
\newpage
\section*{Explicatii}
Algoritmul funcționeaza prin:
\begin{itemize}
\item Propagarea unitatii - eliminarea clauzelor unitare
\item Eliminarea literalului pur - eliminarea literalilor puri
\item Backtracking - căutarea cu revenire
\end{itemize}

\begin{algorithm}[H]
\caption{Algoritmul de Rezoluție}\label{alg:resolution}
\begin{algorithmic}[1]
\Require Mulțime de clauze în formă CNF
\Ensure \textbf{true} dacă satisfiabilă, \textbf{false} altfel

\State $clauze \gets$ clauzele inițiale
\State $noiClauze \gets \emptyset$

\While{$\text{true}$}
    \For{fiecare pereche de clauze $(C_i, C_j)$ în $clauze$}
        \State $rezolvenți \gets \textsc{Rezolvă}(C_i, C_j)$
        \For{fiecare $R$ în $rezolvenți$}
            \If{$R$ este clauza vidă}
                \State \Return \textbf{false} \Comment{Formula e nesatisfiabilă}
            \EndIf
            \If{$R \notin clauze \cup noiClauze$}
                \State $noiClauze \gets noiClauze \cup \{R\}$
            \EndIf
        \EndFor
    \EndFor
    
    \If{$noiClauze$ este vidă}
        \State \Return \textbf{true} \Comment{Nu s-au găsit noi rezolvenți}
    \Else
        \State $clauze \gets clauze \cup noiClauze$
        \State $noiClauze \gets \emptyset$
    \EndIf
\EndWhile

\Statex
\Function{Rezolvă}{$C_i$, $C_j$}
    \State $rezultate \gets \emptyset$
    \For{fiecare literal $l_i \in C_i$}
        \For{fiecare literal $l_j \in C_j$}
            \If{$l_i = -l_j$}
                \State $R \gets (C_i \setminus \{l_i\}) \cup (C_j \setminus \{l_j\})$
                \If{$R$ nu este tautologie}
                    \State $rezultate \gets rezultate \cup \{R\}$
                \EndIf
            \EndIf
        \EndFor
    \EndFor
    \State \Return $rezultate$
\EndFunction
\end{algorithmic}
\end{algorithm}
\newpage
\section*{Explicatii}
Algoritmul functionează prin:
\begin{itemize}
\item Generarea tuturor rezolventilor posibili între perechi de clauze
\item Adăugarea clauzelor noi la mulțimea existentă
\item Oprire când:
  \begin{itemize}
  \item Se obține clauza vida (nesatisfiabil)
  \item Nu se mai pot genera clauze noi (satisfiabil)
  \end{itemize}
\end{itemize}

\section{Studiu de caz/experiment}

Orice formula logica, in cazul in care nu e deja, trebuie adusa la forma clauzala, si mai exact la o conjuncie de disjunctii(FNC - forma normal conjunctiva). Acest lucru se realizeaza cu ajutorul echivalentelor logice si a reducerii cat mai mult a membrilor. Alteori doar prin tehnica reducerii de termeni se poate demonstra satisfisabilitatea. Tinerea cont de ordinea regulilor de rezolvare este imporatnta, doar daca prima nu se poate aplica se trece la urmatoarea si tot asa mai departe.

\medskip
\textbf{Formă clauzala – Definiții}
\medskip

\begin{itemize}
    \item Un literal este o variabila sau negatia unei variabile
    \item O clauza este o mulțime finita de literali
     \item Clauza $C$ este \emph{triviala} dacă aceasta contine atat un literal cat și forma sa negata ($p \in \text{Var}$, $\text{Var} \to \{0, 1\}$, astfel incat $p, \neg p \in C$)
    \item O clauza este \emph{satisfiabila} daca formula este satisfiabila
    \item Clauza vida ($\varnothing$) nu este satisfiabila (disjunctie indexata de $\varnothing$)
    \item O multime de clauze $S = \{C_1, \ldots, C_m\}$ este satisfiabila daca există o evaluare $e : \text{Var} \to \{0, 1\}$ astfel incat $e(C_i) = 1$ pentru orice $i \in \{1, \ldots, m\}$
\end{itemize}

\textbf{\emph{{\Large Exemplu}}}
\medskip

\subsection{Exercitiu 1}

Consideram formula propozitionala:
\[
\phi = \big((x_{1} \rightarrow x_{2}) \lor \sim\big((\sim x_{1} \leftrightarrow x_{3}) \lor x_{4}\big)\big) \land \sim x_{2}
\]

Atribuirea $\langle x_{1} = 0, x_{2} = 0, x_{3} = 1, x_{4} = 1 \rangle$ este satisfiabilă deoarece:

\begin{align*}
\phi &= \big((0 \rightarrow 0) \lor \sim\big((\sim 0 \leftrightarrow 1) \lor 1\big)\big) \land \sim 0 \\
&= (1 \lor \sim (1 \lor 1)) \land 1 \\
&= (1 \lor \sim 1) \land 1 \\
&= (1 \lor 0) \land 1 \\
&= 1 \land 1 \\
&= 1
\end{align*}
\newpage

\subsection{Exercitiu 2}
Fie formula în CNF:
\[
\phi = (x_1 \lor x_2) \land (\neg x_1 \lor x_3) \land (\neg x_2 \lor \neg x_3) \land (x_3 \lor x_4) \land (\neg x_4)
\]

Rezolvare cu DP (Davis-Putnam)

\begin{enumerate}
    \item \textbf{Pasul 1}: Eliminarea literalului pur
    \begin{itemize}
        \item $\neg x_4$ este pur (apare doar negat)
        \item Fixam $x_4 = 0$
        \item Eliminam clauza $(\neg x_4)$
        \item Simplificam $(x_3 \lor x_4)$ la $x_3$
    \end{itemize}

    \item \textbf{Pasul 2}: Propagarea unitatii
    \begin{itemize}
        \item Clauza unitara $x_3$
        \item Fixam $x_3 = 1$
        \item Simplificam $(\neg x_1 \lor x_3)$ și $(\neg x_2 \lor \neg x_3)$
    \end{itemize}

    \item \textbf{Pasul 3}: Alegem $x_1 = 1$
    \begin{itemize}
        \item Obținem $x_2$ liber
        \item Soluție: $\langle x_1=1, x_2=0/1, x_3=1, x_4=0 \rangle$
    \end{itemize}
\end{enumerate}

\newpage

\begin{figure}
\includegraphics[width=1\linewidth]{sat.jpeg}
\end{figure}

---Regula rezolutiei este solida, deci și metoda rezolutiei este solida deci, daca clauza vida care este o disjunctie generalizata de 0 literali (contradictie) poate fi rezolvata dintr-un set de clauze atunci setul de clauze este nesatisfiabil

--- Rezolutia este completa, adica clauza vida poate fi rezolvata din orice set de clauze nesatisfiabil

Problema: implementare prin enumerare evaluari, asigurandu-ne ca

+ nu pierdem niciuna

+ nu enumerăm niciuna dintre ele mai mult decat este necesar, ceea ce poate duce la neterminarea procesului.

Solutie: utilizarea recursivitatii, lasand implicit o stiva să tina evidenta evaluarilor sub interpretare care au fost deja încercate.

Rezolutia devine procedura de decizie prin epuizarea sistematica a tuturor solutiilor posibile (un număr finit), prin adaugare de strategii de rezolutie.

- Strategii de eliminare a clauzelor: eliminarea tautologiei, eliminarea substitutiei, eliminare literalilor
puri

- Strategii de rezolvare: preferința soluțiilor cu clauze unitare, rezoluție liniara, rezolutie ordonată

\section{Complexitate}
Teoria complexitatii masoară timpul de executie al unui algoritm ca o functie de cantitatea de date oferite spre prelucrare. Daca masuram formula SAT de la intrare dupa numărul de variabile n, atunci algoritmul de mai sus se poate executa pentru o durata proportionala cu 2n, pentru anumite formule. Cea mai des folosita metoda de masurare a complexitatii unui algoritm considera cel mai defavorabil caz posibil. De exemplu, printre formulele SAT de lungime 2 exista multe care se pot rezolva imediat, pentru că din prima incercare putem spune că formula este satisfiabilă. Dar exista cel puţin o formula de lungime 2 pentru care algoritmul trebuie sa faca toate cele 4 incercari posibile. Din cauza aceasta, spunem ca complexitatea algoritmului de mai sus este de ordinul 2n, unde în mod implicit cu n se notează dimensiunea datelor de intrare. Teoria complexitatii considera ca orice clasa de probleme pentru care complexitatea unui algoritm este proportionala cu un o functie polinomiala este eficace; prin contrast, atunci cand complexitatea este proportionala cu o functie exponentială (ca mai sus), problema este considerata nerezolvabila. Pentru ilustratie, algoritmii cei mai buni care sorteaza în ordine crescatoare un sir de n numere, au un timp de executie proportional cu n log n, care este o functie mai mica decat polinomul $n^2$ (pentru că functia logaritmica creste mai incet decat orice polinom). Problema sortarii are deci o soluţie eficace. Teoria complexitatii defineste astfel o multime de probleme numită NP (de la Nedeterminist-Polinomial, o denumire traditionala, care are o justificare despre care nu vom discuta acum): clasa NP este compusa din toate problemele pentru care putem verifica foarte eficient daca un anumit raspuns este o solutie corecta (eficient inseamna, din nou, ca verificarea dureaza un timp polinomial in marimea problemei pe care o avem de rezolvat). SAT si toate problemele de mai sus fac parte din NP. De exemplu, problema circuitului hamiltonian este în clasa NP pentru ca, daca cineva ne da o lista de orase putem verifica foarte rapid daca această lista formeaza sau nu un circuit hamiltonian. Pentru a face asta verificam ca fiecare oras apare o singura data în lista, ca toate orasele de pe harta apar, şi ca intre fiecare doua orase consecutive din lista chiar exista un drum direct. Se defineste de asemenea clasa tuturor problemelor pentru care stim sa calculam raspunsul exact intr-un timp scurt, polinomial ani lungimea datelor de la intrare. Aceasta clasa este denumita simplu, P. Prin definiţie deci, această problema este în clasa NP. Nimeni nu cunoaşte insa un algoritm eficient pentru a decide daca un ciclu hamiltonian exista, deci nu stim daca aceasta problema este în clasa P.

\section{Comparaţie cu literatura}

\begin{tabular}{|l|l|}
\hline
\textbf{Element SAT} & \textbf{Corespondent literar} \\ \hline
Variabila propoziționala & Trasatura de caracter \\ \hline
Clauza & Conflict dramatic \\ \hline
Atribuire & Interpretare critica \\ \hline
\end{tabular}

\begin{itemize}
    \item SAT ofera un cadru formal pentru analiza literara    \item Teorema compactitatii corespunde unitatii operei literare
    \item Complexitatea NP reflecta natura "puzzle" a multor texte
\end{itemize}

\noindent
Cu privire la urmatoarele dimensiuni:

\begin{itemize}
  \item problema - este problema abordata rezolvata sau nu,

  \item solutie - ce solutii exista, care sunt limitarile acestora

  \item domeniu - se poate aplica solutia intr-un domeniu nou, abordari din puncte de vedere diferite?

\end{itemize}

\section{Folosirea acesteia si in alte domenii}
\subsection{Aplicatii în verificarea hardware}
Folosind un SAT solver (de ex. MiniSAT), putem modela un circuit digital simplu cu porti logice și verifica daca exista intrari care duc la o stare de hazard.

\subsection{Modelarea problemei hartilor}
Pentru fiecare regiune $R_i$ si culoare $C_j \in \{1,2,3,4\}$:
\begin{itemize}
\item Fiecare regiune are \textbf{cel putin} o culoare: $\bigvee_{j=1}^4 c_{i,j}$
\item Fiecare regiune are \textbf{cel mult} o culoare: $\neg c_{i,j} \lor \neg c_{i,k}, \forall j \neq k$
\item Regiunile adiacente $R_p, R_q$ au culori diferite: $\neg c_{p,j} \lor \neg c_{q,j}, \forall j$
\end{itemize}

\section{Bibliografie online si nu numai}
O listă cu toate resursele pe care le-am folosit in intocmirea lucrarii.

\begin{itemize}
  \item carţi,
  \item alte materiale - prezentari, orice fel de publicatii,
  \item lucrari.

\end{itemize}


\newpage

\begin{thebibliography}{9}

\bibitem{infoarena}
Infoarena Team. \textit{2-SAT Problem}. 2023. \\
\url{https://infoarena.ro/2-sat} (accesat 15.11.2023)

\bibitem{cmu}
Bădoiu, M. \textit{Problema Satisfiabilității}. Carnegie Mellon University, 2003. \\
\url{https://www.cs.cmu.edu/~mihaib/articole/sat/sat-html.html} (accesat 15.11.2023)

\bibitem{stanford}
Stanford University. \textit{SAT Solving and CSPs}. CS 221, 2022. \\
\url{https://stanford.edu/~shervine/teaching/cs-221/cheatsheet-satisfiability} (accesat 15.11.2023)

\bibitem{mit}
MIT OpenCourseWare. \textit{Advanced SAT Techniques}. 6.045, 2021. \\
\url{https://ocw.mit.edu/courses/6-045j-automata-computability-and-complexity-spring-2011/resources/mit6_045js11_lec07/} (accesat 15.11.2023)

\bibitem{cpp}
CP-Algorithms. \textit{2-SAT}. 2023. \\
\url{https://cp-algorithms.com/graph/2SAT.html} (accesat 15.11.2023)

\bibitem{satcompetition}
SAT Competition 2023. \textit{Benchmark Problems}. \\
\url{https://satcompetition.org/} (accesat 15.11.2023)

\bibitem{wiki}
Wikipedia. \textit{Boolean Satisfiability Problem}. \\
\url{https://en.wikipedia.org/wiki/Boolean_satisfiability_problem} (accesat 15.11.2023)

\bibitem{arxiv}
Biere, A. et al. \textit{Recent Advances in SAT Solving}. arXiv, 2022. \\
\url{https://arxiv.org/abs/2205.03310} (accesat 15.11.2023)

\bibitem{minisat}
MiniSAT. \textit{Open-source SAT Solver}. \\
\url{http://minisat.se/} (accesat 15.11.2023)

\end{thebibliography}

\newpage
\end{document}

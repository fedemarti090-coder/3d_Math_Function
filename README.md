# 3DFunctCalc

![Schermata dell'applicazione](img/screen/img-11.png)

> [!IMPORTANT]
> Tutta l'applicazione è stata sviluppata senza l'uso di librerie esterne, neanche header-only: solo Vulkan SDK e Windows API.

Applicazione desktop per esplorare superfici tridimensionali definite da una funzione di due variabili:

$$z = f(x, y)$$

Il motore C++ calcola la superficie e la disegna con Vulkan. Una finestra di controllo Electron permette di cambiare formula e aspetto mentre l'applicazione è in esecuzione.

| | |
|:---:|:---:|
| <div align="center"><img src="img/c++.png" alt="Logo C++" height="120"></div> | <div align="center"><img src="img/vulkan.png" alt="Logo Vulkan" height="120"></div> |

## Funzionalità

### Formule e superfici

- Inserimento di funzioni che usano le variabili $x$ e $y$.
- Operatori $+$, $-$, $*$, $/$ e $\hat{}$, parentesi e moltiplicazione implicita (ad esempio $2x$ equivale a $2 \cdot x$).
- Funzioni trigonometriche $\sin()$, $\cos()$ e $\tan()$, con argomenti espressi in radianti.
- Anteprima della formula e segnalazione visiva quando il motore non accetta l'espressione.
- Scelta del dominio minimo e massimo e del passo di campionamento. La griglia supporta fino a $512$ intervalli per asse.
- Funzioni d'esempio selezionabili dall'interfaccia:
  - **Sella di Scimmia:** $f(x, y) = x^3 - 3xy^2$
  - **Increspatura:** $f(x, y) = \sin(x^2 + y^2)$
  - **Cartone delle Uova:** $f(x, y) = \cos(x) + \cos(y)$
  - **Croce di Malta:** $f(x, y) = \frac{xy}{x^2 + y^2 + 0.1}$
  - **Griglia di Asintoti:** $f(x, y) = \tan(x)\tan(y)$
  - **Scia a Spirale:** $f(x, y) = \frac{\sin(xy)}{1 + x^2 + y^2}$

### Visualizzazione e controlli

- Rendering della superficie tramite Vulkan, con colore interpolato tra due colori in base all'altezza $z$ e opacità regolabile.
- Rotazione della vista con trascinamento del mouse nella finestra Vulkan: tasto sinistro per la rotazione orizzontale, tasto destro per quella verticale.
- Zoom con la rotellina.
- Slider nell'interfaccia di configurazione per ruotare la scena sui tre assi ($X, Y, Z$), con pulsante per azzerare la rotazione.
- Attivazione degli assi cartesiani e dei piani coordinati.
- Anteprime 3D nell'interfaccia per la rotazione e per gli assi.
- Invio delle impostazioni in tempo reale al motore C++ e aggiornamento della superficie quando cambiano formula, dominio o passo.

## Come è organizzato

- `main.cpp` avvia il motore grafico e collega l'interfaccia.
- `core/calc/mathEnigne.hpp` interpreta le formule, valuta i punti e genera la griglia triangolata.
- `core/windowGPU.hpp` gestisce la finestra, la scena e il rendering Vulkan.
- `core/connection/` gestisce lo scambio di impostazioni e stato tra C++ ed Electron tramite socket TCP locale.
- `setting/` contiene l'interfaccia Electron, le anteprime 3D e i controlli.
- `shaders/` contiene gli shader GLSL e le versioni compilate usate dal renderer.
- `test/` raccoglie prove e script di visualizzazione e test.

## RoadMap

Debug dei valori dell'engine:

![img](img/screen/img-1.png)

Il primo render dei dati...

![img](img/screen/img-2.png)

Il grafico senza i colori

![img](img/screen/img-3.png)

Prima funzione renderizzata

![img](img/screen/img-4.png)

Aggiunta di matrici di rotazione

![img](img/screen/img-5.png)

Aggiunta di matrici di zoom

![img](img/screen/img-6.png)

Implementazione di $\sin$, $\cos$ e $\tan$ nell'engine

![img](img/screen/img-7.png)

Creazione dell'interfaccia grafica

![img](img/screen/img-8.png)

Collegamento parziale tra interfaccia e render

![img](img/screen/img-9.png)

Progetto finale totalmente collegato

![img](img/screen/img-10.png)

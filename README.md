# Scriptorium Arcanum

![Versione](https://img.shields.io/badge/brevetto%20meccanico-1.0.1-b08a45)
![Formato](https://img.shields.io/badge/formato-HTML%20singolo-lightgrey)
![Rete](https://img.shields.io/badge/rete-non%20necessaria-lightgrey)

Piccola storia pratica della crittografia, in un unico file HTML: cinque cifrari da provare con le mani, pensati per studenti delle scuole medie inferiori e superiori. Nasce dal «Cifrario di Polibio dinamico» fornito dall'autore (versione 0.9), di cui conserva stile, colori e font. Non fa parte della serie OFFICINA DEGLI ENIGMI: il piè di pagina riporta solo il titolo e «BREVETTO MECCANICO 1.0.1», senza numero di Machina né anno.

## Contenuto

Cinque schede, nell'ordine:

1. **Cesare** (I sec. a.C.): spostamento dell'alfabeto, chiave da 1 a 25.
2. **Polibio** (II sec. a.C.): quadrato 5×5, coordinate riga-colonna. È lo strumento originale, con parola chiave, griglia casuale, scorrimento di righe e colonne, ispezione delle coppie.
3. **ADFGVX** (1918): quadrato 6×6 (lettere e cifre) e trasposizione a colonne con parola chiave.
4. **Bifido** (1901): quadrato 5×5, coordinate mescolate a blocchi (periodo da 0 a 20; 0 = un solo blocco).
5. **Nichilista** (fine Ottocento): quadrato 5×5 e somma numerica con una parola chiave.

Ogni scheda ha:
- **Storia in un minuto** e **Come si rompe**, in un riquadro richiudibile (chiuso all'apertura).
- **Come si fa**: tutorial a 5 passi. I passi agiscono sullo strumento vero, impostando chiavi e testi. Il riquadro resta fisso in alto sugli schermi di almeno 768×600 px; «Mostra», Avanti e Indietro portano alla sezione «Dietro le quinte».
- **Strumento**: testo in chiaro e testo cifrato sono collegati: scrivendo in uno si aggiorna l'altro (nel campo cifrato si decifra). Errori di chiave e di formato sono segnalati con il motivo.
- **Dietro le quinte**: riga con chiaro e cifrato, quadrato, passaggi intermedi (coppie, tabella di trasposizione, righe e colonne, somme).
- **Prova tu**: esercizi con «Carica nello strumento», suggerimento e verifica.

Funzioni specifiche:
- Cesare: «Prova tutte le chiavi» mostra il cifrato letto con i 25 spostamenti; cliccando una riga si imposta la chiave.
- ADFGVX, Bifido, Nichilista: «Quadrato casuale» e «Ordine» (alfabetico). Il quadrato si riempie dalla parola chiave, senza lettere ripetute, e poi con le lettere rimaste.

Esercizi (6): Cesare con chiave nota, Cesare con chiave sconosciuta, Polibio con parola chiave ROMA, ADFGVX (GERMANIA, MARNE), Bifido (CODICE, periodo 5), Nichilista (ROMA, LUPO). I messaggi cifrati sono calcolati dal programma stesso all'apertura.

I risultati degli esercizi e l'ultima scheda aperta restano nel browser (`localStorage`); «cancella i dati salvati», nel piè di pagina, azzera tutto. Se il browser non consente il salvataggio, il programma funziona lo stesso.

## Regole dei cifrari come implementate

- **Cesare**: solo lettere A–Z, accenti tolti; spazi, numeri e punteggiatura restano. Cifrando si sposta in avanti, decifrando indietro. Output in maiuscolo.
- **Quadrati 5×5**: I e J coincidono. **Quadrato 6×6**: 26 lettere e 10 cifre.
- **ADFGVX**: ogni carattere diventa riga+colonna (A D F G V X). Le coppie si scrivono in righe sotto la parola chiave; le colonne si leggono in ordine alfabetico delle lettere della parola (a parità, da sinistra). Output a gruppi di 5 lettere. Spazi e punteggiatura sono scartati. Parola chiave di trasposizione obbligatoria.
- **Bifido**: per ogni blocco si scrivono le righe di tutte le lettere, poi le colonne; la sequenza si rilegge a coppie. Solo lettere. Chi decifra deve usare lo stesso quadrato e lo stesso periodo.
- **Nichilista**: numero della lettera (11–55) più numero della lettera chiave, ripetuta; il cifrato è una serie di numeri tra 22 e 110. In decifratura un risultato fuori da 11–55 compare come «?».
- **Polibio** (strumento originale): coppie riga-colonna; doppio spazio fra le parole.

## Uso

Aprire `scriptorium-arcanum.html` in un browser moderno. Nessuna dipendenza, nessuna rete: CSS (Tailwind compilato) e font (Cinzel, Cormorant Garamond, IM Fell English SC, sottoinsieme latino) sono incorporati. Dimensione circa 430 KB.

## Cronologia delle versioni

- **0.9**: «Cifrario di Polibio dinamico» fornito dall'autore.
- **1.0**: nome Scriptorium Arcanum, cinque schede, tutorial a passi, esercizi, salvataggio, file autonomo.
- **1.0.1**: pagina meno alta (storia richiudibile, campi più bassi), tutorial fisso in alto, «Mostra» porta a «Dietro le quinte», riga chiaro/cifrato nei passaggi.

## Verifiche

Verificato con test automatici:
- Nucleo crittografico (Node): cifrario di Cesare; nichilista con l'esempio ZEBRAS / RUSSIAN (DYNAMITE → 37 106 62 36 67 47 86 …); ADFGVX con l'esempio ATTACK AT 1200AM, chiave PRIVACY (DGDDD AGDDG AFADD FDADV DVFAA DVX, in gruppi da 5); bifido con FLEEATONCE → UAEOLWRINS e un esempio calcolato a mano. Gli esempi esterni sono quelli che ricordo da Wikipedia, non riconfrontati con la fonte. 1500 prove casuali: cifra e decifra tornano al testo di partenza.
- Chromium (Playwright): le 5 schede, cifra e decifra dalle due direzioni, tabella delle 25 chiavi, tutti i passi dei tutorial, esercizi (risposta errata respinta, soluzione accettata, caricamento nello strumento), errori di chiave, salvataggio dopo ricarica, Polibio originale (LUPO → 31 45 35 34), nessun errore di script, nessuna barra di scorrimento orizzontale a 375, 768 e 1280 px; a 1425×749 il riquadro del tutorial e l'inizio di «Dietro le quinte» sono entrambi visibili dopo «Mostra».

Non verificato:
- I dati storici (Svetonio e lo spostamento di 3, Polibio e le torce, ADFGVX nel 1918 risolto da Georges Painvin nel giugno 1918, bifido di Delastelle del 1901, uso del nichilista da parte di gruppi rivoluzionari russi, al-Kindi e l'analisi delle frequenze) sono scritti da memoria, senza controllo su fonti. La spiegazione delle lettere A D F G V X scelte per il Morse è indicata nel testo come «tradizionale»; la data del nichilista è approssimata.
- Dispositivi reali, tocco, Safari e Firefox; l'aspetto mobile è solo emulato.
- Comprensibilità dei testi per medie inferiori e superiori e difficoltà degli esercizi, non provate con studenti.
- Altezza su schermi molto bassi o con zoom elevato; comportamento del riquadro fisso su dispositivi touch.
- Dimensione del file (circa 430 KB) su connessioni o dispositivi lenti.

Non implementato: esercizi di cifratura (gli esercizi attuali chiedono solo di decifrare), analisi delle frequenze guidata, diagramma delle fasi storiche.

## Licenza

Da definire con l'autore.

---
SCRIPTORIUM ARCANUM · Cinque cifrari da provare con le mani · BREVETTO MECCANICO 1.0.1

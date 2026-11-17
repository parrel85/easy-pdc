# Perdite di carico di una linea

Applicazione web per calcolare le perdite di carico di una linea idraulica dal serbatoio di partenza a quello di arrivo, con la prevalenza richiesta alla pompa e l'NPSH disponibile.

Funziona interamente nel browser: niente installazione, niente account, niente server. Si apre da PC, tablet e telefono.

**Usala online:** https://parrel85.github.io/easy-pdc/

## Cosa calcola

- Perdite distribuite (Darcy-Weisbach) e concentrate (coefficienti ξ dei pezzi speciali) per ogni tratto di tubazione
- Perdite delle valvole di regolazione e di bilanciamento a partire dal Kv, oppure il Kv necessario per ottenere un ΔP
- Prevalenza richiesta alla pompa, potenza idraulica e assorbita
- NPSH disponibile in aspirazione
- Carico in eccesso quando la pompa non serve, e il Kv della valvola che lo dissipa

## Funzionalità

- **Fluidi:** acqua (proprietà in funzione della temperatura), acqua con glicole etilenico o propilenico, fluido personalizzato (per esempio liquami o digestato, con viscosità apparente)
- **Serbatoi:** partenza atmosferica o in pressione (anche in depressione); arrivo atmosferico, in pressione o a scarico libero
- **Tubazioni:** materiale e rugosità, DN da DN15 a DN200 o diametro interno libero, lunghezza, conteggio di curve, T, valvole, filtri, riduzioni, imbocchi e sbocchi
- **Valvole:** di regolazione (Kvs, autorità, Kvs commerciali più vicini) e di bilanciamento (Kv di taratura, ΔP minimo di misura), come tratte separate in qualsiasi punto della linea
- **Verifiche:** velocità e perdita specifica massime, regime laminare, NPSH basso, autorità della valvola, valvola di regolazione in aspirazione
- **DN consigliato** per ogni tratto, applicabile con un clic
- **Schema** della linea con serbatoi, quote, pompa e valvole (sigle V1, V2…)
- **Fino a 5 impianti salvati**, con esportazione e importazione per spostarli tra dispositivi
- **Copia risultati** in testo, da incollare in una relazione
- Tema chiaro e scuro, uso da telefono

## Come si usa

1. Scegli il fluido e inserisci la portata.
2. Imposta il serbatoio di partenza e l'arrivo (tipo, pressione, quota).
3. Inserisci i tratti in ordine dal serbatoio di partenza: tubazioni e valvole, ciascuna segnata come aspirazione o mandata. Con ↑ ↓ cambi l'ordine.
4. Leggi prevalenza, NPSH e avvisi nel riquadro dei risultati; il dettaglio per tratto è in fondo alla pagina.

Quota della pompa, rendimento, pressione atmosferica, limiti di verifica e coefficienti ξ si modificano nella sezione "Pompa, criteri di verifica e coefficienti dei pezzi speciali".

## Metodo di calcolo

| Grandezza | Relazione |
|---|---|
| Perdita distribuita | Darcy-Weisbach: ΔP = λ · (L / D) · ρ v² / 2 |
| Fattore d'attrito, turbolento | Swamee-Jain: λ = 0,25 / [log₁₀(ε / 3,7D + 5,74 / Re⁰·⁹)]² |
| Fattore d'attrito, laminare (Re < 2300) | λ = 64 / Re |
| Perdita concentrata | ΔP = Σξ · ρ v² / 2 |
| Valvole | ΔP [bar] = (Q / Kv)² · ρ / 1000 |
| Prevalenza | H = Δz + Δp / (ρg) + perdite / (ρg) (+ v² / 2g allo scarico libero) |
| NPSH disponibile | (p_serbatoio − p_vapore) / (ρg) + (z_serbatoio − z_pompa) − perdite in aspirazione / (ρg) |
| Autorità valvola di regolazione | ΔP valvola / perdite totali della linea (indicativa) |

Le proprietà dell'acqua (densità, viscosità, tensione di vapore) sono calcolate con correlazioni empiriche in funzione della temperatura (0–95 °C). Le proprietà delle miscele con glicole sono valori indicativi a circa 10 °C, interpolati sulla percentuale.

## Limiti e avvertenze

- Lo strumento è un supporto al dimensionamento preliminare e non sostituisce la verifica di un progettista abilitato né i dati dei costruttori.
- I coefficienti ξ predefiniti sono valori tipici di letteratura: per pezzi speciali e valvole specifici usare i dati del costruttore.
- Per fluidi non newtoniani (liquami densi, digestato) il calcolo usa una viscosità apparente costante: il risultato è indicativo.
- Le proprietà del glicole vanno verificate con la scheda del prodotto usato.
- L'autorità della valvola è stimata sulle sole perdite della linea, senza dislivelli e pressioni dei serbatoi.
- Il calcolo riguarda una linea singola in serie, senza diramazioni.

## Dati e privacy

Gli impianti vengono salvati solo nel browser del dispositivo in uso (localStorage). Nessun dato viene inviato a server esterni. Cancellando i dati del browser gli impianti si perdono: conviene esportarli ogni tanto come copia di sicurezza.

## Installazione e aggiornamento

L'applicazione è un unico file, `index.html`.

- **Uso locale:** scarica `index.html` e aprilo con doppio clic in qualsiasi browser, anche senza connessione.
- **GitHub Pages:** in questo repository, *Settings → Pages → Deploy from a branch*, ramo `main`, cartella `/ (root)`.
- **Aggiornamento:** sostituisci `index.html` con la nuova versione (*Add file → Upload files*, poi *Commit changes*). Gli impianti salvati nel browser restano.

## Licenza

Distribuito con licenza MIT. Vedi il file [LICENSE](LICENSE).

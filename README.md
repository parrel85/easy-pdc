# Perdite di carico di una linea

Applicazione web per calcolare le perdite di carico di una linea idraulica dal serbatoio di partenza a quello di arrivo, con la prevalenza richiesta alla pompa e l'NPSH disponibile.

Funziona interamente nel browser: niente installazione, niente account, niente server. Si apre da PC, tablet e telefono.

**Usala online:** https://parrel85.github.io/easy-pdc/

## Cosa calcola

- Perdite distribuite (Darcy-Weisbach) e concentrate (coefficienti ξ dei pezzi speciali) per ogni tratto di tubazione
- Perdite delle valvole di regolazione e di bilanciamento a partire dal Kv, oppure il Kv necessario per ottenere un ΔP
- Prevalenza richiesta alla pompa, potenza idraulica e assorbita
- NPSH disponibile in aspirazione
- Quota di ogni nodo della linea e pressione a fine di ogni tratta, con controllo di depressione e vaporizzazione nei punti alti
- Carico in eccesso quando la pompa non serve, e il Kv della valvola che lo dissipa

## Funzionalità

- **Fluidi:** acqua (proprietà in funzione della temperatura), acqua con glicole etilenico o propilenico, fluido personalizzato (per esempio liquami o digestato, con viscosità apparente)
- **Serbatoi:** partenza atmosferica o in pressione (anche in depressione), con quota del pelo libero e del bocchello di uscita; arrivo atmosferico, in pressione o a scarico libero
- **Tubazioni:** materiale e rugosità, DN da DN15 a DN200 o diametro interno libero, lunghezza, dislivello, conteggio di curve, T, valvole, filtri, riduzioni, imbocchi e sbocchi
- **Catena di nodi:** le tratte (tubazioni e valvole) sono collegate in serie, ognuna parte dal nodo in cui finisce la precedente; le quote si ricavano dal bocchello di partenza sommando i dislivelli
- **Pompa:** sta su un nodo tra due tratte e si sposta con i suoi pulsanti; le tratte prima della pompa sono in aspirazione, quelle dopo in mandata, e la quota della pompa è quella del suo nodo
- **Valvole:** di regolazione (Kvs, autorità, Kvs commerciali più vicini) e di bilanciamento (Kv di taratura, ΔP minimo di misura), come tratte separate in qualsiasi punto della linea
- **Verifiche:** velocità e perdita specifica massime, regime laminare, NPSH basso, autorità della valvola, valvola di regolazione in aspirazione
- **DN consigliato** per ogni tratto, applicabile con un clic
- **Profilo** della linea in scala: serbatoi, tratte con le loro pendenze, valvole e pompa alle quote reali (sigle T1, T2… e V1, V2…)
- **Fino a 5 impianti salvati**, con esportazione e importazione per spostarli tra dispositivi
- **Copia risultati** in testo, da incollare in una relazione
- Tema chiaro e scuro, uso da telefono

## Come si usa

1. Scegli il fluido e inserisci la portata.
2. Imposta il serbatoio di partenza e l'arrivo (tipo, pressione, quota).
3. Inserisci le tratte in ordine dal serbatoio di partenza: tubazioni con lunghezza e dislivello Δz (positivo se il tubo sale nel verso del flusso) e valvole. Con ↑ ↓ cambi l'ordine; con "↑ prima" e "↓ dopo" sposti la pompa tra le tratte.
4. Leggi prevalenza, NPSH e avvisi nel riquadro dei risultati; il dettaglio per tratto è in fondo alla pagina.

Il rendimento si imposta nella scheda della pompa. Pressione atmosferica, limiti di verifica e coefficienti ξ si modificano nella sezione "Criteri di verifica e coefficienti dei pezzi speciali".

## Metodo di calcolo

| Grandezza | Relazione |
|---|---|
| Perdita distribuita | Darcy-Weisbach: ΔP = λ · (L / D) · ρ v² / 2 |
| Fattore d'attrito, turbolento | Swamee-Jain: λ = 0,25 / [log₁₀(ε / 3,7D + 5,74 / Re⁰·⁹)]² |
| Fattore d'attrito, laminare (Re < 2300) | λ = 64 / Re |
| Perdita concentrata | ΔP = Σξ · ρ v² / 2 |
| Valvole | ΔP [bar] = (Q / Kv)² · ρ / 1000 |
| Prevalenza | H = Δz + Δp / (ρg) + perdite / (ρg) (+ v² / 2g allo scarico libero) |
| Quote dei nodi | z₀ = bocchello di partenza; z_k+1 = z_k + Δz della tratta k |
| NPSH disponibile | (p_serbatoio − p_vapore) / (ρg) + (z_pelo − z_nodo pompa) − perdite in aspirazione / (ρg) |
| Pressione a fine tratto | p = ρg · (carico totale − perdite a monte − z − v² / 2g), con carico totale = p₁ / ρg + z₁ (+ H dopo la pompa) |
| Autorità valvola di regolazione | ΔP valvola / perdite totali della linea (indicativa) |

Le proprietà dell'acqua (densità, viscosità, tensione di vapore) sono calcolate con correlazioni empiriche in funzione della temperatura (0–95 °C). Le proprietà delle miscele con glicole sono valori indicativi a circa 10 °C, interpolati sulla percentuale.

## Limiti e avvertenze

- Lo strumento è un supporto al dimensionamento preliminare e non sostituisce la verifica di un progettista abilitato né i dati dei costruttori.
- I coefficienti ξ predefiniti sono valori tipici di letteratura: per pezzi speciali e valvole specifici usare i dati del costruttore.
- Per fluidi non newtoniani (liquami densi, digestato) il calcolo usa una viscosità apparente costante: il risultato è indicativo.
- Le proprietà del glicole vanno verificate con la scheda del prodotto usato.
- L'autorità della valvola è stimata sulle sole perdite della linea, senza dislivelli e pressioni dei serbatoi.
- Il calcolo riguarda una linea singola in serie, senza diramazioni.
- La prevalenza dipende dalle quote dei peli liberi (o dello scarico), non dalla somma dei salti delle singole tratte, che viene contata una sola volta. I dislivelli servono a ricostruire quote e pressioni lungo la linea e la quota della pompa. Se il tubo scarica sopra il pelo libero del serbatoio di arrivo, la prevalenza è calcolata alla quota dello scarico.

## Dati e privacy

Gli impianti vengono salvati solo nel browser del dispositivo in uso (localStorage). Nessun dato viene inviato a server esterni. Cancellando i dati del browser gli impianti si perdono: conviene esportarli ogni tanto come copia di sicurezza.

## Installazione e aggiornamento

L'applicazione è un unico file, `index.html`.

- **Uso locale:** scarica `index.html` e aprilo con doppio clic in qualsiasi browser, anche senza connessione.
- **GitHub Pages:** in questo repository, *Settings → Pages → Deploy from a branch*, ramo `main`, cartella `/ (root)`.
- **Aggiornamento:** sostituisci `index.html` con la nuova versione (*Add file → Upload files*, poi *Commit changes*). Gli impianti salvati nel browser restano.

## Licenza

Distribuito con licenza MIT. Vedi il file [LICENSE](LICENSE).

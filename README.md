# Il Mondo dei Profumi
### Analisi di mercato del settore fragranze — Power BI

Progetto di portfolio realizzato nell'ambito del corso Data Analyst (Epicode).

---

## Executive Summary

Il progetto combina due fonti di dati reali e pubbliche — **Fragrantica** (marche, note olfattive, valutazioni) ed **eBay** (prezzi e vendite) — per costruire una dashboard Power BI che analizza il mercato dei profumi da tre angolazioni: composizione del mercato, tendenze olfattive nel tempo, e comportamento d'acquisto per genere.

Il progetto è guidato da un principio metodologico costante: **usare solo dati reali, dichiarare onestamente i limiti dell'analisi, ed evitare soluzioni tecniche che non si possano spiegare a fondo**. Ogni scelta di modellazione, ogni misura DAX e ogni taglio temporale applicato ai dati è stato verificato sui valori reali prima di essere adottato — nessun numero è stato stimato o assunto.

## Fonti dati

| Fonte | Contenuto | Righe |
|---|---|---|
| [Fragrantica.com Fragrance Dataset](https://www.kaggle.com/datasets/olgagmiufana1/fragrantica-com-fragrance-dataset) (Kaggle) | Marche, note olfattive, valutazioni | ~24.000 profumi |
| [Perfume E-Commerce Dataset 2024](https://www.kaggle.com/datasets/kanchana1990/perfume-e-commerce-dataset-2024) (Kaggle) | Annunci eBay, prezzi, quantità vendute (uomo/donna) | dataset unito con colonna Gender |

## Le domande di business

1. **Marche e paesi** — quali marche e paesi dominano il mercato per numero di referenze?
2. **Tendenze olfattive** — come cambia la popolarità delle famiglie olfattive nel tempo?
3. **Genere e valutazioni** — l'offerta e il gradimento variano per genere?
4. **Profumi più amati** — quali profumi hanno il miglior equilibrio tra valutazione e numero di voti?
5. **Note di successo** — quali famiglie olfattive caratterizzano davvero i profumi di maggior successo?
6. **Prezzi e vendite** — come si distribuiscono fatturato, prezzo medio e volumi tra i generi?

## Insight chiave

- **Il mercato è frammentato**: le prime 10 marche coprono solo il 13% circa dei 24.063 profumi censiti, su un totale di 1.173 marche.
- **Il gradimento non varia per genere** (rating medio 4,0 / 4,0 / 3,9 su men/unisex/women), nonostante l'offerta sia nettamente sbilanciata verso il segmento femminile (11,4K profumi women contro 5,0K men).
- **Woody, aromatic e citrus** dominano il profilo olfattivo dei 100 profumi più amati — un profilo coerente col segmento maschile/legnoso, sovrarappresentato tra i più apprezzati.
- **Gli uomini superano le donne su tutti gli indicatori commerciali**: fatturato stimato (25,8Mln contro 13,9Mln), prezzo medio (46$ contro 40$) e pezzi venduti (761.669 contro 489.363) — un pattern coerente su tre misure indipendenti.
- **La composizione olfattiva del mercato è relativamente stabile nel tempo**: tra 2000 e 2019, nessuna delle sei famiglie principali varia di più di 2 punti percentuali.

## Metodologia e modello dati

- **Schema a stella**: tre tabelle (`Fact_eBay`, `Fra_Cleaned`, `Bridge_Perfume_Accords`) collegate a una dimensione centrale `Dim_Brand`, con relazioni molti-a-uno a filtro singolo.
- **13 misure DAX** raccolte in una tabella dedicata, incluse `SUMX` per il fatturato riga per riga, `DISTINCTCOUNT` per i valori unici, e una misura composita (`VAR`/`RETURN` + logaritmo) per bilanciare valutazione media e numero di voti nel ranking dei profumi più amati.
- **Pulizia dati separata per fonte** prima dell'unione: uniformazione formati numerici (virgola/punto), correzione nomi marca, gestione onesta dei valori mancanti (etichetta "Unknown" invece di ometterli).
- **Filtro temporale verificato sui dati reali**: l'analisi delle tendenze olfattive parte dal 2000 perché è stato controllato che prima di quell'anno il campione fosse troppo piccolo (talvolta sotto le 10 unità) per generare percentuali statisticamente stabili.

Il dettaglio completo di ogni scelta tecnica — incluse le correzioni, i vicoli ciechi valutati e scartati, e il codice DAX delle misure principali — è documentato nella [relazione completa](./Progetto_Profumi_Relazione.pdf).

## Limiti dichiarati

- Il collegamento tra Fragrantica ed eBay avviene a livello di marca, non di singolo profumo: i due dataset non condividono un identificativo univoco a livello di prodotto.
- I conteggi di popolarità riflettono la presenza su Fragrantica, non necessariamente il volume di vendita reale.
- Il dato sugli anni più recenti (oltre il 2019) ha una copertura campionaria inferiore ed è stato escluso dal confronto temporale principale.

## Stack

Power BI Desktop · Power Query (M) · DAX

## File

| File | Contenuto |
|---|---|
| `Progetto_Profumi.pbix` | La dashboard Power BI (richiede Power BI Desktop) |
| `Progetto_Profumi.pdf` | Esportazione visiva della dashboard, consultabile senza Power BI |
| `Progetto_Profumi_Relazione.pdf` | Relazione metodologica completa |

> I file CSV dei dataset non sono inclusi (sono pubblici su Kaggle, link sopra); i dati sono già incorporati nel file `.pbix`.

---

*Carol Pagano — Corso Data Analyst, Epicode*

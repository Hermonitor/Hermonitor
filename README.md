# Hermonitor

Live overview of international trains crossing the Swiss borders (ICE, TGV, EC, IC, RJX, NJ, TER, RE7):
delays, cancellations and the route of each train. Live at **https://hermonitor.ch**.

> Hermonitor is an **unofficial aid for a rough overview**, not an official timetable or disruption
> information. Times and delay forecasts can be wrong or outdated. Always check the official source of the
> respective railway (DB, ÖBB, SNCF, Trenitalia, SBB).

## Data sources

| Source | Used for |
|---|---|
| [Transitous](https://transitous.org) (MOTIS API; see [sources](https://transitous.org/sources/)) | timetables and realtime for the border stations |
| [transport.opendata.ch](https://transport.opendata.ch) | Swiss stationboards (SBB realtime) |
| [ViaggiaTreno](http://www.viaggiatreno.it) | Italian realtime (Gotthard/Simplon axis) |
| ÖBB timetable information (Scotty) | Austrian forecasts where the other sources have none |

Data of the sources is subject to the licenses/terms of the respective publishers.

## Being light on the data providers

Hermonitor is a static single-page app. All requests to Transitous and transport.opendata.ch go through two
small caching proxies (Vercel functions in [`hermonitor-proxy`](#)), so many users share the same answers
and the load on the providers does **not grow with the number of users**:

- answers are cached for ~2 minutes at the edge, the page refreshes every 2 minutes (agreed with Transitous);
- every request carries a `User-Agent` with name, version and a contact address;
- only the needed read endpoints are forwarded, with a global per-minute and per-day budget;
- after a refusal (HTTP 429/403) the proxy and the page stop asking for 10–60 minutes.

## Files

- `index.html` – the built page that is served at hermonitor.ch
- `train-dashboard.source.html` – the readable source with comments (the built page is generated from it)

## Contact

Questions, errors, or concerns about request volume: **hermonteklebrhan4@gmail.com**

## License

MIT, see `LICENSE`.

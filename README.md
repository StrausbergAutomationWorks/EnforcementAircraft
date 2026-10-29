# EnforcementAircraft

A daily list of aircraft used in immigration enforcement in the United States, and of every aircraft registered to a federal law-enforcement agency. Each aircraft carries its Mode S address (hex), registration, registered owner and the entry that put it on the list. Each entry carries its evidence and sources.

This is a downloadable file, not an API.

## Download

Release `data`, replaced every day:

* `enforcementaircraft.json`: the list
* `SHA256SUMS`: its checksum

`https://github.com/StrausbergAutomationWorks/EnforcementAircraft/releases/download/data/enforcementaircraft.json`

## What is on the list

| Entry kind | What it covers | How it is sourced |
|---|---|---|
| `rule` | Every aircraft in the FAA Releasable Aircraft Database registered to a federal law-enforcement agency (DHS and its components, CBP, ICE, the Department of Justice and its components, the US Marshals Service) or to a named contractor operator | The FAA registry |
| `agency` | Every aircraft registered under the owner names of a state or local agency that published reporting places in immigration enforcement | News reports and official releases, cited in the entry |
| `aircraft` | One aircraft, by hex | Sourced, an ICE Air charter, or found by a behaviour detector and marked `detected_unconfirmed` |

Status is one of:

* `sourced`: published evidence links the entry to the work described.
* `detected_unconfirmed`: an ADS-B behaviour detector found it, and the evidence says what was seen. **This is not a finding that the aircraft took part in immigration enforcement.** A detected aircraft is published only when its registrant is a government body or a listed contractor or front company, or when research finds it involved.
* `ice_air_charter`: an airliner that published evidence ties to ICE Air charter flights, the deportation and transfer flights charter airlines fly for ICE under contract. **The airframe flies other work too, so this is not a finding that any one flight is an ICE flight.** Added 2026-10-29.
* `cleared`: found not to be involved. Cleared entries stay in the file with the reason and the source.

**Entries are only ever added.** One leaves the active list only when it is found not to be involved, and it stays in the file as `cleared`.

A detected aircraft whose address appears to be a Privacy ICAO Address is marked **Potential PIA**. Such an address is temporary and has no public registration.

The researched entries live in `entries.json` in this repository, so each change has its own commit. The release file is built from them and from the FAA registry of the date it names in `registry_date`.

## What the list cannot tell you

* **Being on the list says nothing about any one flight.** Many listed aircraft spend most of their time on other work: patrol, search and rescue, transport, training.
* **Some federal aircraft are not registered under the agency's name.** Coast Guard aircraft are military and are not in the FAA registry. Other agencies have registered aircraft under contractor or front-company names. Those reach the list only as researched or detected entries.
* **It only lists what is published or observed.** Absence from the list is not evidence of anything.

## Format

```json
{
 "name": "EnforcementAircraft",
 "schema": 1,
 "built": "2026-10-23T00:00:00Z",
 "registry_date": "2026-10-21",
 "counts": {"aircraft": 287, "held_back_incomplete": 0, "by_entry": {}, "by_status": {}},
 "entries": [{"id": "...", "kind": "rule|agency|aircraft", "name": "...", "status": "...", "evidence": [{"date": "...", "what": "...", "source_url": "..."}], "added": "...", "cleared": null}],
 "aircraft": [{"hex": "a00808", "registration": "N1007G", "owner": "DEPARTMENT OF HOMELAND SECURITY", "country": "US", "state": "DC", "agency": "DHS", "make": "AIRBUS HELICOPTERS INC", "model": "AS350B3", "icao_type": "AS50", "year": "2022", "entry": "us-federal-law-enforcement", "status": "sourced"}]
}
```

Hex addresses are lower case. Owner names are as the FAA registry writes them.

Every aircraft carries an ICAO type designator. It comes from `faa_icao_types.csv` in this repository, which maps each FAA make and model code to its designator and names the entry in FAA Order JO 7360.1K, *Aircraft Type Designators*, that carries it. An aircraft whose make and model is not mapped there is left out of the file until it is.

## Sources and licence

* Registration data: FAA Releasable Aircraft Database, a public US government record.
* Detections: ADS-B positions from community receiver networks, credited in each detection's evidence.
* The data is licensed under the Open Database License (ODbL) 1.0. See `DATA_LICENSE.md`.

Not affiliated with or endorsed by any government agency.

Corrections, with a source, are welcome as an issue.

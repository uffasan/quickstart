# Record Collection Catalog

## Goal
Catalog a vinyl record collection from cover photos into a Discogs-ready CSV file.

## Photo Batches
Photos will arrive in two named batches. Track which batch each record came from in the `Condition` column:
- **Batch: cleaned** — records that are already cleaned and in sleeves
- **Batch: needs cleaning** — records that still need to be cleaned and sleeved

The user will tell you which batch they're submitting when they hand over photos.

## Output File
Write results to `catalog.csv` in the project folder, appending each batch. Never overwrite previous entries.

Columns:
| Column | Description |
|---|---|
| `artist` | Artist name |
| `album` | Album title |
| `year` | Release year (from cover or lookup) |
| `label` | Record label |
| `catalog_number` | Label catalog number if visible on cover, else blank |
| `country` | Country of pressing if determinable, else blank |
| `discogs_release_id` | Discogs release ID if confidently matched, else blank |
| `condition` | "cleaned" or "needs cleaning" based on batch |
| `flag` | See Flagging section below |
| `flag_notes` | What specific info to look up on the physical record |

## Discogs Matching
For each record, search for the Discogs release ID. A confident match means there is one clear result or the catalog number/country narrows it down unambiguously.

If multiple pressings exist and the cover alone doesn't resolve which one, leave `discogs_release_id` blank and flag it.

## Flagging
Set `flag` to `YES` when:
- Multiple Discogs pressings exist and can't be distinguished from the cover
- Artist or album title is ambiguous or unclear in the photo
- Year, country, or catalog number would be needed to match correctly

Set `flag_notes` to a short instruction for what to check on the physical record, e.g.:
- "Check label for catalog number"
- "Check runout groove — US vs UK pressing"
- "Label needed to confirm year"

Leave `flag` blank and `flag_notes` blank when the match is confident.

## User Priorities
- Primary use: checking collection and wantlist at record sales — exact pressing matters less than having the right artist/album
- Not focused on valuation
- Flagged records will be resolved by the user with the physical record in hand

## Session Kickoff
When the user says something like "catalog the photos in the covers folder", find all image files in the `covers/` subfolder (or whatever folder they specify), process them in order, and append results to `catalog.csv`.

Ask the user which batch (cleaned or needs cleaning) before processing if they haven't said.

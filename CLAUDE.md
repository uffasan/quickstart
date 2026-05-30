# Record Collection Catalog

## Goal
Catalog a vinyl record collection from cover photos into a Discogs-ready CSV file.

## Photo Batches
Photos live in two folders. Track which folder each record came from in the `condition` column:
- **`clean/`** — records already cleaned and in sleeves
- **`dirty/`** — records that still need to be cleaned and sleeved

After cataloging a batch, move the processed photos to the matching archive folder (`archive/clean/` or `archive/dirty/`) so the source folders stay clear for new records.

## Folder Structure
```
~/records/
  CLAUDE.md
  catalog.csv
  clean/          ← drop cleaned/sleeved cover photos here
  dirty/          ← drop photos of records needing cleaning here
  archive/
    clean/        ← processed clean photos moved here
    dirty/        ← processed dirty photos moved here
```

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
| `condition` | "clean" or "dirty" based on source folder |
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
When the user says something like "catalog the new records", process all image files in `clean/` and `dirty/`. After successfully appending each photo's record to `catalog.csv`, move that photo to the corresponding `archive/clean/` or `archive/dirty/` folder.

If both folders are empty, let the user know there's nothing to process.

# PowerPlant Final — NotebookLM Export

- **Source notebook:** PowerPlant Final
- **Notebook ID:** `554c0f2f-9f05-4b77-ba1f-79a25eb92204`
- **Exported:** 2026-05-17
- **Content type:** Indexed fulltext from NotebookLM (PDF text extraction + MP4 transcripts). Original PDF/MP4 binaries are NOT downloadable from NotebookLM — only the indexed text.

## Files

### Lecture videos (transcripts)
- `Lectures_17-30_merged.md` — all 14 MP4 transcripts (lectures 17-30) concatenated in order. Individual `NN_mp4.md` files were merged then deleted on 2026-05-17.

### PDF chapters
- `Chapter_06_Economic_Dispatch.md`
- `Chapter_07_Automatic_Power_Generation.md`
- `Chapter_08_Electric_Power_Substation.md`
- `Chapter_09_Smart_Grid_Digital_Substation.md`
- `Chapter_10_Substation_Protection_Relaying.md`

### Helpers
- `_manifest.json` — id ↔ filename ↔ char count map
- `_download.ps1` — re-run script (idempotent; overwrites .md files)

## Notes
- No artifacts (podcasts/quizzes/reports/notes) existed in the notebook at export time.
- To re-pull (e.g. after adding sources): `& .\_download.ps1` from PowerShell.

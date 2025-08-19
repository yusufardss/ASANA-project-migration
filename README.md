# ASANA Project Migration

Script Python untuk menyalin komentar & attachment dari task sumber → tujuan di Asana, termasuk subtask, anti-duplikat, retry, serta fallback URL untuk file besar.

## Fitur
- Idempotent: hindari duplikat komentar/attachment
- Rekursif hingga subtask
- Retry & rate-limit handling
- Deteksi file > ~95MB → pasang URL
- Log checklist untuk task sumber yang completed

## Prasyarat
- Python 3.9+
- PAT Asana (akun sumber & tujuan)

## Instalasi
pip install -r requirements.txt

## Konfigurasi (di file .py)
- `TOKEN_A`, `TOKEN_B` : PAT sumber/tujuan
- `PROJECT_A`, `PROJECT_B` : GID project
- Pemetaan top-level task:
  - `MATCH_MODE="exact"|"fuzzy"|"csv"`
  - `FUZZY_CUTOFF=0.85` (jika fuzzy)
  - `MAPPING_CSV="mapping.csv"` (jika csv; kolom: `source_task_gid,target_task_gid`)

## Menjalankan
python your_script.py

## Catatan
- Script tidak mengubah status task tujuan; hanya log task sumber yang completed.
- Token ada di kode: **disarankan** pindahkan ke ENV sebelum commit.

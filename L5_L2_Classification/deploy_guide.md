# Deploy Guide — PAX_STORAGE
**Stack:** Python 3.11, SQLite, AES-256-GCM, mmap, AIOSS_FORMAT | Air-gap capable

## Prerequisites
Anticloud core stack installed. PAX 27B weights (pax-27b-q4.gguf). AIOSS_FORMAT.

## Install
```bash
pip install anticloud-pax-storage
```

## AIOSS Integration
```bash
aioss init --module PAX_STORAGE --output ./pax_storage.aioss
```

## Air-Gap
```bash
pip download -r requirements.txt -d ./wheels/
pip install --no-index --find-links ./wheels/ -r requirements.txt
```

## PAX Harness Wiring
```python
from anticloud_pax import PAXHarness
harness = PAXHarness(model_path="./pax-27b-q4.gguf", module="PAX_STORAGE",
                     aioss_chain="./pax_storage.aioss",
                     classification="L5_NARROW_L2_GENERAL")
```

## Verification
```bash
aioss verify --chain ./pax_storage.aioss --verbose
python -m pax_storage.tests.smoke
```

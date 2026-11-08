# Deploy Guide — L_TIMEFLUX
**Tier:** TIER_7_BIOSIGNALS_NEURO | **Stack:** Python 3.11, timeflux 0.x, redis, docker, PAX 27B, AIOSS_FORMAT
**Air-gap capable after initial setup.**

## Prerequisites
Python 3.11+, timeflux 0.x, Redis 7.0+, Docker (for containerized deployment). EEG hardware via K_BRAINFLOW.

## Environment
Docker container runtime. Redis server. EEG hardware or synthetic. 8GB RAM. Low-latency CPU.

## AIOSS Integration
```bash
aioss init --module L_TIMEFLUX --output ./l_timeflux.aioss
aioss append --chain ./l_timeflux.aioss --payload ./output.bin --module L_TIMEFLUX
aioss verify --chain ./l_timeflux.aioss
```

## Air-Gap Setup
```bash
pip download -r requirements.txt -d ./wheels/
pip install --no-index --find-links ./wheels/ -r requirements.txt
```

## PAX 27B Harness Wiring
```python
from anticloud_pax import PAXHarness
harness = PAXHarness(
    model_path="./pax-27b-q4.gguf",
    module="L_TIMEFLUX",
    aioss_chain="./L_TIMEFLUX.aioss",
    classification="L5_NARROW_L2_GENERAL"
)
result = harness.process(input_data)
```

## Verification
```bash
aioss verify --chain ./L_TIMEFLUX.aioss --verbose
python -m L_TIMEFLUX.tests.smoke
```

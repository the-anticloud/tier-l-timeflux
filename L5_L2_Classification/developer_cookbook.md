# Developer Cookbook — L_TIMEFLUX
**Stack:** Python 3.11, timeflux 0.x, redis, docker, PAX 27B, AIOSS_FORMAT
**Domain:** TimeFlux (pipeline): full real-time BCI system deployment for Anticloud clinical use

## Start real-time BCI system
```python
from l_timeflux import TimeFluxBCISystem

system = TimeFluxBCISystem(
    graph="./anticloud_bci_prod.yaml",
    pax_model="./pax-27b-q4.gguf",
    broker="redis://localhost:6379",
    containerized=True,
    aioss_chain="./l_timeflux.aioss"
)

system.start()
print(f"BCI system running. Listening for EEG events...")

for event in system.event_stream():
    print(f"[{event.ts}] {event.type}: {event.payload}")
    system.log_aioss(event)

system.stop()
```

## AIOSS Chain Append
```python
import hashlib, time

def aioss_append(chain_path, payload: bytes, module_id: str):
    entry_hash = hashlib.sha3_256(payload).digest()
    ts = int(time.time_ns()).to_bytes(8, 'big')
    with open(chain_path, 'rb') as f:
        f.seek(-32, 2); prev_hash = f.read(32)
    new_hash = hashlib.sha3_256(prev_hash + entry_hash + ts).digest()
    with open(chain_path, 'ab') as f:
        f.write(ts + entry_hash + new_hash)
    return new_hash.hex()
```

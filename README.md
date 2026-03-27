# Caliptra CSRNG

CTR_DRBG (AES-256) cryptographically secure random number generator from the [CHIPS Alliance Caliptra Root of Trust](https://github.com/chipsalliance/caliptra-rtl).

## Features

- **Algorithm**: CTR_DRBG per NIST SP 800-90A using AES-256 in ECB mode
- **Security strength**: 256 bits
- **Seed length**: 384 bits (KeyLen + BlkLen)
- **Output**: 128-bit random blocks per generate
- **Instances**: Multiple independent DRBG instances (default NHwApps=2 + 1 SW)
- **Commands**: Instantiate, Reseed, Generate, Update, Uninstantiate
- **Bus**: AHB-Lite slave (32/64-bit configurable)
- **Entropy**: Hardware entropy source interface (entropy_src_hw_if)
- **Alerts**: Fatal and recoverable with sparse FSM encoding
- **Interrupts**: 4 (cmd_done, entropy_req, hw_inst_exc, fatal_err)

## Architecture

```
csrng (AHB-Lite wrapper)
├── csrng_core (core integration)
│   ├── csrng_main_sm (command sequencing FSM)
│   ├── csrng_cmd_stage (command interface staging)
│   ├── csrng_ctr_drbg_cmd (seed preparation)
│   ├── csrng_ctr_drbg_upd (DRBG update function)
│   ├── csrng_ctr_drbg_gen (DRBG generate function)
│   ├── csrng_block_encrypt (AES-256 cipher core)
│   └── csrng_state_db (per-instance state database)
└── csrng_reg_top (TL-UL/AHB register interface)
```

## Upstream

Extracted from [chipsalliance/caliptra-rtl](https://github.com/chipsalliance/caliptra-rtl) `src/csrng`. See `upstream.yaml` for commit tracking.

## License

Apache-2.0 — see [LICENSE](LICENSE).

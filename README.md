# clone-lin-maker-clipper-take

Experimental **LIN** clone of MakerDAO / Sky `Clipper.take` — the Dutch-auction
collateral buy (`owe = mul(slice, price)` with tab cap and chost dust floor).

**Proofs live in [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open)** — this repo is the LIN copy only.

- **Upstream (hash-pinned, not vendored):** [makerdao/dss](https://github.com/makerdao/dss) `fa4f6630afb0624d04a003e920b0d71a00331d98`
  - `src/clip.sol` sha256 `1ea897fc0e8e0964a2e5098716d86fdcd93d11e0b2e4f65998eb1b7650d167de` blob `c43d8fff46a4ad225d1fa031b4b1de618345cba7`
  - License AGPL-3.0-or-later. This repository does **not** vendor the Solidity source.
- **LIN kernel:** [`src/lin_maker_clipper_take.lin`](src/lin_maker_clipper_take.lin) (identical to lin-open)
- **C11 oracle copy:** [`test/oracles/maker_clipper_take_c11.c`](test/oracles/maker_clipper_take_c11.c)
- **Transpilable kernel:** [`test/oracles/maker_clipper_take_kernel.c`](test/oracles/maker_clipper_take_kernel.c)
- **Proofs (lin-open only):** `examples/maker_clipper_take/` and `make maker-clipper-take-proof`
- **Class:** EXPERIMENTAL uint64-scale. Not mainnet uint256 rad/wad/ray. Not a production clipper replacement.

Named goldens: FULL `lot=1000 amt=2000 price=100` slice **1000** owe **100000**;
TAB_CAP leftover tab **0** slice **500**; CHOST partial slice **300** leftover tab **70000**;
NO_PARTIAL (tab leq chost, slice lt lot) **0**;
TOO_EXPENSIVE / NEEDS_RESET / STOPPED ge 3 **0**; STOPPED=2 still allows take;
take is not wards-auth; chip/tip are kick/redo not take;
OVERFLOW `7e9*3e9` fail-closes while naive i64 wraps.

## Reproduce proofs (in lin-open)

```
make maker-clipper-take-proof
```

## Not claimed

Uint256 rad/wad/ray / mainnet Clipper.take / Dog.bark parity.
LIN replacing Maker, Sky, clipper, or the EVM. TVL or dollar savings. zk soundness.
`vat.slip` / `vat.flux` / `vat.move`. Hidden `sales[]` maps, `clipperCall` callbacks, or abacus timestamps.

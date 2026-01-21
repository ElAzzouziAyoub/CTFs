# RSA Private Key (d) Recovery — Brutal Cheat Sheet

## Given
- Public modulus: `N`
- Public exponent: `e`

Goal:
- Recover private exponent `d`

---

## Absolute Truth
You **CANNOT** compute `d` from only `N` and `e` **unless RSA is broken**.

If you can factor `N`, RSA is dead.

#### Tools
- FactorDB (first stop)
- yafu
- msieve
- cado-nfs

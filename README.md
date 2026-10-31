# Technical notes

- **Runtime:** ES2022, Web Crypto; HTTPS, localhost, or `file:`. No runtime dependencies. `crypto.getRandomValues()` plus rejection sampling provides unbiased integer draws; failures stop generation.
- **Length profiles:** 15–128 for password-only authentication; 8–128 with MFA, following [NIST SP 800-63B-4 §3.1.1.2](https://pages.nist.gov/800-63-4/sp800-63b.html#passwordver). Verifier-side blocklists, throttling, hashing, and FIPS validation are outside this static app.
- **Word sampling:** dynamic programming counts exact-length sequences; one uniform `BigInt` rank selects the sequence, layout, and case mask. For `n` words, both optional blocks yield `2n(2n+1)` layouts; randomized initials yield `2^n−1` masks. Number/symbol values add factors of 100/8.
- **Character sampling:** uniform alphabet draws, rejecting strings missing a selected character group. Inclusion–exclusion counts accepted strings.
- **Strength display:** `log2(possible outputs)`, assuming uniform secure draws. Fixed grammar/separators contribute zero bits. The 80-bit advisory threshold is app policy, not a NIST requirement or cryptographic validation.
- **Configuration:** `LEXICON` stores word pools; `PhrasePlanner.collection()` defines disjoint grammar templates. Short Story phrases use adjective–noun pairs or single nouns.
- **Browser:** CSP blocks connections (`connect-src 'none'`); no persistence. Clipboard uses `writeText()` with `execCommand("copy")` fallback. Relative asset paths support GitHub Pages project subpaths; `.nojekyll` disables Jekyll.

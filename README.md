# Sample Size Calculator

A static, dependency-free web calculator for clinical and epidemiological sample size estimation. Covers ten scenarios across continuous and dichotomous outcomes using both precision-based and hypothesis-testing approaches — directly replicating R functions from `MESS`, `pwr`, and base R.

🔗 **Live site:** `https://ronaldolum.github.io/sample-size-calculator/`

---

## Scenarios Covered

### Continuous Outcomes

| # | Approach | Scenario | R Equivalent |
|---|----------|----------|--------------|
| 1 | Precision | Single sample mean | Manual formula |
| 2 | Precision | Two-group means | Manual formula |
| 3 | Hypothesis test | One-sample mean | `MESS::power_t_test(..., type = "one.sample")` |
| 4 | Hypothesis test | Two-sample means, equal n | `MESS::power_t_test(..., type = "two.sample")` |
| 5 | Hypothesis test | Two-sample means, unequal n | `MESS::power_t_test(..., ratio = k)` |

### Dichotomous Outcomes

| # | Approach | Scenario | R Equivalent |
|---|----------|----------|--------------|
| 6 | Precision | Single proportion | Manual formula |
| 7 | Precision | Two-group proportions | Manual formula |
| 8 | Hypothesis test | One-sample proportion | `stats::power.prop.test(..., alternative = "one.sided")` |
| 9 | Hypothesis test | Two-sample proportions, equal n | `stats::power.prop.test(..., alternative = "two.sided")` |
| 10 | Hypothesis test | Two-sample proportions, unequal n | `pwr::pwr.2p2n.test(h = ES.h(...))` |

---

## Formulas Used

### Precision-Based (Continuous)

**Single mean:**
```
n = (z_{α/2} × σ / d)²
```

**Two groups:**
```
n₁ = z² × (σ₁² + σ₂² / r) / d²
n₂ = r × n₁
```

### Precision-Based (Dichotomous)

**Single proportion:**
```
n = z² × p × (1−p) / d²
```

**Two groups:**
```
n₁ = z² × (p₁q₁ + p₂q₂ / r) / d²
n₂ = r × n₁
```

### Hypothesis Testing (Continuous)

**One-sample:**
```
n = ((z_α + z_β) × σ / |δ|)²
```

**Two-sample, equal n:**
```
n = (z_α + z_β)² × 2σ² / δ²   (per group)
```

**Two-sample, unequal n:**
```
n₁ = (z_α + z_β)² × σ² × (1 + 1/k) / δ²
n₂ = k × n₁
```

### Hypothesis Testing (Dichotomous)

**One-sample proportion:**
```
n = (z_α√(p₂q₂) + z_β√(p₁q₁))² / (p₁ − p₂)²
```

**Two-sample, equal n (pooled):**
```
n = (z_α√(2p̄q̄) + z_β√(p₁q₁ + p₂q₂))² / (p₁ − p₂)²   (per group)
```

**Two-sample, unequal n (Cohen's h):**
```
h  = 2·arcsin(√p₁) − 2·arcsin(√p₂)
n₁ = (z_α + z_β)² × (1 + 1/k) / h²
n₂ = k × n₁
```

---

## Files

```
/
├── index.html      # Full calculator (single self-contained file)
├── sitemap.xml     # Google sitemap for search indexing
└── README.md       # This file
```

---

## Deploying to GitHub Pages

1. Create a new GitHub repository (public).
2. Upload `index.html`, `sitemap.xml`, and `README.md` to the root.
3. Go to **Settings → Pages**.
4. Under *Source*, select **Deploy from a branch** → `main` → `/ (root)`.
5. Click **Save**. Your site will be live at:
   ```
   https://ronaldolum.github.io/sample-size-calculator/
   ```
6. Update the `<loc>` URL in `sitemap.xml` to match your live URL, then re-upload.

---

## Local Development

No build tools required. Open `index.html` directly in any modern browser:

```bash
# Option 1 — just open the file
open index.html

# Option 2 — serve locally (Python)
python3 -m http.server 8000
# then visit http://localhost:8000
```

---

## Browser Support

Works in all modern browsers (Chrome, Firefox, Safari, Edge). No external dependencies beyond Google Fonts (loaded via CDN; falls back gracefully if offline).

---

## License

© 2026 Ronald Olum. All rights reserved.

This project and its source code may not be used, copied, modified, or distributed without explicit permission from the author.

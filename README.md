# pd5219-DATAB-projekt
# Wyniki zapytań SQL

### Zapytanie 2: Testy z więcej niż 30 pacjentami

```sql
SELECT t.test_type, COUNT(DISTINCT pt.patient_id) AS patient_count
FROM tests t
JOIN patient_test pt ON t.test_id = pt.test_id
GROUP BY t.test_type
HAVING patient_count > 30;
```

**Wynik:**

| test_type | patient_count |
|-----------|---------------|
| NGS-panel | 38 |
| SNP Array | 39 |
### Zapytanie 3: Średnia liczba wariantów dla każdego testu

```sql
SELECT t.test_type, AVG(variant_count) AS avg_variants
FROM tests t
JOIN (
    SELECT test_id, COUNT(*) AS variant_count
    FROM results
    GROUP BY test_id
) r ON t.test_id = r.test_id
GROUP BY t.test_type;
```
**Wynik:**

| test_type | avg_variants |
|-----------|--------------|
| SNP Array | 3.0000 |
| NGS-panel | 3.6857 |
| WES | 3.5294 |
| WGS | 3.6071 |

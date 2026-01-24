# Конспект первой сессии: SQL-логика и мышление аналитика

**Дата:** 20.07.2024
**Тема:** Основы SQL, ключевое отличие WHERE и HAVING.

## Главный инсайт: WHERE vs HAVING

*   **`WHERE`** — фильтрует **СТРОКИ** **ДО** группировки (`GROUP BY`).
    *   *Пример:* `WHERE year = 2023 AND status = 'Акт'`
*   **`HAVING`** — фильтрует **ГРУППЫ** **ПОСЛЕ** группировки.
    *   *Пример:* `HAVING SUM(amount) > 1000000`

## Правило
> `WHERE` — для фильтрации по полям таблицы.  
> `HAVING` — для фильтрации по результатам (`SUM`, `COUNT`, `AVG`).

## Пример
```sql
-- Найти отделы со средней зарплатой > 50000 и больше 3 сотрудников
SELECT
    department,
    AVG(salary) as avg_salary,
    COUNT(*) as emp_count
FROM employees
WHERE active = TRUE       -- Фильтр строк ДО группировки
GROUP BY department
HAVING AVG(salary) > 50000 AND COUNT(*) > 3 -- Фильтр групп ПОСЛЕ
ORDER BY avg_salary DESC;

# Домашнее задание к занятию "`SQL. Часть 2`" - `Баланюк Евгения`

---

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

```
SELECT s.store_id, CONCAT(s2.first_name, ' ', s2.last_name), c.city, COUNT(c2.customer_id) 
FROM store s
JOIN staff s2 ON s2.store_id = s.store_id
JOIN address a ON a.address_id = s2.address_id
JOIN city c ON c.city_id = a.city_id
JOIN customer c2 ON c2.store_id = s.store_id
GROUP BY s.store_id, CONCAT(s2.first_name, ' ', s2.last_name), c.city
HAVING COUNT(c2.customer_id) > 300;
```

![](https://github.com/EvgeniyaBalanyuk/screenshots/blob/main/SQL_2%20№1.png)

### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

```
SELECT COUNT(film_id)
FROM film
WHERE length > (SELECT AVG(length) FROM film);
```

![](https://github.com/EvgeniyaBalanyuk/screenshots/blob/main/SQL_2%20№2.png)

### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

```
SELECT MONTH(p.payment_date), SUM(p.amount) payments, COUNT(r.rental_id) 
FROM payment p 
JOIN rental r ON r.rental_id = p.rental_id 
GROUP BY MONTH(p.payment_date)
ORDER BY payments DESC
LIMIT 1;
```

![](https://github.com/EvgeniyaBalanyuk/screenshots/blob/main/SQL_2%20№3.png)

# sql-odev-12
1)film tablosunda film uzunluğu length sütununda gösterilmektedir. Uzunluğu ortalama film uzunluğundan fazla kaç tane film vardır?
2)film tablosunda en yüksek rental_rate değerine sahip kaç tane film vardır?
3)film tablosunda en düşük rental_rate ve en düşün replacement_cost değerlerine sahip filmleri sıralayınız.
4)payment tablosunda en fazla sayıda alışveriş yapan müşterileri(customer) sıralayınız.
1)
SELECT Count(length)
FROM film
WHERE length >
(
	SELECT AVG(length)
	FROM film
);

2)
SELECT COUNT(rental_rate)
FROM film
WHERE rental_rate =
(
	SELECT MAX(rental_rate)
	FROM film
);

3)
SELECT title, rental_rate, replacement_cost, (SELECT MIN(rental_rate) FROM film), (SELECT MIN(replacement_cost) FROM film)
FROM film
WHERE rental_rate =
(
	SELECT MIN(rental_rate)
	FROM film
)
AND replacement_cost = 
(
	SELECT MIN(replacement_cost)
	FROM Film
);

4)

SELECT customer.first_name, customer.last_name, payment.customer_id, COUNT(payment.customer_id)
FROM payment, customer
WHERE customer.customer_id = payment.customer_id
GROUP BY customer.first_name, customer.last_name, payment.customer_id
ORDER BY COUNT(payment.customer_id) DESC;

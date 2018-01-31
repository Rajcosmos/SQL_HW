1a. select first_name,last_name from actor;

1b. select concat(upper(first_name),' ',upper(last_name)) as 'Actor Name' from actor;

2a. select actor_id,first_name,last_name from actor where first_name='Joe';

2b. select * from actor where last_name REGEXP 'GEN';

2c. select * from actor where last_name REGEXP 'LI' order by last_name,first_name;

2d. select country_id,country from country where country IN ('Afghanistan','Bangladesh','China');

3a.alter table actor add column middle_name varchar (45) after first_name;

3b.alter table actor modify column middle_name blob;

3c.alter table actor drop column middle_name;

4a. select last_name,count(*) from actor group by last_name;

4b. select last_name,count(*) as c from actor group by last_name having c>=2;

4c. update actor set first_name='HARPO', last_name='WILLIAMS' where first_name like 'GROUCHO' and last_name like 'WILLIAMS';

4d. update actor set first_name= CASE when first_name='HARPO' then 'GROUCHO' else 'MOUCHO GROUCHO' END where actor_id=172;

5a. show create table address;

6a. select s.first_name,s.last_name,a.address from staff s inner join address a on a.address_id=s.address_id;

6b. select s.first_name,s.last_name,s.staff_id,sum(amount) from staff s join payment p using(staff_id) where payment_date like '2005-08%' group by staff_id ;

6c. select count(fa.actor_id),f.title from film_actor fa inner join film f on fa.film_id=f.film_id group by title;

6d. select f.title,count(film_id) from inventory i join film f using (film_id) where title like 'Hunchback Impossible';

6e. select c.first_name,c.last_name,c.customer_id, sum(amount) from customer c join payment using (customer_id) group by customer_id order by last_name;

7a. select title from film where title like 'K%' or title like 'Q%' and language_id in (select language_id from language where name = 'English');

7b. select first_name,last_name from actor where actor_id in (select actor_id from film_actor where film_id in (select film_id from film where title in ('Alone Trip')));

7c. select c.email from customer c join address using (address_id) join city using (city_id) join country using (country_id) where country = 'Canada';

7d. select title from film where film_id in (select film_id from film_category where category_id in (select category_id from category where name='Family'));

7e. select title, count(film_id) as frequently_rented from rental join inventory using (inventory_id) join film using (film_id) group by title order by frequently_rented desc;

7f.select store_id, concat('$',format(sum(amount),2)) as total_revenue from payment join staff using (staff_id) join store using (store_id) group by store_id;

7g.select store_id,address,city,country from address join store using (address_id) join city using (city_id) join country using (country_id);

7h.select sum(amount) as total,name from film_category join category using (category_id) join inventory using (film_id) join rental using (inventory_id) join payment using(rental_id) group by name order by total desc limit 5;

8a.create view top_five_genres as select sum(amount) as total,name from film_category join category using (category_id) join inventory using (film_id) join rental using (inventory_id) join payment using(rental_id) group by name order by total desc limit 5;

8b.select * from top_five_genres; Note: (select * from <view_name>)

8c.drop view top_five_genres;

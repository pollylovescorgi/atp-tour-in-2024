# atp-tour-in-2024
Useful insights from men's tennis results in 2024

Итак, начнем анализ с определения топ-10 теннисистов, которые одержали наибольшее кол-во побед в 2024 году, а потом выведем данные о победителях турниров и общем кол-ве трофеев за прошедший сезон

```python
select "Winner", COUNT("Winner") as count_of_wins
from atp_tennis at
where "Date" like '2024%'
group by "Winner"
order by count_of_wins desc
limit 10
	
select "Winner", count("Winner") as count_of_trophies
from atp_tennis at
where "Round" = 'The Final' 
and "Date" like '2024%'
group by "Winner" 
order by count_of_trophies desc
```

Теперь рассмотрим единоличного лидера по показателям выше - какие турниры выиграл Янник Синнер и на каких покрытиях

```python
select "Tournament", "Series"
from atp_tennis at
where "Winner" = 'Sinner J.' 
and "Date" like '2024%' 
and "Round" = 'The Final'
```

```python
select "Surface",count("Surface") as titles_on_each_surface
from atp_tennis at
where "Winner" = 'Sinner J.' 
and "Date" like '2024%' 
and "Round" = 'The Final'
group by "Surface" 
order by titles_on_each_surface desc
```

Из результата запроса можно увидеть, что большинство побед Синнера в 2024 году пришлось на турниры, проходившие на покрытии "хард". Справедливо ли сделать общий вывод, что лидер мирового рейтинга прежде всего должен уметь успешно играть именно на этом покрытии? Можно проверить, посчитав кол-во матчей на каждом из покрытий 

```python
select "Surface", count("Surface") as num_of_matches
from atp_tennis at
where "Date" like '2024%'
group by "Surface"
order by num_of_matches desc
```

Действительно, в 2024 году было сыграно 1488 матчей на "харде", 832 - на грунте и всего 311 на траве. Учитывая разницу между кол-ом сыгранных матчей, справедливо утверждение, что в настоящее время важным требованием для доминирования в ATP-туре является качественная игра на харде 

Теперь рассмотрим результаты сезона 2024 года на разного рода рекорды и аномалии. Так, например, на последнем турнире в Монако был сыгран матч с итоговым счетом 6-0 6-0. Были ли такие результаты в 2024 году? 

```python
select "Winner", COUNT("Score") as count_of_scores
from atp_tennis at
where "Score" = '6-0 6-0' 
and "Date" like '2024%'
group by "Winner"
```

Но были ли "выписаны баранки" хотя бы в одном из сыгранных сетов? 

```python
select "Winner", COUNT("Score") as count_of_scores
from atp_tennis at 
where "Score" like '%6-0%' 
and "Date" like '2024%'
group by "Winner"
order by count_of_scores desc
```

Да, такие сеты с "баранками" были. Лидером по этому показателю в 2024 году стал Алекс Деминор (5 сетов) - победитель того самого матча в Монте-Карло 

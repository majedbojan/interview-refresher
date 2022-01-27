# Basic

## Basic string searches

```sql
select *
	from cd.facilities
	where
		name like '%Tennis%';
```

## Matching against multiple possible values

```sql
select *
	from cd.facilities
	where
		facid in (1,5);
```

```sql
select *
	from cd.facilities
	where
		facid in (
			select facid from cd.facilities
			);
```

## Classify results into buckets

```sql
select name,
       case when (monthlymaintenance > 100) then
	     'expensive'
		 else
		 'cheap'
		 end AS cost
       from cd.facilities
```

## Working with dates

```sql
select memid, surname, firstname, joindate
	from cd.members
	where joindate >= '2012-09-01';
```

## Removing duplicates, and ordering results

```sql
select distinct surname
	from cd.members
order by surname
limit 10;
```

## Combining results from multiple queries

```sql
select surname
	from cd.members
union
select name
	from cd.facilities;
```

## Simple aggregation

- You'd like to get the signup date of your last member

```sql
select joindate AS latest
  from cd.members
  order by joindate DESC
  limit 1;
```

```sql
select max(joindate) as latest
  from cd.members
```

## More aggregation

```sql
select firstname, surname, joindate
	from cd.members
	where joindate =
		(select max(joindate)
			from cd.members);
```

```sql
select firstname, surname, joindate
  from cd.members
  order by joindate desc
  limit 1

```

# Joins and Subqueries

Different types of the JOINs in SQL:

- `(INNER) JOIN`: Returns records that have matching values in both tables
- `LEFT (OUTER) JOIN`: Returns all records from the left table, and the matched records from the right table
- `RIGHT (OUTER) JOIN`: Returns all records from the right table, and the matched records from the left table
- `FULL (OUTER) JOIN`: Returns all records when there is a match in either left or right table

## Retrieve the start times of members' bookings (Inner join)

How can you produce a list of the start times for bookings by members named 'David Farrell'?

### inner join

```sql
select starttime
       from cd.bookings bks
       INNER JOIN cd.members mems
	   on mems.memid = bks.memid
       where
	   mems.firstname = 'David' AND mems.surname = 'Farrell'
```

### Another format of inner join

```sql
select bks.starttime
       from
	     cd.bookings bks,
         cd.members mems
       where
	     mems.firstname = 'David'
		 AND
		 mems.surname = 'Farrell'
		 AND
		 mems.memid = bks.memid
```

- How can you produce a list of the start times for bookings for tennis courts, for the date '2012-09-21'? Return a list of start time and facility name pairings, ordered by the time.

```sql
select starttime as start, fs.name as name
from
  cd.bookings bks
inner join
  cd.facilities fs
 on bks.facid = fs.facid
where fs.name in('Tennis Court 1', 'Tennis Court 2')
and bks.starttime >= '2012-09-21'
and bks.starttime < '2012-09-22'
Order by bks.starttime
```

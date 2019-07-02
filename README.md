# Authoritative articles

1. Using your favorite DB client, design and create a table called `authors` that would store the first name, the last name, and the sex of each of the following authors:
    
      - Abi Maxwell (F)
      - Anthony Alofsin (M)
      - Emily Temple (F)
      - Gabrielle Bellot (F)
      - Meg Donohue (F)
      - Philip Eil (M)
      - Roxana Robinson (F)
      - Tobias Carroll (M)
      - Veronica Esposito (F)
     
    Don’t forget that each table must have an ID field. Please also create the necessary constraints, keys and/or indices for the table. In order to do this you might first need to read this document through the end.
     
    Copy and paste the SQL query generated by the client below:
    
    ```postgresql
   create table authors
   (
   	id int,
   	"First name" text,
   	"Last name" text,
   	"Sex" text
   );
    ```

2. **Manually** create a query or a series of queries filling the table with the data. Put the query/queries below:

    ```postgresql
    INSERT INTO "authors" ("id", "First name", "Last name", "Sex") VALUES (1, 'Abi', 'Maxwell', 'F');
    INSERT INTO "authors" ("id", "First name", "Last name", "Sex") VALUES (2, 'Anthony', 'Alofsin', 'M');
    INSERT INTO "authors" ("id", "First name", "Last name", "Sex") VALUES (3, 'Emily', 'Temple', 'F');
    INSERT INTO "authors" ("id", "First name", "Last name", "Sex") VALUES (4, 'Gabrielle', 'Bellot', 'F');
    INSERT INTO "authors" ("id", "First name", "Last name", "Sex") VALUES (5, 'Meg', 'Donohue', 'F');
    INSERT INTO "authors" ("id", "First name", "Last name", "Sex") VALUES (6, 'Philip', 'Eil', 'M');
    INSERT INTO "authors" ("id", "First name", "Last name", "Sex") VALUES (7, 'Roxana', 'Robinson', 'F');
    INSERT INTO "authors" ("id", "First name", "Last name", "Sex") VALUES (8, 'Tobias', 'Carroll', 'M');
    INSERT INTO "authors" ("id", "First name", "Last name", "Sex") VALUES (9, 'Veronica', 'Esposito', 'F');
    ```

3. Using the client, design and create a table called `articles` that would store the information from the file [articles.xlsx](articles.xlsx). Use the already created `authors` table in order to refer to the authors. Don’t forget to create an ID field and all necessary constraints/keys/indices.

    Copy and paste the SQL query generated by the client below:

    ```postgresql
   create table articles
   (
   	Title text,
   	Author_id int,
   	Date date,
   	Rating double precision,
   	Text text
   );
    ```

4. **Using the client**, fill the table:

    ```postgresql
   INSERT INTO "articles" ("title", "author_id", "date", "rating", "text") VALUES ('How Alison Bechdel Understands Her Life as Fiction', 4, '2017-10-04', 4.3, '<p>A third of the ...');
   INSERT INTO "articles" ("title", "author_id", "date", "rating", "text") VALUES ('How Jamaica Kincaid Helped Me Understand My Mother', 4, '2019-03-22', 3.35, '<p>For two decades...</p>');
   INSERT INTO "articles" ("title", "author_id", "date", "rating", "text") VALUES ('How Many Copies Did Famous Books Sell in the First Year?', 3, '2019-06-25', 2.4, '<p>Book publishing can ...</p>');
   INSERT INTO "articles" ("title", "author_id", "date", "rating", "text") VALUES ('My Decade-Long Fascination with the Tale of Monica Lewinsky', 4, '2019-05-29', 5, '<p>For over a decade ...</p>');
   INSERT INTO "articles" ("title", "author_id", "date", "rating", "text") VALUES ('On “Good Men” and the Vague, Low Standards Required to Be One', 1, '2018-04-29', 4.5, '<p>The first time I ...</p>');
   INSERT INTO "articles" ("title", "author_id", "date", "rating", "text") VALUES ('On Frank Lloyd Wright and the Architectural War For New York’s Skyline', 2, '2019-02-01', 3.85, '<p>The New ...”</p>');
   INSERT INTO "articles" ("title", "author_id", "date", "rating", "text") VALUES ('On the Modern American Obsession with French Revolution Narratives', 8, '2019-05-03', 4, '<p>Will we ever run ....</p>');
   INSERT INTO "articles" ("title", "author_id", "date", "rating", "text") VALUES ('On Walt Whitman, Unsung Newspaperman', 6, '2018-09-15', 4.25, '<p>There are ...</p>');
   INSERT INTO "articles" ("title", "author_id", "date", "rating", "text") VALUES ('The 12 Best Book Covers of June', null, '2019-06-27', 3.75, '<p>Another month ...</p>');
   INSERT INTO "articles" ("title", "author_id", "date", "rating", "text") VALUES ('The Grand Cultural Influence of Octavia Butler', 3, '2019-06-21', 3.8, '<p>Tomorrow, June 22, ...</p>');
   INSERT INTO "articles" ("title", "author_id", "date", "rating", "text") VALUES ('What Gets Lost (and Found) in Translating Prose to Comics', 8, '2019-01-08', 4.6, '<p>As goes language, ...</p>');
   INSERT INTO "articles" ("title", "author_id", "date", "rating", "text") VALUES ('Why We’ll Never Get Tired of Literary Retellings', 5, '2019-05-28', 4.95, '<p>I make an effort to r....</p>');
    ```

5. Retrieve articles with the information about the author attached to each row (there should be 12 rows in the result and around 10 columns, including the article’s title, text, rating, and date as well as the author’s name and sex):

    ```postgresql
   SELECT * FROM articles INNER JOIN authors ON articles.author_id = authors.id;
    ```

6. To get the twelve rows, you must have used one of the constructions `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, or `FULL JOIN`. How many rows would the other three have returned? First try to think of the answers and then verify them by running the queries (it’s important you understand the results). Put the numbers below:

    ```
    INNER JOIN: ? 12
    LEFT JOIN: ? 13
    RIGHT JOIN: ? 14
    FULL JOIN: ? 15
    ```

7. Imagine you’re using pagination to display articles showing five articles per page. Retrieve the content for the first page: create a query that would return the latest five articles, ordered from the latest to the earliest.

    ```postgresql
    SELECT * FROM  articles  LIMIT 5 OFFSET 7;
    ```

8. Retrieve the content for the second page: articles 6 through 10 (still assuming chronological order).

    ```postgresql
   SELECT * FROM  articles LIMIT 5 OFFSET 5;
    ```
    
9. Retrieve the content for the third page: articles 11 through 15 (never mind there are actually only 12 of them currently in the table).

    ```postgresql
    SELECT * FROM  articles LIMIT 5 OFFSET 10;
    ```
    
10. Count the number of five-article pages required to accommodate all articles:

    ```postgresql
    SELECT ceil(count(*)/5::double precision)  FROM  articles;
    ```
    
11. Calculate an average rating of the articles, rounded to the nearest integer:

    ```postgresql
    SELECT round(AVG(rating)) FROM  articles;
    ```

12. Count males and females among the authors. There should be two rows (for males and females) and two columns: `sex` (`F` or `M`) and `cnt` (count).

    ```postgresql
    SELECT count('F') AS "cnt","Sex" FROM  authors GROUP BY "Sex";
    ```

13. Find the date of the earliest (put in the column `earliest`) and latest (put in the column `latest`) article written by each author:

    ```postgresql
    SELECT authors."First name" ||' '|| authors."Last name",
    min(articles.date) AS "earliest",
    max(articles.date) AS "latest"
    FROM authors INNER JOIN articles ON articles.author_id = authors.id
    GROUP BY authors."First name" ||' '|| authors."Last name";
    ```
    
14. Calculate the total length of the text written by each author (count both `text` and `title`; you can keep the tags in `text` while counting):

    ```postgresql
    SELECT authors."First name" ||' '|| authors."Last name", sum(length(title) + length(text))
    FROM articles LEFT JOIN authors ON articles.author_id = authors.id
    GROUP BY author_id, authors."First name", authors."Last name";
    ```
    
15. Output all the authors in a random order. There should be only one column aliased `author` with the first and last name of the author concatenated (using a space, of course). The order of the rows should be different on each request:

    ```postgresql
    SELECT "First name" ||' '|| "Last name" AS "author"
    FROM authors ORDER BY RANDOM()
    LIMIT 9;
    ```

16. "Anonymize" the authors: replace each author’s last name with the properly capitalized reverse of it. E.g., `Alofsin` should become `Nisfola`, `Esposito` should become `Otisopse`, etc.

    ```postgresql
    UPDATE authors SET  "Last name" = reverse("Last name");
    ```
    
17. Delete all articles that don’t have an author:

    ```postgresql
    DELETE FROM articles WHERE author_id IS null;
    ```

18. **(optional)** Delete all authors that haven’t written any articles:

    ```postgresql
    ... here goes your SQL ...
    ```

Don’t forget to create a pull request.

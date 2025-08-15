# Netflix SQL Analysis

This project contains a collection of SQL queries for analyzing a Netflix dataset stored in two tables:  
- **`shows_movies.titles`** — metadata for movies and TV shows  
- **`shows_movies.credits`** — cast and crew information  

The queries cover rating analysis, genre breakdowns, country-level stats, top/bottom performers, and people (actors/directors) with notable contributions.

---

## 📂 Dataset Structure

### Table: `shows_movies.titles`
| Column                | Type        | Description |
|-----------------------|-------------|-------------|
| `id`                  | INT         | Unique ID for the title |
| `title`               | VARCHAR     | Name of the movie/show |
| `type`                | VARCHAR     | `Movie` or `Show` |
| `imdb_score`          | FLOAT       | IMDb rating |
| `tmdb_score`          | FLOAT       | TMDB rating |
| `tmdb_popularity`     | FLOAT       | TMDB popularity metric |
| `release_year`        | INT         | Year of release |
| `runtime`             | FLOAT       | Duration in minutes |
| `seasons`             | INT         | Number of seasons (for shows) |
| `genres`              | VARCHAR     | Genre(s) of the title |
| `production_countries`| VARCHAR     | Countries of production |
| `age_certification`   | VARCHAR     | Age rating (e.g., PG-13) |

### Table: `shows_movies.credits`
| Column           | Type        | Description |
|------------------|-------------|-------------|
| `id`             | INT         | Title ID (foreign key to `titles.id`) |
| `name`           | VARCHAR     | Name of the person |
| `role`           | VARCHAR     | `actor`, `actress`, or `director` |
| `character`      | VARCHAR     | Character played (for actors) |

---

## 🛠 Requirements
- SQL engine (MySQL, PostgreSQL, or compatible)
- The `shows_movies` schema with both tables populated
- Proper indexing on `id`, `type`, `role` for best performance

---

## 📊 Query Categories

### Ratings & Rankings
1. **Top 10 movies/shows by IMDb score**
2. **Bottom 10 movies/shows by IMDb score**
3. **Average IMDb and TMDB scores** for movies vs shows
4. **Top actors & directors** by number of appearances

### Time & Trend Analysis
5. Count of movies/shows **per decade**
6. Number of titles **released each year**
7. **Average runtimes** by type (movie/show)

### Country & Certification
8. Average scores per **production country**
9. Average scores per **age certification**
10. Most common **age certifications** for movies

### Genres
11. **Top genres** for movies and shows
12. Top 3 **most common genres** overall

### People-Centric Insights
13. Actors in **highly rated titles**
14. Actors/actresses playing **the same character** in multiple titles
15. Average IMDb score for **leading roles**

### Special Filters
16. Movies with **high IMDb score (>7.5)** and **high TMDB popularity (>80)**
17. Shows with **most seasons**
18. Movies released **since 2010** with their directors

---

## 🚀 Usage

1. Import your Netflix dataset into the `shows_movies.titles` and `shows_movies.credits` tables.
2. Open `Netflix_SQL_Analysis.sql` in your SQL client.
3. Run queries individually or as a batch.

---

## ⚠ Notes
- Queries use `shows_movies.` schema prefix; remove or adjust if your schema is different.
- Some queries rely on both IMDb and TMDB scores being non-null.
- `character` is a reserved keyword in some SQL engines — escape or rename if needed.

---

## 📌 Example Query

**Top 10 Movies by IMDb Score:**
```sql
SELECT title, type, imdb_score
FROM shows_movies.titles
WHERE imdb_score >= 8.0
  AND type = 'MOVIE'
ORDER BY imdb_score DESC
LIMIT 10;

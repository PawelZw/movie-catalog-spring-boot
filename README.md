# movie-catalog-spring-boot

🔥 CRUD type application using Java, MySQL, Docker, REST API, Spring Boot

💡 Technologies
  Java, MySQL, Docker, REST API, Spring Boot


 
# Description
An application that allows you to add records to the database, as well as read, update and delete. A MySQL relational database running in a Docker container was used.
We communicate with the database using an application made in Java using the Springboot framework


# Code


**Code snippet describing the Movie class, representing data fetched from the database:**
 
```
package pl.myapplication.moviecatalog;

import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;


@Data
@AllArgsConstructor
@NoArgsConstructor
public class Movie {

    private int id;
    private String title;
    private int rating;

```
The data retrieved from the database is:
- movie id
- Title of the movie
- movie rating





**Code snippet describing the MovieRepository class, responsible for communication with the database:**


 ```
package pl.myapplication.moviecatalog;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.BeanPropertyRowMapper;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.stereotype.Repository;
import java.util.List;

@Repository
public class MovieRepository {

    @Autowired
    JdbcTemplate jdbcTemplate;

    public List<Movie> getAll() {
        return jdbcTemplate.query("SELECT id, title, rating FROM movie",
                BeanPropertyRowMapper.newInstance(Movie.class));
    }


    public Movie getById(int id) {
        return jdbcTemplate.queryForObject("SELECT id, title, rating FROM movie WHERE " +
                "id = ?", BeanPropertyRowMapper.newInstance(Movie.class), id);
    }

    public int save(List<Movie> movies) {
        movies.forEach(movie -> jdbcTemplate
                .update("INSERT INTO movie(title, rating) VALUES(?, ?)",
                        movie.getTitle(), movie.getRating()
                ));

        return 1;
    }

    public int update(Movie movie) {
        return jdbcTemplate.update("UPDATE movie SET title=?, rating=? WHERE id=?",
                movie.getTitle(), movie.getRating(), movie.getId());
    }


    public int delete(int id) {
       return jdbcTemplate.update("DELETE FROM movie WHERE id=?", id);
    }
}
   
   ```

Conclusions:
 I wrote this code to increase my skills in using various technologies to build projects. In addition, the application is an example of using a relational database. 
 
 

🙋‍♂️ Feel free to contact me
Write sth nice ;) Find me on pawelzwolicki@gmail.com

 
👏 Thanks 

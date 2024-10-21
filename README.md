# React-Hooks-Checkpoint

Voici une structure de base pour votre application de cinéma en React, en utilisant des hooks pour gérer l'état et le filtrage.

1. Créez une application React
Si vous ne l'avez pas encore fait, créez une nouvelle application React :

bash
Copier le code
npx create-react-app cinema-app
cd cinema-app
2. Structure des fichiers
Organisez vos composants dans un dossier src/components :

css
Copier le code
src/
├── components/
│   ├── MovieCard.js
│   ├── MovieList.js
│   ├── Filter.js
│   └── AddMovieForm.js
└── App.js
3. Créez les composants
MovieCard.js

jsx
Copier le code
import React from 'react';

const MovieCard = ({ movie }) => {
  return (
    <div className="movie-card">
      <img src={movie.posterURL} alt={movie.title} />
      <h2>{movie.title}</h2>
      <p>{movie.description}</p>
      <p>Rating: {movie.rating}</p>
    </div>
  );
};

export default MovieCard;
MovieList.js

jsx
Copier le code
import React from 'react';
import MovieCard from './MovieCard';

const MovieList = ({ movies }) => {
  return (
    <div className="movie-list">
      {movies.map((movie, index) => (
        <MovieCard key={index} movie={movie} />
      ))}
    </div>
  );
};

export default MovieList;
Filter.js

jsx
Copier le code
import React from 'react';

const Filter = ({ titleFilter, setTitleFilter, ratingFilter, setRatingFilter }) => {
  return (
    <div className="filter">
      <input
        type="text"
        placeholder="Filter by title"
        value={titleFilter}
        onChange={(e) => setTitleFilter(e.target.value)}
      />
      <input
        type="number"
        placeholder="Filter by rating"
        value={ratingFilter}
        onChange={(e) => setRatingFilter(e.target.value)}
      />
    </div>
  );
};

export default Filter;
AddMovieForm.js

jsx
Copier le code
import React, { useState } from 'react';

const AddMovieForm = ({ addMovie }) => {
  const [title, setTitle] = useState('');
  const [description, setDescription] = useState('');
  const [posterURL, setPosterURL] = useState('');
  const [rating, setRating] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    addMovie({ title, description, posterURL, rating });
    setTitle('');
    setDescription('');
    setPosterURL('');
    setRating('');
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" placeholder="Title" value={title} onChange={(e) => setTitle(e.target.value)} required />
      <input type="text" placeholder="Description" value={description} onChange={(e) => setDescription(e.target.value)} required />
      <input type="text" placeholder="Poster URL" value={posterURL} onChange={(e) => setPosterURL(e.target.value)} required />
      <input type="number" placeholder="Rating" value={rating} onChange={(e) => setRating(e.target.value)} required />
      <button type="submit">Add Movie</button>
    </form>
  );
};

export default AddMovieForm;
4. Créez le composant principal
App.js

jsx
Copier le code
import React, { useState } from 'react';
import MovieList from './components/MovieList';
import Filter from './components/Filter';
import AddMovieForm from './components/AddMovieForm';

const App = () => {
  const [movies, setMovies] = useState([]);
  const [titleFilter, setTitleFilter] = useState('');
  const [ratingFilter, setRatingFilter] = useState('');

  const addMovie = (movie) => {
    setMovies([...movies, movie]);
  };

  const filteredMovies = movies.filter(movie =>
    movie.title.toLowerCase().includes(titleFilter.toLowerCase()) &&
    (ratingFilter === '' || movie.rating >= ratingFilter)
  );

  return (
    <div className="app">
      <h1>My Movie Collection</h1>
      <AddMovieForm addMovie={addMovie} />
      <Filter
        titleFilter={titleFilter}
        setTitleFilter={setTitleFilter}
        ratingFilter={ratingFilter}
        setRatingFilter={setRatingFilter}
      />
      <MovieList movies={filteredMovies} />
    </div>
  );
};

export default App;
5. Styles (Optionnel)
Vous pouvez ajouter des styles CSS pour améliorer l'apparence de votre application. Créez un fichier App.css et importez-le dans App.js.

6. Lancer l'application
Démarrez l'application avec :

bash
Copier le code
npm start
Voilà ! Vous avez une application de cinéma où vous pouvez ajouter des films, les afficher et les filtrer par titre et note. N'hésitez pas à l'améliorer en ajoutant des fonctionnalités supplémentaires ou en peaufinant le design !

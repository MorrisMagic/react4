import React from 'react';

function MovieCard({ title, description, posterURL, rating }) {
  return (
    <div style={{ border: "1px solid #ccc", padding: "16px", margin: "8px", width: "200px" }}>
      <img src={posterURL} alt={title} style={{ width: "100%" }} />
      <h3>{title}</h3>
      <p>{description}</p>
      <p>Rating: {rating}</p>
    </div>
  );
}

export default MovieCard;

import React from 'react';
import MovieCard from './MovieCard';

function MovieList({ movies }) {
  return (
    <div style={{ display: "flex", flexWrap: "wrap" }}>
      {movies.map((movie, index) => (
        <MovieCard key={index} {...movie} />
      ))}
    </div>
  );
}

export default MovieList;

import React from 'react';

function Filter({ setFilterTitle, setFilterRating }) {
  return (
    <div style={{ marginBottom: "16px" }}>
      <input
        type="text"
        placeholder="Filter by title"
        onChange={(e) => setFilterTitle(e.target.value)}
        style={{ marginRight: "8px", padding: "8px" }}
      />
      <input
        type="number"
        placeholder="Filter by rating"
        onChange={(e) => setFilterRating(e.target.value)}
        style={{ padding: "8px" }}
      />
    </div>
  );
}

export default Filter;


import React, { useState } from 'react';
import MovieList from './MovieList';
import Filter from './Filter';

function App() {
  const [movies, setMovies] = useState([
    {
      title: "Inception",
      description: "A skilled thief is offered a chance to erase his criminal history.",
      posterURL: "https://example.com/inception.jpg",
      rating: 5,
    },
    {
      title: "The Matrix",
      description: "A computer hacker learns about the true nature of reality.",
      posterURL: "https://example.com/matrix.jpg",
      rating: 4.5,
    },
  ]);

  const [filterTitle, setFilterTitle] = useState('');
  const [filterRating, setFilterRating] = useState('');

  const filteredMovies = movies.filter((movie) => 
    movie.title.toLowerCase().includes(filterTitle.toLowerCase()) &&
    movie.rating >= filterRating
  );

  const addMovie = (movie) => {
    setMovies([...movies, movie]);
  };

  return (
    <div style={{ padding: "16px" }}>
      <h1>My Movie App</h1>
      <Filter setFilterTitle={setFilterTitle} setFilterRating={setFilterRating} />
      <button onClick={() => addMovie({ title: "New Movie", description: "New Description", posterURL: "https://example.com/new.jpg", rating: 3 })}>
        Add New Movie
      </button>
      <MovieList movies={filteredMovies} />
    </div>
  );
}

export default App;


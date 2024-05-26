import React, { useState } from 'react';
import axios from 'axios';
import Autosuggest from 'react-autosuggest';
import Papa from 'papaparse';

const App: React.FC = () => {
  const [data, setData] = useState([]);
  const [value, setValue] = useState('');
  const [suggestions, setSuggestions] = useState([]);

  // Fetch car data from the CSV file when component mounts
  React.useEffect(() => {
    axios.get('/path/to/your/data.csv')
      .then(response => {
        Papa.parse(response.data, {
          header: true,
          complete: function(results) {
            setData(results.data);
          }
        });
      });
  }, []);

  // Teach Autosuggest how to calculate suggestions for any given input value.
  const getSuggestions = (value: string) => {
    const inputValue = value.trim().toLowerCase();
    const inputLength = inputValue.length;
    return inputLength === 0 ? [] : data.filter((car: any) =>
      car.model.toLowerCase().slice(0, inputLength) === inputValue
    );
  };

  // When suggestion is clicked, Autosuggest needs to populate the input field
  // based on the clicked suggestion.
  const getSuggestionValue = (suggestion: any) => suggestion.model;

  // Render a suggestion.
  const renderSuggestion = (suggestion: any) => (
    <div>
      {suggestion.model}
    </div>
  );

  const onChange = (event: any, { newValue }: any) => {
    setValue(newValue);
  };

  const onSuggestionsFetchRequested = ({ value }: any) => {
    setSuggestions(getSuggestions(value));
  };

  const onSuggestionsClearRequested = () => {
    setSuggestions([]);
  };

  const inputProps = {
    placeholder: 'Type a car model',
    value,
    onChange: onChange
  };

  return (
    <div>
      <Autosuggest
        suggestions={suggestions}
        onSuggestionsFetchRequested={onSuggestionsFetchRequested}
        onSuggestionsClearRequested={onSuggestionsClearRequested}
        getSuggestionValue={getSuggestionValue}
        renderSuggestion={renderSuggestion}
        inputProps={inputProps}
      />
      {/* Render the filtered cars here */}
    </div>
  );
};

export default App;

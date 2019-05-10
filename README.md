# AJAX-Type-Ahead

Simple type ahead suggestion feature using Fetch API to get an array of cities and Regular Expressions to filter the array

## Concepts Applied

Using Fetch API to get JSON data and populate array

```
const endpoint = 'https://gist.githubusercontent.com/Miserlou/c5cd8364bf9b2420bb29/raw/2bf258763cdddd704f8ffd3ea9a3e81d25e2c6f6/cities.json';
const places = [];

fetch(endpoint)
  .then(blob => blob.json())
  .then(json => places.push(...json));
```

Using Regular Expressions and String.prototype.match()
to filter the list of cities to those that contain the search string

```
function findMatches(searchString, places) {
  const regex = new RegExp(searchString, 'gi');
  return places.filter(place => {
    return place.city.match(regex) || place.state.match(regex)
  })
}
```

Using Array.Prototype.Map and Template Literals to iterate through the array of cities and create HTML in the DOM, also adds highlighting to each occurence of the search string

```
  const html = matchArray.map(place => {
    const regex = new RegExp(this.value, 'gi') // this.value is the search string
    const cityName = place.city.replace(regex, `<span class="hl">${this.value}</span>`);
    const stateName = place.state.replace(regex, `<span class="hl">${this.value}</span>`);
    return `
      <li>
        <span>${cityName}, ${stateName}</span>
        <span class="population">${numberWithCommas(place.population)}</span>
      </li>
    `;
  }).join('');
  suggestions.innerHTML = html;
```

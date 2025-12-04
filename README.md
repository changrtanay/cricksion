# Cricksion 

## Description

**Cricksion** is a web application that displays the list of ongoing cricket matches in real-time. The app fetches data from a cricket API to show information such as the match name and its status (e.g., Live, Completed). It allows users to easily check the current status of cricket matches happening across various leagues and tournaments.

## Screenshot
Here is a screenshot from the live demo:

![Screenshot](/screenshot.png)

## Features

- Display ongoing cricket matches.
- Fetch data in real-time using a cricket API (cricapi).
- Simple and responsive layout with minimal styling.
- List of live match details with match name and status.

## Tech Stack

- **HTML**: Structure of the webpage.
- **CSS**: Basic styling of the page to ensure responsiveness.
- **JavaScript**: Fetch API to retrieve live data about cricket matches.

## Setup and Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/changrtanay/cricksion.git
   ```
2. **Open the project**:
   Navigate to the project directory and open the `index.html` file in your web browser.

3. **API Key**:
   The application uses the `cricapi` service to fetch live match data. You must use your own API key for the app to work.

   To use the API:
   - Sign up for a free API key at [cricapi.com](https://www.cricapi.com/).
   - Replace the API key in the JavaScript code at:
   ```javascript
   const apiKey = "your_api_key";
   ```
   (Located inside the `script.js` file.)

## File Structure

- `index.html`: The main HTML file that contains the structure and links to external resources (CSS and JavaScript).
- `style.css`: The CSS file that provides the basic styles and ensures the page is responsive.
- `script.js`: The JavaScript file that fetches the data from the API and displays it on the page.

## Code Explanation

### HTML

The HTML file sets up the basic structure for displaying ongoing matches:

- The page has a title (`Cricksion`).
- The main body contains a paragraph (`p`) stating "Ongoing Cricket Matches" and an unordered list (`ul`) that will be populated with match data.

```html
<p>Ongoing Cricket Matches</p>
<ul>
  <li id="matches"></li>
</ul>
```

### CSS

The `style.css` file provides minimal styling for the application, ensuring a clean and responsive layout.

```css
body {
  min-width: 300px;
}
```

### JavaScript

The `script.js` file fetches data from the cricapi service:

- It uses `fetch` to get the match data from the API endpoint.
- The `getMatchData()` function processes the response and populates the list with match names and their statuses.
- If there are any ongoing matches, they are displayed on the page as list items.

```javascript
async function getMatchData() {
  return await fetch("https://api.cricapi.com/v1/currentMatches?apikey=your_api_key&offset=0")
    .then(data => data.json())
    .then(data => {
      if (data.status != "success") return;

      const matchesList = data.data;

      if (!matchesList) return [];

      const relevantData = matchesList.map(match => `${match.name}, ${match.status}`);
      
      document.getElementById("matches").innerHTML = relevantData.map(match => `<li>${match} </li>`).join('');
      
      return relevantData;
    })
    .catch(e => console.log(e));
}

getMatchData();
```

## Contributing

Feel free to fork the repository and create pull requests with improvements or bug fixes. Contributions are welcome!

## License

This project is open-source and available under the [MIT License](LICENSE).

## Acknowledgments

- [cricapi.com](https://www.cricapi.com/) for providing the cricket match data API.
- This project was built as a simple demonstration of how to fetch and display real-time data on a webpage.

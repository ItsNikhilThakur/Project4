# Project4
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>News Feed Layout</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="controls">
        <label for="columnCount">Columns: </label>
        <input type="range" id="columnCount" min="1" max="5" value="3">
        <label for="columnGap">Gap: </label>
        <input type="range" id="columnGap" min="10" max="50" value="20">
        <label for="columnWidth">Width: </label>
        <input type="range" id="columnWidth" min="100" max="300" value="200">
    </div>

    <button id="themeToggle">Toggle Theme</button>

    <div class="news-feed">
        <article>Article 1...</article>
        <article>Article 2...</article>
        <!-- Articles will be dynamically added -->
    </div>

    <script src="script.js"></script>
</body>
</html>






/* Base styles */
body {
    font-family: Arial, sans-serif;
    background-color: var(--bg-color, white);
    color: var(--text-color, black);
    margin: 0;
    padding: 0;
}

.controls {
    margin: 20px;
    padding: 10px;
}

label {
    margin-right: 10px;
}

input[type="range"] {
    margin-right: 20px;
}

button {
    padding: 10px 20px;
    margin: 20px;
    cursor: pointer;
}

/* Default column layout */
.news-feed {
    column-count: 3; /* Number of columns */
    column-gap: 20px; /* Gap between columns */
    column-width: 200px; /* Width of each column */
    max-width: 1200px; /* Maximum width of the container */
    margin: 0 auto; /* Center the container */
}

/* Shorthand (for all three properties) */
.news-feed-shorthand {
    columns: 3 200px; /* 3 columns, 200px column width */
    column-gap: 20px;
}

/* Print styles for better readability */
@media print {
    .news-feed {
        column-count: 1; /* Single column when printed */
        column-gap: 0;
    }
}

/* Media query for responsive design */
@media (max-width: 768px) {
    .news-feed {
        column-count: 1; /* Single column for mobile */
    }
}

/* Dark theme styles */
.dark-theme {
    --bg-color: black;
    --text-color: white;
}







// Get elements
const columnCount = document.getElementById('columnCount');
const columnGap = document.getElementById('columnGap');
const columnWidth = document.getElementById('columnWidth');
const newsFeed = document.querySelector('.news-feed');
const themeToggleButton = document.getElementById('themeToggle');

// Update feed layout based on user input
columnCount.addEventListener('input', updateLayout);
columnGap.addEventListener('input', updateLayout);
columnWidth.addEventListener('input', updateLayout);

// Function to update the layout dynamically
function updateLayout() {
    const columns = columnCount.value;
    const gap = columnGap.value + "px";
    const width = columnWidth.value + "px";

    // Apply the changes dynamically to the feed
    newsFeed.style.columnCount = columns;
    newsFeed.style.columnGap = gap;
    newsFeed.style.columnWidth = width;

    // Save the preferences in localStorage
    savePreferences();
}

// Function to save preferences to localStorage
function savePreferences() {
    localStorage.setItem('columnCount', columnCount.value);
    localStorage.setItem('columnGap', columnGap.value);
    localStorage.setItem('columnWidth', columnWidth.value);
}

// Function to load preferences from localStorage
function loadPreferences() {
    if (localStorage.getItem('columnCount')) {
        columnCount.value = localStorage.getItem('columnCount');
        columnGap.value = localStorage.getItem('columnGap');
        columnWidth.value = localStorage.getItem('columnWidth');
        updateLayout(); // Apply saved preferences
    }
}

// Load preferences when the page loads
loadPreferences();

// Add a new article to the feed (simulate live updates)
function addArticle() {
    const newArticle = document.createElement('article');
    newArticle.textContent = `Article ${document.querySelectorAll('article').length + 1}`;
    newsFeed.appendChild(newArticle);
}

// Add a new article every 5 seconds
setInterval(addArticle, 5000);

// Theme toggle functionality
themeToggleButton.addEventListener('click', () => {
    document.body.classList.toggle('dark-theme');
});

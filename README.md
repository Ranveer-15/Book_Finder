Hosted Link: https://ranveer-15.github.io/Book_Finder/
📖 About This Project
Book Finder is a web application that allows users to: ✅ View book categories dynamically 📂 ✅ Search for best-selling books 📚 ✅ Click on a category to filter books 🔍 ✅ Display top books with "Show More" functionality ✨
It fetches real-time book data from an API and displays it dynamically using JavaScript DOM manipulation.

🛠️ Technologies Used
* HTML - Page structure
* CSS - Styling and layout
* JavaScript (ES6+) - API calls, event handling, and DOM manipulation
* Fetch API - To retrieve book data from an external API

⚡ JavaScript Functionality Used
🔗 1. Fetching Data from an API
* The app fetches book categories and best-selling books from external APIs.
* getData(url) is a reusable function to fetch and return JSON data from a given URL.

async function getData(url) {
  const response = await fetch(url);
  const result = await response.json();
  return result;
}

📂 2. Fetching & Displaying Book Categories
* The getCategories(CATEGORY_API) function fetches book categories and calls displayCategories() to show them.
* Each category is clickable, and clicking it filters books.

function displayCategories(arr) {
  const fragment = document.createDocumentFragment();
  
  arr.forEach((obj) => {
    const category = document.createElement("p");
    category.innerText = obj.list_name;

    category.addEventListener("click", (e) => {
      booksContainer.innerHTML = ""; // Clear previous results
      let categoryBooksObject = books.find((obj) => e.target.innerText === obj.list_name);
      displayBooks(categoryBooksObject.books);
    });

    fragment.append(category);
  });
  categoryContainer.append(fragment);
}

📚 3. Fetching & Displaying Top Books
* The getAllBooks(TOPBOOKS_API) function fetches all books and displays the first 3 books from each category.

async function getAllBooks(url) {
  const data = await getData(url);
  books = data;

  booksContainer.append("BEST SELLER BOOKS");
  data.forEach((obj) => {
    let fewBooks = obj.books.slice(0, 3); // Get first 3 books
    displayBooks(fewBooks);
  });
}

🖼️ 4. Displaying Books in the UI
* Books are displayed dynamically using DOM manipulation.
* Each book has an image, title, and author name.

function displayBooks(arr) {
  const parentDiv = document.createElement("div");
  parentDiv.classList.add("parent-div");

  const heading = document.createElement("h2");
  heading.innerText = arr[0].list_name;
  parentDiv.append(heading);

  const innerBooksDiv = document.createElement("div");
  innerBooksDiv.classList.add("inner-books-div");

  arr.forEach((obj) => {
    const bookDiv = document.createElement("div");
    bookDiv.classList.add("book-div");

    const image = document.createElement("img");
    image.src = obj.book_image;

    const title = document.createElement("p");
    title.innerText = obj.title;

    const author = document.createElement("p");
    author.innerText = obj.author;

    bookDiv.append(image, title, author);
    innerBooksDiv.append(bookDiv);
  });

  parentDiv.append(innerBooksDiv);

  const showMoreButton = document.createElement("button");
  showMoreButton.innerText = "Show More";
  showMoreButton.classList.add("show-more");

  parentDiv.append(showMoreButton);
  booksContainer.append(parentDiv);
}

🎯 5. Handling "All Categories" Click
* Clicking on "All Categories" resets the book list to all best-seller books.

allCategories.addEventListener("click", ()=> {
  booksContainer.innerHTML = ""; 
  getAllBooks(TOPBOOKS_API);
});

🚀 How It Works
1. Fetches book categories from an API and displays them.
2. Fetches the top best-selling books and displays the first 3 books from each category.
3. Clicking on a category filters books from that category.
4. Clicking "All Categories" resets the book list.


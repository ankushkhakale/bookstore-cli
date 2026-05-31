# 📚 Book Store CLI

A lightweight, elegant command-line interface for managing your personal book collection. Built with **Go**, this project demonstrates practical use of Go's powerful standard library to create a user-friendly tool for book inventory management.

## 🎯 Project Overview

**BookStore CLI** is a straightforward yet effective solution for organizing and managing book metadata through the command line. Whether you're curating a personal library, maintaining a bookstore inventory, or simply exploring Go programming, this tool provides an intuitive interface to perform all essential CRUD (Create, Read, Update, Delete) operations on book records.

The project showcases fundamental Go concepts including:
- **Flag parsing** for command-line arguments
- **JSON marshaling/unmarshaling** for data persistence
- **File I/O operations** for working with persistent storage
- **Struct definitions** for type safety
- **Basic error handling** patterns
- **CLI design patterns** for creating user-friendly command interfaces

## ✨ Features

- **📖 View Books**: Display all books in your collection or search for a specific book by ID
- **➕ Add Books**: Quickly add new books to your inventory with all relevant details
- **✏️ Update Books**: Modify existing book information whenever details change
- **🗑️ Delete Books**: Remove books from your collection with a simple command
- **📄 JSON Storage**: All data is persistently stored in a JSON file for easy access and portability
- **🖥️ Intuitive CLI**: Clean, command-based interface that's easy to learn and use

## 🚀 Getting Started

### Prerequisites

- **Go 1.17 or higher** installed on your system
- Basic familiarity with command-line interfaces

### Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/ankushkhakale/bookstore-cli.git
   cd bookstore-cli
   ```

2. **Build the application**:
   ```bash
   go build -o bookstore
   ```

   This will create an executable named `bookstore` (or `bookstore.exe` on Windows) in your current directory.

3. **Verify the installation**:
   ```bash
   ./bookstore
   ```
   
   You should see a message prompting you to provide a valid command.

## 📖 Usage Guide

### Understanding Commands

The BookStore CLI operates on a command-based system. The general syntax is:

```
./bookstore <command> [flags]
```

### Available Commands

#### 1. **GET - Retrieve Books**

View books from your collection.

**Get All Books:**
```bash
./bookstore get --all
```

This displays all books in your library in a formatted table with columns: ID, Title, Author, Price, and ImageURL.

**Get a Specific Book by ID:**
```bash
./bookstore get --id 1
```

Returns details for the book with ID "1". Useful when you need information about a specific title.

**Example Output:**
```
Id 	 Title 	                                      Author 	         Price 	 ImageURL
1 	 How to Win Friends and Influence People  Dale Carnegie    600 	 https://images-na.ssl-images-amazon.com/...
```

---

#### 2. **ADD - Add New Books**

Add a new book to your collection with the following fields:

```bash
./bookstore add \
  --id 6 \
  --title "Your Book Title" \
  --author "Author Name" \
  --price "999" \
  --image_url "https://example.com/book-cover.jpg"
```

**Parameters:**
- `--id`: Unique identifier for the book (string, required)
- `--title`: Book title (string, required)
- `--author`: Author name (string, required)
- `--price`: Book price (string, required)
- `--image_url`: URL to the book's cover image (string, required)

**Important Note:** All parameters are required. If any field is missing, the command will fail with an error message.

**Example:**
```bash
./bookstore add --id 6 --title "Clean Code" --author "Robert C. Martin" --price "500" --image_url "https://example.com/clean-code.jpg"
```

Output on success:
```
Book added successfully
```

---

#### 3. **UPDATE - Modify Existing Books**

Update information for an existing book. The book must already exist in your collection (identified by ID).

```bash
./bookstore update \
  --id 6 \
  --title "Updated Title" \
  --author "Updated Author" \
  --price "1000" \
  --image_url "https://example.com/updated-cover.jpg"
```

**Parameters:** Same as ADD command (all required).

**Example:**
```bash
./bookstore update --id 6 --title "Clean Code (Revised)" --author "Robert C. Martin" --price "550" --image_url "https://example.com/clean-code-revised.jpg"
```

Output on success:
```
Book added successfully
```

**Note:** The command will fail if you try to update a book ID that doesn't exist in your collection.

---

#### 4. **DELETE - Remove Books**

Delete a book from your collection by its ID.

```bash
./bookstore delete --id 6
```

**Parameters:**
- `--id`: ID of the book to remove (string, required)

**Example:**
```bash
./bookstore delete --id 5
```

Output on success:
```
Book deleted successfully
```

**Error Handling:** If you attempt to delete a book with an ID that doesn't exist, you'll receive an error message: "Book not found".

---

## 📁 Project Structure

```
bookstore-cli/
├── main.go           # Entry point and CLI command definitions
├── books.go          # Core business logic for CRUD operations
├── books.json        # JSON file storing all book data (persistent storage)
├── go.mod            # Go module definition
├── bookstore         # Compiled executable
└── README.md         # This file
```

### File Descriptions

- **main.go**: Defines the CLI structure using Go's `flag` package. Sets up command parsing and routes commands to appropriate handlers.
- **books.go**: Contains the core logic for:
  - Reading books from `books.json`
  - Saving books to `books.json`
  - Handling GET, ADD, UPDATE, and DELETE operations
  - Error checking and validation

- **books.json**: A JSON array containing all book records. Each record includes: id, title, author, price, and image_url.

## 📊 Data Model

Each book in the collection is represented by the following structure:

```go
type Book struct {
    Id       string `json:"id"`
    Title    string `json:"title"`
    Author   string `json:"author"`
    Price    string `json:"price"`
    Imageurl string `json:"image_url"`
}
```

All fields are stored as strings for simplicity and flexibility.

## 🧪 Sample Data

The project comes with sample books pre-loaded in `books.json`:

1. **"How to Win Friends and Influence People"** by Dale Carnegie - ₹600
2. **"Think and Grow Rich"** by Napoleon Hill - ₹500
3. **"The 7 Habits of Highly Effective People"** by Stephen R. Covey - ₹700
4. **"Atomic Habits"** by James Clear - ₹300
5. **"The 4-Hour Work Week"** by Tim Ferris - ₹4000

Feel free to modify, delete, or add to these entries using the CLI commands!

## 💡 Learning Outcomes & Go Concepts

This project is an excellent introduction to practical Go programming. Here's what you'll learn:

### 1. **Flag Parsing**
The project demonstrates how to parse command-line flags using Go's `flag` package:
- Creating separate flagsets for different commands
- Defining string and boolean flags
- Parsing and validation

### 2. **JSON Handling**
Working with JSON in Go:
- Marshaling Go structs to JSON (`json.Marshal`)
- Unmarshaling JSON to Go structs (`json.Unmarshal`)
- Struct tags for JSON field mapping (`json:"fieldname"`)

### 3. **File I/O**
Reading and writing files:
- `ioutil.ReadFile()` for reading file contents
- `ioutil.WriteFile()` for writing data to files
- File permission handling (0644)

### 4. **Error Handling**
Go's approach to error handling:
- Returning errors as values
- Error checking and propagation
- Creating user-friendly error messages

### 5. **CLI Design Patterns**
Building effective command-line tools:
- Command-subcommand patterns
- Required vs optional parameters
- User guidance through error messages and usage help

## 🔧 How It Works

### Adding a Book - Step by Step

1. User runs: `./bookstore add --id 6 --title "New Book" --author "Someone" --price "500" --image_url "http://url.com/image.jpg"`
2. The CLI parses the `add` command and extracts the flags
3. `handleAddBook()` is called with the parameters
4. The function validates that all required fields are provided
5. Current books are loaded from `books.json` using `getBooks()`
6. A new `Book` struct is created with the provided data
7. The new book is appended to the books slice
8. All books (including the new one) are saved back to `books.json` using `saveBooks()`
9. Success message is displayed to the user

### Updating a Book - Step by Step

1. User runs: `./bookstore update --id 6 --title "Updated Title" ...`
2. Current books are loaded from `books.json`
3. The function iterates through all books to find one with matching ID
4. When found, the book's data is replaced with new values
5. All books are saved back to `books.json`
6. If no matching ID is found, an error is displayed

### Deleting a Book - Step by Step

1. User runs: `./bookstore delete --id 6`
2. Current books are loaded from `books.json`
3. The function searches for a book with the specified ID
4. When found, the book is removed from the slice using slice operations
5. Remaining books are saved back to `books.json`
6. If no matching ID is found, an error is displayed

## 🎓 Why This Project Matters

This project serves as an excellent learning foundation because it:

- **Combines multiple Go concepts** in a real-world scenario
- **Is simple enough to understand** yet complex enough to teach valuable patterns
- **Demonstrates persistent data storage** with JSON files
- **Shows proper error handling** practices
- **Uses idiomatic Go patterns** for CLI applications
- **Provides a practical tool** you can actually use

## 🚀 Possible Enhancements

If you want to extend this project, consider:

- Add **search functionality** (search by title, author, or genre)
- Implement **categories or tags** for book organization
- Add **rating and review** system
- Create a **REST API** to serve the book data
- Build a **web interface** using Go's `net/http` package
- Add **configuration file support** for customization
- Implement **database storage** (SQLite, PostgreSQL, etc.)
- Create **export functionality** (CSV, PDF formats)

## 🤝 Contributing

This is a learning project. If you'd like to improve it or add features:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## 📝 License

This project is provided as-is for educational purposes.

## 🎯 Takeaway

The **BookStore CLI** is more than just a tool—it's a practical playground for learning Go. It demonstrates that you don't need complex frameworks or libraries to build something useful. With just Go's standard library, you can create clean, functional command-line applications that solve real problems.

Happy coding! 📚
# Book-project
This project uses OOP 

# Define the Book class
class Book:
    def __init__(self, title, author, isbn=None, ariel=None): 
        self.title = title
        self.author = author
        self.isbn = isbn
        self.ariel = ariel
        self.borrowed = False

    def check_out(self):
        if not self.borrowed:
            self.borrowed = True
            return True
        return False

    def return_book(self):
        self.borrowed = False

    def __str__(self):
        id_string = ""
        if self.isbn:
            id_string += f"ISBN: {self.isbn}"
        if self.ariel:
            if id_string: 
                id_string += ", "
            id_string += f"Ariel: {self.ariel}"
        if not id_string:
            id_string = "No identifier"
            
        return f"{self.title} by {self.author}. Identifiers: {id_string}"

# Define the Patron class
class Patron:
    def __init__(self, name):
        self.name = name
        self.borrowed_books = []

    def borrow_book(self, book):
        if book.check_out():
            self.borrowed_books.append(book)
            print(f"{self.name} has borrowed {book.title}")
        else:
            print(f"{book.title} is currently not available.")

    def return_book(self, book):
        if book in self.borrowed_books:
            book.return_book()
            self.borrowed_books.remove(book)
            print(f"{self.name} has returned {book.title}")
        else:
            print(f"{self.name} does not have {book.title}.")

    def list_borrowed_books(self):
        for book in self.borrowed_books:
            print(book)

    def __str__(self):
        return f"Patron: {self.name}, Books Borrowed: {len(self.borrowed_books)}"


# Define the Library class
class Library:
    def __init__(self):
        self.books = []
        self.patrons = []

    def add_book(self, book):
        self.books.append(book)

    def add_patron(self, patron):
        self.patrons.append(patron)

    def find_book(self, title):
        for book in self.books:
            if book.title == title:
                return book
        return None

    def find_patron(self, name):
        for patron in self.patrons:
            if patron.name == name:
                return patron
        return None

    def __str__(self):
        return f"Library has {len(self.books)} books and {len(self.patrons)} patrons."


# Example usage
def main():
    # Create a library instance
    my_library = Library()

    # Create some books
    book1 = Book("The Great Gatsby", "F. Scott Fitzgerald", "123456789")
    book2 = Book("1984", "George Orwell", "987654321")
    book3 = Book("Cricket In Times Square", "George Seldon", ariel="AR0001")

    # Add books to the library
    my_library.add_book(book1)
    my_library.add_book(book2)
    my_library.add_book(book3)

    # Create a patron
    john_doe = Patron("John Doe")

    # Add patron to the library
    my_library.add_patron(john_doe)

    # Patron borrows a book
    john_doe.borrow_book(book1)
    john_doe.borrow_book(book3)

    # List borrowed books
    john_doe.list_borrowed_books()

    # Patron returns a book
    john_doe.return_book(book1)

    # Print the library status
    print(my_library)

if __name__ == "__main__":
    main()

# Library-management-database-
import psycopg2

# Connect to PostgreSQL
conn = psycopg2.connect(
    database="library management system",
    user="postgres",
    password="your_password",
    host="localhost",
    port="5432"
)

cursor = conn.cursor()

# Add Book
def add_book(title, author):
    cursor.execute(
        "INSERT INTO books (title, author) VALUES (%s, %s)",
        (title, author)
    )
    conn.commit()
    print("Book added successfully!")

# View Books
def view_books():
    cursor.execute("SELECT * FROM books")
    rows = cursor.fetchall()
    for row in rows:
        print(row)

# Issue Book
def issue_book(book_id):
    cursor.execute(
        "UPDATE books SET available = FALSE WHERE book_id = %s",
        (book_id,)
    )
    conn.commit()
    print("Book issued!")

# Return Book
def return_book(book_id):
    cursor.execute(
        "UPDATE books SET available = TRUE WHERE book_id = %s",
        (book_id,)
    )
    conn.commit()
    print("Book returned!")

# Menu
while True:
    print("\n1.Add Book\n2.View Books\n3.Issue Book\n4.Return Book\n5.Exit")
    choice = input("Enter choice: ")

    if choice == '1':
        title = input("Enter title: ")
        author = input("Enter author: ")
        add_book(title, author)

    elif choice == '2':
        view_books()

    elif choice == '3':
        book_id = int(input("Enter book ID: "))
        issue_book(book_id)

    elif choice == '4':
        book_id = int(input("Enter book ID: "))
        return_book(book_id)

    elif choice == '5':
        break

cursor.close()
conn.close()

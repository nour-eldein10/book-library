using System;
using System.Collections.Generic;

namespace BookShopTest
{
    public class Book
    {
        private static List<Book> booksList = new List<Book>();

        private string name;
        private double price;
        private string author;

        public Book() { }

        public Book(string name, double price, string author)
        {
            this.name = name;
            this.price = price;
            this.author = author;
        }

        public string Name
        {
            get { return name; }
            set { name = value; }
        }

        public double Price
        {
            get { return price; }
            set { price = value; }
        }

        public string Author
        {
            get { return author; }
            set { author = value; }
        }

        public static void DisplayAllBook()
        {
            List<Book> listBook = booksList;
            if (listBook.Count == 0)
            {
                Console.WriteLine("There is no data !!");
            }
            else
            {
                Console.WriteLine("Name            Author                    Price");
                foreach (Book book in listBook)
                {
                    Console.WriteLine($"{book.Name}            {book.Author}                  {book.Price}");
                }
            }
        }

        public static void AddBooks()
        {
            Console.WriteLine("Enter The Count of book : ");
            int countBook = int.Parse(Console.ReadLine());
            if (countBook < 0)
            {
                Console.WriteLine("Not Valid, the count must be > 0");
            }
            else
            {
                for (int i = 0; i < countBook; i++)
                {
                    Console.WriteLine($"Enter Book {i + 1} name");
                    string nameBook = Console.ReadLine();
                    Console.WriteLine($"Enter Book {i + 1} author");
                    string authorBook = Console.ReadLine();
                    Console.WriteLine($"Enter Book {i + 1} price");
                    double priceBook = double.Parse(Console.ReadLine());

                    Book b = new Book(nameBook, priceBook, authorBook);

                    booksList.Add(b);
                }
            }
        }

        public static Book GetBookByName(string name)
        {
            foreach (Book book in booksList)
            {
                if (book.Name.Equals(name))
                {
                    return book;
                }
            }

            return null;
        }

        public static bool UpdateBook(Book newBook, Book oldBook)
        {
            if (booksList.Count > 0)
            {
                int index = -1;
                for (int i = 0; i < booksList.Count; i++)
                {
                    if (booksList[i].Name.Equals(oldBook.Name))
                    {
                        index = i;
                        break;
                    }
                }

                if (index != -1)
                {
                    booksList[index].Name = newBook.Name;
                    booksList[index].Author = newBook.Author;
                    booksList[index].Price = newBook.Price;

                    return true;
                }
            }

            return false;
        }

        public static bool DeleteBook(Book book)
        {
            if (booksList.Count > 0)
            {
                booksList.Remove(book);
                return true;
            }

            return false;
        }

        public static void DeleteBook2()
        {
            Console.WriteLine("Enter Name Book ");
            string bookName = Console.ReadLine();
            Book book = GetBookByName(bookName);
            if (book == null)
            {
                Console.WriteLine("No book founded !! ");
            }
            else
            {
                //delete
                if (DeleteBook(book))
                {
                    Console.WriteLine("deleted successfuly");
                }
                else
                {
                    Console.WriteLine("deleted fails");
                }
            }
        }

        public static void UpdateBooks()
        {
            bool isMenu = true;
            while (isMenu)
            {
                Console.WriteLine("----Update Menu----");
                Console.WriteLine("1- Update Book Name");
                Console.WriteLine("2- Update Book Author");
                Console.WriteLine("3- Update Book price");
                Console.WriteLine("4- Back To Main Menu");
                Console.WriteLine("5- Exit");
                Console.WriteLine("Enter your choice: ");

                int choiceNumber1 = int.Parse(Console.ReadLine());
                switch (choiceNumber1)
                {
                    case 1:
                        Console.WriteLine("Enter book name : ");
                        string bookName = Console.ReadLine();
                        Book oldBook = GetBookByName(bookName);
                        Book newBook = GetBookByName(bookName);
                        if (oldBook == null)
                        {
                            Console.WriteLine("No book with this name !!");
                        }
                        else
                        {
                            Console.WriteLine("Enter book new name : ");
                            string newName = Console.ReadLine();

                            newBook.Name = newName;
                            if (UpdateBook(newBook, oldBook))
                            {
                                Console.WriteLine("updated successfluty");
                            }
                            else
                            {
                                Console.WriteLine("updated fails");
                            }
                        }

                        break;

                    case 2:
                        Console.WriteLine("Enter book name : ");
                        string bookName1 = Console.ReadLine();
                        Book oldBook1 = GetBookByName(bookName1);
                        Book newBook1 = GetBookByName(bookName1);
                        if (oldBook1 == null)
                        {
                            Console.WriteLine("No book with this name !!");
                        }
                        else
                        {
                            Console.WriteLine("Enter book new author : ");
                            string newAuthor = Console.ReadLine();

                            newBook1.Author = newAuthor;
                            if (UpdateBook(newBook1, oldBook1))
                            {
                                Console.WriteLine("updated successfluty");
                            }
                            else
                            {
                                Console.WriteLine("updated fails");
                            }
                        }

                        break;

                    case 4:
                        isMenu = false;

                        break;
                    case 5:
                        Environment.Exit(0);
                        break;
                }
            }
        }
    }

    public class BookShopTest
    {
        public static void ExistFromApp()
        {
            Environment.Exit(0);
        }

        static void Main(string[] args)
        {
            bool isMenu = true;
            while (isMenu)
            {
                Console.WriteLine("----Main Menu----");
                Console.WriteLine("1- Display All Books");
                Console.WriteLine("2- Add Books");
                Console.WriteLine("3- Update Books");
                Console.WriteLine("4- Delete Book");
                Console.WriteLine("5- Exit");
                Console.WriteLine("Enter your choice: ");

                int choiceNumber = int.Parse(Console.ReadLine());
                switch (choiceNumber)
                {
                    case 1:
                        Book.DisplayAllBook();
                        break;

                    case 2:
                        Book.AddBooks();
                        break;

                    case 3:
                        Book.UpdateBooks();
                        break;

                    case 4:
                        Book.DeleteBook2();
                        break;

                    case 5:
                        ExistFromApp();
                        break;
                }
            }
        }
    }
}

import java.util.*;
import java.util.Scanner;
import java.util.Map;
import java.util.List;
import java.util.HashMap;
class Author {
    private String name;
    private String email;

    public Author(String name, String email){
        this.name = name;
        this.email = email;
    }

    public String getName(){
        return name;

    }
    public String getemail(){
        return email;

    }

}
class Book{
    private String id;
    private String title;
    private Author author;
    private int numberofcopies;
public Book(String id, String title,Author author, int numberofcopies){
    this.id =id;
    this.title = title;
    this.author =author;
    this.numberofcopies = numberofcopies;
    }


public String getId(){
    return id;
}
public String gettitle(){
    return title;
    }
public Author getAuthor(){
    return author;
    }
public int getNumberofcopies(){
    return numberofcopies;
    }
public void setNumberofcopies(int numberofcopies){
    this.numberofcopies = numberofcopies;
  }
}
class Bookstore{
private Map<String,Book> books;


  public Bookstore(){
     books = new HashMap();

    }
  public void addBook(Book book){
      books.put(book.getId(), book);
    }
  public void removeBook(String bookId){
      books.remove(bookId);
    }
public Book getBook(String bookId){
    return books.get(bookId);
}
public List<Book> getAllBooks(){
    return new ArrayList(books.values());
    }
}
class AuthorManager{
private Map<String,Author> authors;


  public AuthorManager(){
      authors = new HashMap();

    }
  public void addAuthor( Author  author){
      authors.put(author.getName(), author);
    }
  public void removeAuthor(String  authorName){
       authors.remove( authorName);
    }
public Author getAuthor(String  authorName){
    return  authors.get( authorName);}
public List< Author> getAllauthors(){
    return new ArrayList( authors.values());
    }
}
public class BookManagement {

    
    private Bookstore bookstore;
    private AuthorManager authorManager;
   


    public void  BookShopManagement(){
        bookstore = new Bookstore();
        authorManager = new AuthorManager();
    }

    public void controlpanel(){
        System.out.println( " \t \t \t control panel");
        System.out.println( " \t \t \t username ");
        System.out.println( " \t \t \t password");
        System.out.println( " \t \t \t incorrect password");
        System.out.println( " \t \t \t username");
        System.out.println( " \t \t \t password");
        System.out.println( " \t \t \t Welcome to book shop");
        System.out.println( " \t \t \t Book shop management");
        System.out.println( " \t \t \t group member: foriengehan,diwand khan");
        System.out.println( " \t \t \t Roll  numrber: 71-kk-34    ,  31-cp-100");
        System.out.println( " 1.ADD Book");
        System.out.println( " 2.Display book");
        System.out.println( " 3.check particular book");
        System.out.println( " 4.update book");
        System.out.println( " 5.delete book");
        System.out.println( " 6.Add author");
        System.out.println( " 7.Display button");
        System.out.println( " 8.Exit");
    }

    public void addBook(){
        Scanner scanner = new Scanner(System.in);
        System.out.println( " \n\t\t\t ADD BOOKS");
        System.out.println( "  Book Id");
        String bookId = scanner.nextLine();
        System.out.println( "  Book title");
         String Booktitle = scanner.nextLine();
         System.out.println( "Author Name");
         String AuthorName = scanner.nextLine();
         System.out.println( " Author email");
         String Authoremail = scanner.nextLine();
       System.out.println( " No OF Books");
         int  numberofcopies = scanner.nextInt();
        scanner.nextLine();

      Author author = authorManager.getAuthor(AuthorName);
      if(author == null){
          author = new Author(AuthorName,Authoremail);
          authorManager.addAuthor(author);
      }

     Book book = new Book(bookId,Booktitle,author,numberofcopies);
     bookstore.addBook(book);
    }

    public void showbook(){
        System.out.println( " \t \t \t  ALL Book ");
        
List<Book> books = bookstore.getAllBooks();
for(Book book :books){
    System.out.println( "  Book Id " + book.getId());
    System.out.println( "  Book title" + book.gettitle());
    System.out.println( " Author Name"+ book.getAuthor().getName());
    System.out.println( "  Author email" + book.getAuthor().getemail());
    System.out.println( "   No OF Books" + book.getNumberofcopies());
    System.out.println();
        }
if (books.isEmpty()){
    System.out.println("no book found");
        }
    }
public void checkbook(){
     Scanner scanner = new Scanner(System.in);
    System.out.println("\t\t\t check particular book");
    System.out.println("book Id");
    String BookId = scanner.nextLine();
    Book book = bookstore.getBook(BookId);
    if(book != null){
        System.out.println( "  Book Id " + book.getId());

    System.out.println( "  Book title" + book.gettitle());
    System.out.println( " Author Name"+ book.getAuthor().getName());
    System.out.println( "  Author email" + book.getAuthor().getemail());
    System.out.println( "   No OF Books" + book.getNumberofcopies());
    System.out.println();
        }
 else{

        System.out.println("book Id not found");
    }
    }
    
public void updatebook(){
    Scanner scanner = new Scanner(System.in);
    System.out.println("update book record");
    System.out.println("book Id");
    String BookId = scanner.nextLine();
    Book book = bookstore.getBook(BookId);
    if(book != null){
        System.out.println("new book title");
         String newTitle = scanner.nextLine();
         System.out.println("new Author name");
          String newAuthorName= scanner.nextLine();
          System.out.println("new new Autho email");
           String newAuthoremail = scanner.nextLine();
           System.out.println("new no of nbook");
            int newNumberofcopies = scanner.nextInt();
            scanner.nextLine();
            Author author = authorManager.getAuthor(newAuthorName);
      if(author == null){
          author = new Author(newAuthorName,newAuthoremail);
          authorManager.addAuthor(author);
        }
            book.setNumberofcopies(newNumberofcopies);
            System.out.println("book update successfully");
    } else {
            System.out.println("book Id not found");
            }
    }

      public void deleteBook(){
          Scanner scanner = new Scanner(System.in);
    System.out.println("\n\n\t\tdelete a book");
    System.out.println("book Id");
    String BookId = scanner.nextLine();
     Book book = bookstore.getBook(BookId);
    if(book != null){
        bookstore.removeBook(BookId);
        System.out.println(" book is deleted successfully.. ");
          }
 else{
         System.out.println(" bookId not found ");
          }
    }
      public void addAuthor(){
          Scanner scanner = new Scanner(System.in);
    System.out.println("\t\t\t ADD AUTHORS ");
    System.out.println("author Name");
    String authorName = scanner.nextLine();
            System.out.println("author email");
    String authoremail= scanner.nextLine();
     Author author = new Author(authorName,authoremail);
          authorManager.addAuthor(author);
    }
      public void showauthor(){
           System.out.println("ALL AUTHORS");
           List<Author> authors = authorManager.getAllauthors();
for(Author author : authors){
    System.out.println( "  AuthorName" + author.getName());
    System.out.println( "  Authoremail" + author.getemail());
    System.out.println( );
          }
if(authors.isEmpty()){
    System.out.println("no author found" );
          }
    }

      public void run(){
          Scanner scanner = new Scanner(System.in);
          int choice;
          do
          {
               controlpanel();
               System.out.println("Enter your choice(1-8)");
               choice = scanner.nextInt();
               scanner.nextLine();
               switch(choice){
                   case 1:
                       addBook();
                       break;
                   case 2:
                        showbook();
                       break;
                  case 3:
                       checkbook();
                       break;
                  case 4:
                       updatebook();
                       break;
                  case 5:
                       deleteBook();
                       break;
                   case 6:
                       addAuthor();
                       break;
                   case 7:
                       showauthor();
                       break;
                   case 8:
                    System.out.println("Thank you for using  the book management system");
                       break;
                   default:
                       System.out.println("\n invalid choice,please try again");
              }
          }

           while (choice != 8);
    }
      public static void main(String [] args){
          BookManagement  bookshopmanagment = new BookManagement();
          bookshopmanagment.run();
    }
}
    















               








           

    
    
    









    









































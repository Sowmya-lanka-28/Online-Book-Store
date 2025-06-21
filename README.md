# Online-Book-Store
public class Book 
{
 int id;
 String title;
 String author;
 double price;
public Book(int id, String title, String author, double price) {
	super();
	this.id = id;
	this.title = title;
	this.author = author;
	this.price = price;
}
 
 public void dispaly()
 {
	 System.out.println(id+" | "+title+" | "+author+" | $ "+price);
	 
 }
 }


 
 import java.util.ArrayList;
import java.util.Scanner;

public class BookStore 
{

	    static ArrayList<Book> bookList = new ArrayList<>();
	    static Cart cart = new Cart();
	    static Scanner sc = new Scanner(System.in);

	    public static void main(String[] args) {
	        loadBooks(); // hardcoded or from file

	        int choice;
	        do {
	            System.out.println("\n--- Online Book Store ---");
	            System.out.println("1. View Books\n2. Search Book\n3. Add to Cart\n4. View Cart\n5. Checkout\n6. Exit");
	            choice = sc.nextInt();
	            sc.nextLine(); // consume newline

	            switch (choice) {
	                case 1: viewBooks(); break;
	                case 2: searchBook(); break;
	                case 3: addToCart(); break;
	                case 4: cart.viewCart(); break;
	                case 5: cart.checkout(); break;
	                case 6: System.out.println("Goodbye!"); break;
	                default: System.out.println("Invalid choice");
	            }
	        } while (choice != 6);
	    }

	    public static void loadBooks() {
	        bookList.add(new Book(1, "Java Basics", "James Gosling", 299.0));
	        bookList.add(new Book(2, "OOP in Java", "Bjarne Stroustrup", 399.0));
	        bookList.add(new Book(3, "Data Structures", "Robert Lafore", 499.0));
	    }

	    public static void viewBooks() {
	        for (Book b : bookList) {
	            b.dispaly();
	        }
	    }

	    public static void searchBook() {
	        System.out.print("Enter book title to search: ");
	        String keyword = sc.nextLine().toLowerCase();
	        for (Book b : bookList) {
	            if (b.title.toLowerCase().contains(keyword)) {
	                b.dispaly();
	            }
	        }
	    }

	    public static void addToCart() {
	        System.out.print("Enter book ID to add to cart: ");
	        int id = sc.nextInt();
	        for (Book b : bookList) {
	            if (b.id == id) {
	                cart.addToCart(b);
	                return;
	            }
	        }
	        System.out.println("Book not found.");
	    }


     
     import java.util.ArrayList;

public class Cart 
{
ArrayList<Book> cartItems=new ArrayList<>();
public void addToCart(Book book)
{
	cartItems.add(book);
	 System.out.println(book.title + " added to cart.");
}

public void viewCart() {
    if (cartItems.isEmpty()) {
        System.out.println("Cart is empty.");
        return;
    }
    double total = 0;
    for (Book b : cartItems) {
        b.dispaly();
        total += b.price;
    }
    System.out.println("Total: ₹" + total);
}

public void checkout() {
    System.out.println("Thank you for your purchase!");
    cartItems.clear();

}
}

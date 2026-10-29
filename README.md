import java.util.Scanner;
public class Main {
    static Scanner sc = new Scanner(System.in);
    static double getPrice(int category, int item) {
        switch (category) {
            case 1:
                if (item == 1) return 1500;
                if (item == 2) return 2500;
                break;
            case 2:
                if (item == 1) return 500;
                if (item == 2) return 1200;
                break;
            case 3:
                if (item == 1) return 1800;
                if (item == 2) return 2200;
                break;
            case 4:
                if (item == 1) return 2000;
                if (item == 2) return 900;
                break;
        }
        return 0;
    }

    static double calculsubto(double price, int quantity) {
        return quantity * price;
    }

    static double calcuTax(double subtotal) {
        return subtotal * 0.12;
    }

    static double calcudis(double subtotal, int customerType) {
        return customerType == 2 ? subtotal * 0.15 : 0;
    }

    static double calculateShipping(int orderType, double subtotal) {
        if (subtotal >= 3000) {
            return 0;
        }
        switch (orderType) {
            case 1:
                return 50;
            case 2:
                return 100;
            default:
                return 0;
        }
    }
    static void displayReceipt(String name, String address,
                               int customerType, int category, int item, int orderType,
                               int quantity, double price, double subtotal, double tax,
                               double discount, double shipping, double total) {

        String[] categories = {"Electronics", "Clothing", "Home Items", "Accessories"
        };
        String[] orderTypes = {"Standard Delivery", "Express Delivery", "Store Pickup"
        };
        String itemname = "";
        switch (category) {
            case 1:
                itemname = (item == 1) ? "Headphones":"Speaker";
                break;
            case 2:
                itemname = (item == 1) ? "T-shirt":"Jacket";
                break;
            case 3:
                itemname = (item == 1) ? "Blender":"Rice Cooker";
                break;
            case 4:
                itemname = (item == 1) ? "Watch":"Bag";
                break;
        }
        System.out.println("------------ SHOPPING RECEIPT -------------");
        System.out.println("Customer name: " + name);
        System.out.println("Customer Address: " + address);
        System.out.println("Customer Type: " +
                (customerType == 1 ? "Regular" : "VIP"));
        System.out.println("Category: " + categories[category]);
        System.out.println("Item: " + itemname);
        System.out.println("Order Type: " + orderTypes[orderType]);
        System.out.println("Quantity: " + quantity);

        System.out.printf("Price per Item: P%.2f%n", price);
        System.out.printf("Subtotal:  ₱%.2f%n", subtotal);
        System.out.printf("Tax:  ₱%.2f%n", tax);
        System.out.printf("Discount: %.2f%n",discount);
        System.out.printf("Shipping Fee:  ₱%.2f%n", shipping);
        System.out.printf("TOTAL COST:  ₱%.2f%n", total);
        System.out.println("=======================================");
    }

    public static void main(String[] args) {

        System.out.print("Customer Name: ");
        String name = sc.nextLine();

        System.out.print("Customer Address: ");
        String address = sc.nextLine();

        System.out.print("Customer Type (1-Regular, 2-VIP): ");
        int customerType = sc.nextInt();

        System.out.println("Order Type:");
        System.out.println("1. Standard Delivery");
        System.out.println("2. Express Delivery");
        System.out.println("3. Store Pickup");
        System.out.print("Choose Order Type: ");
        int orderType = sc.nextInt();

        System.out.println("Product Category:");
        System.out.println("1. Electronics");
        System.out.println("2. Clothing");
        System.out.println("3. Home Items");
        System.out.println("4. Accessories");
        System.out.print("Choose Category: ");
        int category = sc.nextInt();

        if (category < 1 || category > 4) {
            System.out.println("Invalid category.");
            return;
        }

        System.out.println("\nAvailable Items:");
        switch (category) {
            case 1:
                System.out.println("1. Headphones -  ₱1500");
                System.out.println("2. Speaker -  ₱2500");
                break;
            case 2:
                System.out.println("1. T-shirt -  ₱500");
                System.out.println("2. Jacket -  ₱1200");
                break;
            case 3:
                System.out.println("1. Blender -  ₱1800");
                System.out.println("2. Rice Cooker - ₱2200");
                break;
            case 4:
                System.out.println("1. Watch - ₱2000");
                System.out.println("2. Bag -   ₱900");
                break;
        }

        System.out.print("Choose Item: ");
        int item = sc.nextInt();

        if (item < 1 || item > 2) {
            System.out.println("Invalid item.");
            return;
        }
        System.out.print("Quantity: ");
        int quantity = sc.nextInt();

        double price = getPrice(category, item);
        double subtotal = calculsubto(price, quantity);
        double tax = calcuTax(subtotal);
        double discount = calcudis(subtotal, customerType);
        double shipping = calculateShipping(orderType, subtotal);
        double total = subtotal + tax + shipping - discount;

        displayReceipt(name, address, customerType, category, item,
                orderType, quantity, price, subtotal, tax, discount,
                shipping, total);
    }
}

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

class Item {
    private String name;
    private int quantity;
    private double price;

    public Item(String name, int quantity, double price) {
        this.name = name;
        this.quantity = quantity;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public int getQuantity() {
        return quantity;
    }

    public double getPrice() {
        return price;
    }

    public void setQuantity(int quantity) {
        this.quantity = quantity;
    }

    @Override
    public String toString() {
        return "Item: " + name + ", Quantity: " + quantity + ", Price: $" + String.format("%.2f", price);
    }
}

class Inventory {
    private Map<String, Item> items;

    public Inventory() {
        this.items = new HashMap<>();
    }

    public void addItem(Item item) {
        items.put(item.getName(), item);
        System.out.println(item.getName() + " added to inventory.");
    }

    public void removeItem(String itemName) {
        if (items.containsKey(itemName)) {
            items.remove(itemName);
            System.out.println(itemName + " removed from inventory.");
        } else {
            System.out.println("Item " + itemName + " not found in inventory.");
        }
    }

    public Item getItem(String itemName) {
        return items.get(itemName);
    }

    public void updateQuantity(String itemName, int newQuantity) {
        Item item = items.get(itemName);
        if (item != null) {
            item.setQuantity(newQuantity);
            System.out.println(itemName + " quantity updated to " + newQuantity);
        } else {
            System.out.println("Item " + itemName + " not found in inventory.");
        }
    }

    public List<Item> getAllItems() {
        return new ArrayList<>(items.values());
    }

    public void displayAllItems() {
        if (items.isEmpty()) {
            System.out.println("Inventory is empty.");
        } else {
            System.out.println("--- Inventory ---");
            for (Item item : items.values()) {
                System.out.println(item);
            }
            System.out.println("-----------------");
        }
    }
}

public class InventoryManagementSystem {
    public static void main(String[] args) {
        Inventory inventory = new Inventory();

        // Add items
        inventory.addItem(new Item("Laptop", 10, 1200.00));
        inventory.addItem(new Item("Mouse", 50, 25.00));
        inventory.addItem(new Item("Keyboard", 30, 75.00));

        // Display all items
        inventory.displayAllItems();

        // Update quantity
        inventory.updateQuantity("Laptop", 15);

        // Remove an item
        inventory.removeItem("Mouse");

        // Display updated inventory
        inventory.displayAllItems();

        // Get a specific item
        Item keyboard = inventory.getItem("Keyboard");
        if (keyboard != null) {
            System.out.println("\nFound item: " + keyboard);
        }
    }
}

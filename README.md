package Exp6;

import java.util.*;

abstract class Device {
    int deviceId;
    String brand;
    double price;

    Device(int deviceId, String brand, double price){
        this.deviceId = deviceId;
        this.brand = brand;
        this.price = price;
    }

    abstract void displayDetails();
}

interface Discountable {
    void applyDiscount(double percentage);
    double finalPrice();
}

class Smartphone extends Device implements Discountable {
    double discountedPrice;

    Smartphone(int id, String brand, double price){
        super(id,brand,price);
        discountedPrice = price;
    }

    public void applyDiscount(double percentage){
        discountedPrice = price - (price * (percentage/100));
    }

    public double finalPrice(){
        return discountedPrice;
    }

    void displayDetails(){
        System.out.println("Device ID: " + deviceId);
        System.out.println("Brand    : " + brand);
        System.out.println("Price    : " + price);
        System.out.println("Final Price After Discount: " + discountedPrice);
    }
}

public class SmartStore {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Smartphone phone = null;

        while(true){
            System.out.println("\n1. Add Smartphone");
            System.out.println("2. Apply Discount");
            System.out.println("3. View Device Details");
            System.out.println("4. Exit");
            System.out.print("Enter choice: ");

            int ch = sc.nextInt();

            switch(ch){
                case 1:
                    System.out.print("Enter Device ID: ");
                    int id = sc.nextInt();
                    System.out.print("Enter Brand: ");
                    String brand = sc.next();
                    System.out.print("Enter Price: ");
                    double price = sc.nextDouble();
                    phone = new Smartphone(id,brand,price);
                    break;

                case 2:
                    if(phone == null){
                        System.out.println("Add device first");
                    } else {
                        System.out.print("Enter discount percentage: ");
                        double per = sc.nextDouble();
                        phone.applyDiscount(per);
                    }
                    break;

                case 3:
                    if(phone == null){
                        System.out.println("No device added");
                    } else {
                        phone.displayDetails();
                    }
                    break;

                case 4:
                    System.exit(0);
                    break;

                default:
                    System.out.println("Invalid");
            }
        }
    }
}

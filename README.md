# Logistics-Management-System

ICT 1011 Computer Programming-Assignment(Individual)

import java.util.Scanner;



public class LogisticsManagementSystem {

    // Constants

    private static final int MAX\_CITIES = 30;

    private static final int MAX\_DELIVERIES = 50;

    private static final double FUEL\_PRICE = 310.0;

&nbsp;  

&nbsp;  // Arrays for data storage

&nbsp;   private static String\[] cities = new String\[MAX\_CITIES];

&nbsp;   private static int\[]\[] distances = new int\[MAX\_CITIES]\[MAX\_CITIES];

&nbsp;   private static Delivery\[] deliveries = new Delivery\[MAX\_DELIVERIES];

&nbsp;   

&nbsp;   // Vehicle data

&nbsp;   private static final String\[] VEHICLE\_TYPES = {"Van", "Truck", "Lorry"};

&nbsp;   private static final int\[] CAPACITIES = {1000, 5000, 10000};

&nbsp;   private static final int\[] RATES\_PER\_KM = {30, 40, 80};

&nbsp;   private static final int\[] AVG\_SPEEDS = {60, 50, 45};

&nbsp;   private static final int\[] FUEL\_EFFICIENCIES = {12, 6, 4};

&nbsp;   

&nbsp;   private static int cityCount = 0;

&nbsp;   private static int deliveryCount = 0;

&nbsp;   private static Scanner sc = new Scanner(System.in);

&nbsp;   

&nbsp;   public static void main(String\[] args) {

&nbsp;       loadData();

&nbsp;       

&nbsp;       while (true) {

&nbsp;           displayMainMenu();

&nbsp;           int choice = getIntInput("Enter your choice: ");

&nbsp;           

&nbsp;           switch (choice) {

&nbsp;               case 1:

&nbsp;                   manageCities();

&nbsp;                   break;

&nbsp;               case 2:

&nbsp;                   manageDistances();

&nbsp;                   break;

&nbsp;               case 3: 

&nbsp;                   handleDeliveryRequest();

&nbsp;                   break;

&nbsp;               case 4: 

&nbsp;                   generateReports();

&nbsp;                   break;

&nbsp;               case 5: 

&nbsp;                   saveData();

&nbsp;                   System.out.println("Thank you for using Logistics Management System!");

&nbsp;                   return;

&nbsp;               default: 

&nbsp;                   System.out.println("Invalid choice! Please try again.");

&nbsp;           }

&nbsp;       }

&nbsp;   }

&nbsp;   private static void displayMainMenu() {

&nbsp;       System.out.println("\\n=== Logistics Management System ===");

&nbsp;       System.out.println("1. City Management");

&nbsp;       System.out.println("2. Distance Management");

&nbsp;       System.out.println("3. Delivery Request");

&nbsp;       System.out.println("4. Reports");

&nbsp;       System.out.println("5. Exit");

&nbsp;   }

&nbsp;private static void manageCities() {

&nbsp;       while (true) {

&nbsp;           System.out.println("\\n=== City Management ===");

&nbsp;           System.out.println("1. Add City");

&nbsp;           System.out.println("2. View Cities");

&nbsp;           System.out.println("3. Back to Main Menu");

&nbsp;           

&nbsp;           int choice = getIntInput("Enter your choice: ");

&nbsp;           

&nbsp;           switch (choice) {

&nbsp;               case 1:

&nbsp;                   addCity(); 

&nbsp;                   break;

&nbsp;               case 2: 

&nbsp;                   viewCities(); 

&nbsp;                   break;

&nbsp;               case 3:

&nbsp;                   return;

&nbsp;               default:

&nbsp;                   System.out.println("Invalid choice!");

&nbsp;           }

&nbsp;       }

&nbsp;   }

private static void addCity() {

&nbsp;       if (cityCount >= MAX\_CITIES) {

&nbsp;           System.out.println("Maximum cities reached!");

&nbsp;           return;

&nbsp;       }

&nbsp;       

&nbsp;       System.out.print("Enter city name: ");

&nbsp;       String cityName = sc.nextLine().trim();

&nbsp;       

&nbsp;       if (cityName.isEmpty()) {

&nbsp;           System.out.println("City name cannot be empty!");

&nbsp;           return;

&nbsp;       }

&nbsp;       

&nbsp;       // Check for duplicate

&nbsp;       for (int i = 0; i < cityCount; i++) {

&nbsp;           if (cities\[i].equalsIgnoreCase(cityName)) {

&nbsp;               System.out.println("City already exists!");

&nbsp;               return;

&nbsp;           }

&nbsp;       }

&nbsp;       

&nbsp;       cities\[cityCount] = cityName;

&nbsp;       cityCount++;

&nbsp;       System.out.println("City added successfully!");

&nbsp;   }

&nbsp;private static void viewCities() {

&nbsp;       System.out.println("\\n=== Cities List ===");

&nbsp;       if (cityCount == 0) {

&nbsp;           System.out.println("No cities added yet.");

&nbsp;           return;

&nbsp;       }

&nbsp;       

&nbsp;       for (int i = 0; i < cityCount; i++) {

&nbsp;           System.out.println((i + 1) + ". " + cities\[i]);

&nbsp;       }

&nbsp;   }


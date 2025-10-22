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

&nbsp;   


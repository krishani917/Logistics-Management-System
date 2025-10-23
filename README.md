# Logistics-Management-System

ICT 1011 Computer Programming-Assignment(Individual)

import java.util.Scanner;



public class LogisticsManagementSystem {

    // Constants

    private static final int MAX\_CITIES = 30;

    private static final int MAX\_DELIVERIES = 50;

    private static final double FUEL\_PRICE = 310.0;

 

   // Arrays for data storage

    private static String\[] cities = new String\[MAX\_CITIES];

    private static int\[]\[] distances = new int\[MAX\_CITIES]\[MAX\_CITIES];

    private static Delivery\[] deliveries = new Delivery\[MAX\_DELIVERIES];

 

    // Vehicle data

    private static final String\[] VEHICLE\_TYPES = {"Van", "Truck", "Lorry"};

    private static final int\[] CAPACITIES = {1000, 5000, 10000};

    private static final int\[] RATES\_PER\_KM = {30, 40, 80};

    private static final int\[] AVG\_SPEEDS = {60, 50, 45};

    private static final int\[] FUEL\_EFFICIENCIES = {12, 6, 4};

 

    private static int cityCount = 0;

    private static int deliveryCount = 0;

    private static Scanner sc = new Scanner(System.in);

 

    public static void main(String\[] args) {

        loadData();

 

        while (true) {

            displayMainMenu();

            int choice = getIntInput("Enter your choice: ");

 

            switch (choice) {

                case 1:

                    manageCities();

                    break;

                case 2:

                    manageDistances();

                    break;

                case 3:

                    handleDeliveryRequest();

                    break;

                case 4:

                    generateReports();

                    break;

                case 5:

                    saveData();

                    System.out.println("Thank you for using Logistics Management System!");

                    return;

                default:

                    System.out.println("Invalid choice! Please try again.");

            }

        }

    }

    private static void displayMainMenu() {

        System.out.println("\\n=== Logistics Management System ===");

        System.out.println("1. City Management");

        System.out.println("2. Distance Management");

        System.out.println("3. Delivery Request");

        System.out.println("4. Reports");

        System.out.println("5. Exit");

    }

 private static void manageCities() {

        while (true) {

            System.out.println("\\n=== City Management ===");

            System.out.println("1. Add City");

            System.out.println("2. View Cities");

            System.out.println("3. Back to Main Menu");

 

            int choice = getIntInput("Enter your choice: ");

 

            switch (choice) {

                case 1:

                    addCity();

                    break;

                case 2:

                    viewCities();

                    break;

                case 3:

                    return;

                default:

                    System.out.println("Invalid choice!");

            }

        }

    }

private static void addCity() {

        if (cityCount >= MAX\_CITIES) {

            System.out.println("Maximum cities reached!");

            return;

        }

 

        System.out.print("Enter city name: ");

        String cityName = sc.nextLine().trim();

 

        if (cityName.isEmpty()) {

            System.out.println("City name cannot be empty!");

            return;

        }

 

        // Check for duplicate

        for (int i = 0; i < cityCount; i++) {

            if (cities\[i].equalsIgnoreCase(cityName)) {

                System.out.println("City already exists!");

                return;

            }

        }

 

        cities\[cityCount] = cityName;

        cityCount++;

        System.out.println("City added successfully!");

    }

 private static void viewCities() {

        System.out.println("\\n=== Cities List ===");

        if (cityCount == 0) {

            System.out.println("No cities added yet.");

            return;

        }

 

        for (int i = 0; i < cityCount; i++) {

            System.out.println((i + 1) + ". " + cities\[i]);

        }

    }

private static void manageDistances() {

        if (cityCount < 2) {

            System.out.println("Need at least 2 cities to manage distances!");

            return;

        }

 

        while (true) {

            System.out.println("\\n=== Distance Management ===");

            System.out.println("1. Set Distance");

            System.out.println("2. View Distance Table");

            System.out.println("3. Back to Main Menu");

 

            int choice = getIntInput("Enter your choice: ");

 

            switch (choice) {

                case 1:

                    setDistance();

                    break;

                case 2:

                    viewDistanceTable();

                    break;

                case 3:

                    return;

                default:

                    System.out.println("Invalid choice!");

            }

        }

    }

    private static void setDistance() {

        viewCities();

        int city1 = getIntInput("Enter first city number: ") - 1;

        int city2 = getIntInput("Enter second city number: ") - 1;

 

        if (city1 < 0 || city1 >= cityCount || city2 < 0 || city2 >= cityCount) {

            System.out.println("Invalid city selection!");

            return;

        }

 

        if (city1 == city2) {

            System.out.println("Distance to same city is always 0!");

            return;

        }

 

        int distance = getIntInput("Enter distance (km): ");

        distances\[city1]\[city2] = distance;

        distances\[city2]\[city1] = distance; // Symmetric

        System.out.println("Distance set successfully!");

    }

    private static void viewDistanceTable() {

        System.out.println("\\n=== Distance Table ===");

        System.out.print("     ");

        for (int i = 0; i < cityCount; i++) {

            System.out.printf("%-10s", cities\[i].substring(0, Math.min(8, cities\[i].length())));

        }

        System.out.println();

 

        for (int i = 0; i < cityCount; i++) {

            System.out.printf("%-5s", cities\[i].substring(0, Math.min(4, cities\[i].length())));

            for (int j = 0; j < cityCount; j++) {

                System.out.printf("%-10d", distances\[i]\[j]);

            }

            System.out.println();

        }

    }

private static void handleDeliveryRequest() {

&nbsp;       if (cityCount < 2) {

&nbsp;           System.out.println("Need at least 2 cities for delivery!");

&nbsp;           return;

&nbsp;       }

&nbsp;       

&nbsp;       if (deliveryCount >= MAX\_DELIVERIES) {

&nbsp;           System.out.println("Maximum deliveries reached!");

&nbsp;           return;

&nbsp;       }

&nbsp;       

&nbsp;       System.out.println("\\n=== New Delivery Request ===");

&nbsp;       viewCities();

&nbsp;       

&nbsp;       int source = getIntInput("Enter source city number: ") - 1;

&nbsp;       int destination = getIntInput("Enter destination city number: ") - 1;

&nbsp;       

&nbsp;       if (source < 0 || source >= cityCount || destination < 0 || destination >= cityCount) {

&nbsp;           System.out.println("Invalid city selection!");

&nbsp;           return;

&nbsp;       }

&nbsp;       

&nbsp;       if (source == destination) {

&nbsp;           System.out.println("Source and destination cannot be same!");

&nbsp;           return;

&nbsp;       }

&nbsp;       

&nbsp;       if (distances\[source]\[destination] == 0) {

&nbsp;           System.out.println("Distance not set between these cities!");

&nbsp;           return;

&nbsp;       }

&nbsp;       

&nbsp;       // Display vehicle options

&nbsp;       System.out.println("\\nVehicle Options:");

&nbsp;       for (int i = 0; i < VEHICLE\_TYPES.length; i++) {

&nbsp;           System.out.println((i + 1) + ". " + VEHICLE\_TYPES\[i] + 

&nbsp;                            " (Capacity: " + CAPACITIES\[i] + "kg, Rate: " + 

&nbsp;                            RATES\_PER\_KM\[i] + " LKR/km)");

&nbsp;       }

&nbsp;       

&nbsp;       int vehicleType = getIntInput("Select vehicle (1-3): ") - 1;

&nbsp;       if (vehicleType < 0 || vehicleType >= VEHICLE\_TYPES.length) {

&nbsp;           System.out.println("Invalid vehicle selection!");

&nbsp;           return;

&nbsp;       }

&nbsp;       

&nbsp;       int weight = getIntInput("Enter weight (kg): ");

&nbsp;       if (weight > CAPACITIES\[vehicleType]) {

&nbsp;           System.out.println("Weight exceeds vehicle capacity!");

&nbsp;           return;

&nbsp;       }

&nbsp;       

&nbsp;       // Calculate delivery details

&nbsp;       calculateAndDisplayDelivery(source, destination, vehicleType, weight);

&nbsp;   }

&nbsp;private static void calculateAndDisplayDelivery(int source, int destination, int vehicleType, int weight) {

&nbsp;       int distance = distances\[source]\[destination];

&nbsp;       double baseCost = distance \* RATES\_PER\_KM\[vehicleType] \* (1 + weight / 10000.0);

&nbsp;       double deliveryTime = (double) distance / AVG\_SPEEDS\[vehicleType];

&nbsp;       double fuelUsed = (double) distance / FUEL\_EFFICIENCIES\[vehicleType];

&nbsp;       double fuelCost = fuelUsed \* FUEL\_PRICE;

&nbsp;       double operationalCost = baseCost + fuelCost;

&nbsp;       double profit = baseCost \* 0.25;

&nbsp;       double customerCharge = operationalCost + profit;

&nbsp;       

&nbsp;       // Store delivery record

&nbsp;       deliveries\[deliveryCount] = new Delivery(

&nbsp;           cities\[source], cities\[destination], distance, 

&nbsp;           VEHICLE\_TYPES\[vehicleType], weight, customerCharge, deliveryTime

&nbsp;       );

&nbsp;       deliveryCount++;

&nbsp;       

&nbsp;       // Display results

&nbsp;       System.out.println("\\n--- DELIVERY COST ESTIMATION ---");

&nbsp;       System.out.println("From: " + cities\[source]);

&nbsp;       System.out.println("To: " + cities\[destination]);

&nbsp;       System.out.println("Distance: " + distance + " km");

&nbsp;       System.out.println("Vehicle: " + VEHICLE\_TYPES\[vehicleType]);

&nbsp;       System.out.println("Weight: " + weight + " kg");

&nbsp;       System.out.printf("Base Cost: %.2f LKR\\n", baseCost);

&nbsp;       System.out.printf("Fuel Used: %.2f L\\n", fuelUsed);

&nbsp;       System.out.printf("Fuel Cost: %.2f LKR\\n", fuelCost);

&nbsp;       System.out.printf("Operational Cost: %.2f LKR\\n", operationalCost);

&nbsp;       System.out.printf("Profit: %.2f LKR\\n", profit);

&nbsp;       System.out.printf("Customer Charge: %.2f LKR\\n", customerCharge);

&nbsp;       System.out.printf("Estimated Time: %.2f hours\\n", deliveryTime);

&nbsp;   }

&nbsp;   


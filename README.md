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

        if (cityCount < 2) {

            System.out.println("Need at least 2 cities for delivery!");

            return;

        }

 

        if (deliveryCount >= MAX\_DELIVERIES) {

            System.out.println("Maximum deliveries reached!");

            return;

        }

 

        System.out.println("\\n=== New Delivery Request ===");

        viewCities();

 

        int source = getIntInput("Enter source city number: ") - 1;

        int destination = getIntInput("Enter destination city number: ") - 1;

 

        if (source < 0 || source >= cityCount || destination < 0 || destination >= cityCount) {

            System.out.println("Invalid city selection!");

            return;

        }

 

        if (source == destination) {

            System.out.println("Source and destination cannot be same!");

            return;

        }

 

        if (distances\[source]\[destination] == 0) {

            System.out.println("Distance not set between these cities!");

            return;

        }

 

        // Display vehicle options

        System.out.println("\\nVehicle Options:");

        for (int i = 0; i < VEHICLE\_TYPES.length; i++) {

            System.out.println((i + 1) + ". " + VEHICLE\_TYPES\[i] +

                             " (Capacity: " + CAPACITIES\[i] + "kg, Rate: " +

                             RATES\_PER\_KM\[i] + " LKR/km)");

        }

 

        int vehicleType = getIntInput("Select vehicle (1-3): ") - 1;

        if (vehicleType < 0 || vehicleType >= VEHICLE\_TYPES.length) {

            System.out.println("Invalid vehicle selection!");

            return;

        }

 

        int weight = getIntInput("Enter weight (kg): ");

        if (weight > CAPACITIES\[vehicleType]) {

            System.out.println("Weight exceeds vehicle capacity!");

            return;

        }

 

        // Calculate delivery details

        calculateAndDisplayDelivery(source, destination, vehicleType, weight);

    }

 private static void calculateAndDisplayDelivery(int source, int destination, int vehicleType, int weight) {

        int distance = distances\[source]\[destination];

        double baseCost = distance \* RATES\_PER\_KM\[vehicleType] \* (1 + weight / 10000.0);

        double deliveryTime = (double) distance / AVG\_SPEEDS\[vehicleType];

        double fuelUsed = (double) distance / FUEL\_EFFICIENCIES\[vehicleType];

        double fuelCost = fuelUsed \* FUEL\_PRICE;

        double operationalCost = baseCost + fuelCost;

        double profit = baseCost \* 0.25;

        double customerCharge = operationalCost + profit;

 

        // Store delivery record

        deliveries\[deliveryCount] = new Delivery(

            cities\[source], cities\[destination], distance,

            VEHICLE\_TYPES\[vehicleType], weight, customerCharge, deliveryTime

        );

        deliveryCount++;

 

        // Display results

        System.out.println("\\n--- DELIVERY COST ESTIMATION ---");

        System.out.println("From: " + cities\[source]);

        System.out.println("To: " + cities\[destination]);

        System.out.println("Distance: " + distance + " km");

        System.out.println("Vehicle: " + VEHICLE\_TYPES\[vehicleType]);

        System.out.println("Weight: " + weight + " kg");

        System.out.printf("Base Cost: %.2f LKR\\n", baseCost);

        System.out.printf("Fuel Used: %.2f L\\n", fuelUsed);

        System.out.printf("Fuel Cost: %.2f LKR\\n", fuelCost);

        System.out.printf("Operational Cost: %.2f LKR\\n", operationalCost);

        System.out.printf("Profit: %.2f LKR\\n", profit);

        System.out.printf("Customer Charge: %.2f LKR\\n", customerCharge);

        System.out.printf("Estimated Time: %.2f hours\\n", deliveryTime);

    }

private static void generateReports() {

        System.out.println("\\n=== Performance Reports ===");

        System.out.println("Total Deliveries Completed: " + deliveryCount);

 

        double totalDistance = 0;

        double totalRevenue = 0;

        double totalProfit = 0;

        double totalTime = 0;

        double longestRoute = 0;

        double shortestRoute = Double.MAX\_VALUE;

 

        for (int i = 0; i < deliveryCount; i++) {

            Delivery delivery = deliveries\[i];

            totalDistance += delivery.distance;

            totalRevenue += delivery.cost;

            totalProfit += delivery.cost \* 0.25; // Assuming 25% profit margin

            totalTime += delivery.time;

 

            if (delivery.distance > longestRoute) longestRoute = delivery.distance;

            if (delivery.distance < shortestRoute) shortestRoute = delivery.distance;

        }

 

        System.out.printf("Total Distance Covered: %.2f km\\n", totalDistance);

        System.out.printf("Average Delivery Time: %.2f hours\\n",

                         deliveryCount > 0 ? totalTime / deliveryCount : 0);

        System.out.printf("Total Revenue: %.2f LKR\\n", totalRevenue);

        System.out.printf("Total Profit: %.2f LKR\\n", totalProfit);

        System.out.printf("Longest Route: %.2f km\\n", longestRoute);

        System.out.printf("Shortest Route: %.2f km\\n",

                         shortestRoute == Double.MAX\_VALUE ? 0 : shortestRoute);

    }

 private static void loadData() {

&nbsp;       // Basic implementation - can be extended to read from files

&nbsp;       System.out.println("Loading system data...");

&nbsp;   }

&nbsp;   

&nbsp;   private static void saveData() {

&nbsp;       // Basic implementation - can be extended to save to files

&nbsp;       System.out.println("Saving system data...");

&nbsp;   }

&nbsp;   

&nbsp;   // Utility methods

&nbsp;   private static int getIntInput(String message) {

&nbsp;       while (true) {

&nbsp;           try {

&nbsp;               System.out.print(message);

&nbsp;               return Integer.parseInt(sc.nextLine());

&nbsp;           } catch (NumberFormatException e) {

&nbsp;               System.out.println("Please enter a valid number!");

&nbsp;           }

&nbsp;       }

&nbsp;   }

&nbsp;   

&nbsp;   // Delivery record class

&nbsp;   static class Delivery {

&nbsp;       String source;

&nbsp;       String destination;

&nbsp;       int distance;

&nbsp;       String vehicleType;

&nbsp;       int weight;

&nbsp;       double cost;

&nbsp;       double time;

&nbsp;       

&nbsp;       public Delivery(String source, String destination, int distance, 

&nbsp;                      String vehicleType, int weight, double cost, double time) {

&nbsp;           this.source = source;

&nbsp;           this.destination = destination;

&nbsp;           this.distance = distance;

&nbsp;           this.vehicleType = vehicleType;

&nbsp;           this.weight = weight;

&nbsp;           this.cost = cost;

&nbsp;           this.time = time;

&nbsp;       }

&nbsp;   }

}


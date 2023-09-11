
Your son took a vacation through Europe without telling you. When the kid returned from the vacation you asked him where did he go. The kid told you: Dad I went to these cities: Amsterdam, Kiev, Zurich, Prague, Berlin, Barcelona.
I used only train as transportation and these were the available tickets:
Paris-Skopje, Zurich-Amsterdam, Prague-Zurich, Barcelona-Berlin, Kiev-Prague, Skopje-Paris, Amsterdam-Barcelona, Berlin-Kiev, Berlin-Amsterdam.
You know that your kid started with Kiev
Write a data structure in java and algorithm that will give you the route which your son was traveling.

import java.util.*;
public class VacationRoute {
    public static List<String> findRoute(String[] tickets) {
        // Create a graph representation of the available tickets
        Map<String, List<String>> graph = new HashMap<>();
        for (String ticket : tickets) {
            String[] parts = ticket.split("-");
            String fromCity = parts[0];
            String toCity = parts[1];
            graph.putIfAbsent(fromCity, new ArrayList<>());
            graph.get(fromCity).add(toCity);
        }

        // Initialize variables
        String startCity = "Kiev"; // Your son started in Kiev
        Set<String> visited = new HashSet<>();
        List<String> route = new ArrayList<>();

        // Define a recursive DFS function to find the route
        dfs(startCity, graph, visited, route);

        return route;
    }

    private static void dfs(String city, Map<String, List<String>> graph, Set<String> visited, List<String> route) {
        visited.add(city);
        route.add(city);

        if (graph.containsKey(city)) {
            for (String neighbor : graph.get(city)) {
                if (!visited.contains(neighbor)) {
                    dfs(neighbor, graph, visited, route);
                }
            }
        }
    }

    public static void main(String[] args) {
        String[] tickets = {
            "Paris-Skopje", "Zurich-Amsterdam", "Prague-Zurich",
            "Barcelona-Berlin", "Kiev-Prague", "Skopje-Paris",
            "Amsterdam-Barcelona", "Berlin-Kiev", "Berlin-Amsterdam"
        };

        // Find the route
        List<String> route = findRoute(tickets);

        // Print the route
        System.out.println("Route traveled by your son:");
        for (String city : route) {
            System.out.println(city);
        }
    }
}

/* Print the destination coordinates and both distances on one line. */
void printDistanceRow(const char name[], double fromLat, double fromLon,
                      double toLat, double toLon)
{
    double globalKm = distanceKm(fromLat, fromLon, toLat, toLon);
    double localKm = localDistanceKm(fromLat, fromLon, toLat, toLon);

    printf("%-18s %11.6f %12.6f %12.1f %12.1f\n",
           name, toLat, toLon, globalKm, localKm);
}

int main(void)
{
    const double hawLat = 53.557078;
    const double hawLon = 10.023109;

    printf("Distances from HAW Hamburg\n");
    printf("%-18s %11s %12s %12s %12s\n",
           "Location", "Latitude", "Longitude", "Global (km)", "Local (km)");

    printDistanceRow("HAW Hamburg", hawLat, hawLon, hawLat, hawLon);
    printDistanceRow("Eiffel Tower", hawLat, hawLon, 48.858363, 2.294481);
    printDistanceRow("Palma de Mallorca", hawLat, hawLon, 39.562553, 2.661947);
    printDistanceRow("Las Vegas", hawLat, hawLon, 36.156214, -115.148736);
    printDistanceRow("Copacabana", hawLat, hawLon, -22.971177, -43.182543);
    printDistanceRow("Waikiki Beach", hawLat, hawLon, 21.281004, -157.837456);
    printDistanceRow("Surfer's Paradise", hawLat, hawLon, -28.002695, 153.431781);

    return 0;
}

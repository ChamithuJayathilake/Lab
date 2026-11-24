/* 1. Include directives */
#define _USE_MATH_DEFINES

#include <stdio.h>
#include <math.h>

/* 2. Prototypes */
double degreesToRadians(double degrees);
double distanceKm(double lat1, double lon1, double lat2, double lon2);
double LocalDistance(double lat1, double lon1, double lat2, double lon2);
void printDistanceRow(const char name[], double fromLat, double fromLon, double toLat, double toLon);

/* 3. Global variables */
const double hawLat = 53.557078;
const double hawLon = 10.023109;

/* 4. Main function */
int main(void)
{
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

/* 5. Other functions */
double degreesToRadians(double degrees)
{
    return degrees * M_PI / 180.0;
}

// Global distance on the Earth's surface, using workbook equation (15.4).
double distanceKm(double lat1, double lon1, double lat2, double lon2)
{
    const double earthRadiusKm = 6378.388;

    if (lat1 == lat2 && lon1 == lon2)
    {
        return 0.0;
    }

    double lat1Rad = degreesToRadians(lat1);
    double lat2Rad = degreesToRadians(lat2);
    double lonDiffRad = degreesToRadians(lon2 - lon1);
    double cosAngle = sin(lat1Rad) * sin(lat2Rad) + cos(lat1Rad) * cos(lat2Rad) * cos(lonDiffRad);

    double angleRad = acos(cosAngle);
    return earthRadiusKm * angleRad;
}

double LocalDistance(double lat1, double lon1, double lat2, double lon2)
{
    const double kmPerDegree = 111.3;

    // cos() expects the average latitude in radians.
    double averageLatitude = (lat1 + lat2) / 2.0;
    double averageRadians = averageLatitude * M_PI / 180.0;

    // dy is the north-south distance. dx is the east-west distance.
    double dy = kmPerDegree * fabs(lat1 - lat2);
    double dx = kmPerDegree * cos(averageRadians) * fabs(lon1 - lon2);

    return sqrt(dx * dx + dy * dy);
}

void printDistanceRow(const char name[], double fromLat, double fromLon, double toLat, double toLon)
{
    double globalKm = distanceKm(fromLat, fromLon, toLat, toLon);
    double localKm = LocalDistance(fromLat, fromLon, toLat, toLon);

    printf("%-18s %11.6f %12.6f %12.1f %12.1f\n", name, toLat, toLon, globalKm, localKm);
}

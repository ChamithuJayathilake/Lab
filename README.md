#include <stdio.h>

int main() {
    int field;

    unsigned long long grains_on_field = 1;
    unsigned long long sum_grains = 0;

    printf("Field |     On field         | Sum\n");
    printf("------+----------------------+------------------------------------\n");

    for (field = 1; field <= 64; field++) {
        sum_grains += grains_on_field;

        printf("%5d | %20llu | %20llu   (= %.1e)\n", field, grains_on_field, sum_grains, (double)sum_grains);

        if (field == 8) {
            printf("------+----------------------+-------------------------------------\n");
        }
        else if (field == 16) {
            printf("------+----------------------+-------------------------------------\n");
        }
        else if (field == 32) {
            printf("------+----------------------+-------------------------------------\n");
        }
        else if (field == 64) {
            printf("------+----------------------+-------------------------------------\n");
        }
        grains_on_field *= 2;
    }
    return 0;
}

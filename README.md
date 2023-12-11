
# include <stdio.h>
# include <stdlib.h>
# include <string.h>

# define MAX_SPACES 10
# define FILENAME "parking_status.txt"

// Function to update the parking status in the text file and display in terminal
void updateParkingStatus(int status[]) {
    FILE *file = fopen(FILENAME, "w");
    if (file == NULL) {
        printf("Error opening file!\n");
        exit(1);
    }

    printf("Parking Spaces Status:\n");
    fprintf(file, "Parking Spaces Status:\n");

    for (int i = 0; i < MAX_SPACES; ++i) {
        printf("Space %d: %s\n", i + 1, status[i] ? "Occupied" : "Empty");
        fprintf(file, "Space %d: %s\n", i + 1, status[i] ? "Occupied" : "Empty");
    }

    fclose(file);
}

int main() {
    int parkingSpaces[MAX_SPACES] = {0}; // 0 for empty, 1 for occupied

    // Initial status: all spaces are empty
    updateParkingStatus(parkingSpaces);

    int choice;
    do {
        printf("\nCar Parking System\n");
        printf("1. Park Car\n");
        printf("2. Remove Car\n");
        printf("3. View Parking Status\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1: {
                int space;
                printf("Enter parking space number to park the car (1 - %d): ", MAX_SPACES);
                scanf("%d", &space);

                if (space >= 1 && space <= MAX_SPACES) {
                    if (parkingSpaces[space - 1] == 0) {
                        parkingSpaces[space - 1] = 1; 
                        printf("Car parked successfully in space %d.\n", space);
                        updateParkingStatus(parkingSpaces);
                    } else {
                        printf("Space %d is already occupied.\n", space);
                    }
                } else {
                    printf("Invalid space number.\n");
                }
                break;
            }
            case 2: {
                int space;
                printf("Enter parking space number to remove the car (1 - %d): ", MAX_SPACES);
                scanf("%d", &space);

                if (space >= 1 && space <= MAX_SPACES) {
                    if (parkingSpaces[space - 1] == 1) {
                        parkingSpaces[space - 1] = 0; 
                        printf("Car removed from space %d.\n", space);
                        updateParkingStatus(parkingSpaces);
                    } else {
                        printf("Space %d is already empty.\n", space);
                    }
                } else {
                    printf("Invalid space number.\n");
                }
                break;
            }
            case 3:
                updateParkingStatus(parkingSpaces);
                printf("already showed.\n");
                break;
            case 4:
                printf("Exiting...\n");
                break;
            default:
                printf("Invalid choice. Please enter a valid option.\n");
        }
    } while (choice != 4);

    return 0;
}

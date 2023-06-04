#include<stdio.h>//important to have an standard input and output
#include<stdlib.h> //this is for system("clear")
#include <string.h> //for strings to function correctly

//Defining the Box size
#define BOX_WIDTH 10
#define BOX_HEIGHT 10
#define FILENAME "user_data.csv"

//for the clearscreen function
void clear_screen(){
    system("cls");
       }

//for the box to print the "x" mark to the current location or the new location that the user inputed
void display_box(int user_x, int user_y){
    int i, j;

    for(i = 0; i<BOX_HEIGHT; i++){
        for(j = 0; j<BOX_WIDTH; j++){
            if(i == user_y && j == user_x){
                printf("X");
            }else{
            printf("-");
            }
        }
    printf("\n");
    }
}

//File Handling
struct UserData {
    char username[20];
    char password[20];
};
void saveUserData(struct UserData user) {
    FILE *file = fopen(FILENAME, "w");
    if (file == NULL) {
        printf("Error opening file!\n");
        return;
    }

    fprintf(file, "Username,Password\n");
    fprintf(file, "%s,%s\n", user.username, user.password);

    fclose(file);
}
int main(){
    struct UserData user;

    printf("  Log-in\n");
    printf("Username: ");
    scanf("%s", user.username);
    printf("Password: ");
    scanf("%s", user.password);

    // Here you can check the username and password against a stored value or a database

    saveUserData(user);
    printf("User data saved to file.\n");

    printf("\n");//for the newline

    int x = 0, y = 0;//initializing the coordinates of Angkul
    int min_x = 0, max_x = BOX_WIDTH - 1, min_y = 0, max_y = BOX_HEIGHT -1; //set the boundaries of the box
    char direction;

//This is where the mini system display the information about the directions
    printf("Starting point Location of Angkul: (%d, %d)\n",x ,y);
    printf("  DIRECTIONS MENU:\n");
    printf(" 1.N= North\n");
    printf(" 2.S= south\n");
    printf(" 3.W= West\n");
    printf(" 4.E= East\n");

//Loop
    while (1){
        printf("Where do you want to go?: ");
        scanf(" %c",&direction);

    clear_screen();

    int new_x = x, new_y = y;

//Conditions
    switch(direction){
        case 'N':
        case 'n':
            new_y -=1;
            break;
        case 'S':
        case 's':
            new_y +=1;
        break;
        case 'W':
        case 'w':
            new_x -=1;
            break;
        case 'E':
        case 'e':
            new_x +=1;
            break;
        default:
            printf("Invalid directions!\n");
            continue;//para mo balik siya :( sa loop deay..
    }

//setting Boundary of the box
    if (new_x < min_x || new_x > max_x || new_y < min_y || new_y > max_y){
        printf("You cannot move to that direction!\n");
    }else{
        x = new_x;
        y = new_y;
        printf("New Location of Angkul: (%d, %d)\n", x, y);
    }
//This is where we print the box with the current location that the user inputed
    display_box(x, y);

}
return 0;
}

# Message-Encryption-in-C
# ![Cipher](cipher.png)

This is a C program that performs an XOR encryption of a text message.

[![Try with Replit Badge](https://replit.com/badge?caption=Try%20with%20Replit)](https://replit.com/@Dual-CoreCore/Message-Encryption#main.c)

```c

/* 
 !██╗  ██╗ ██████╗ ██████╗ 
 !╚██╗██╔╝██╔═══██╗██╔══██╗
  !╚███╔╝ ██║   ██║██████╔╝
  !██╔██╗ ██║   ██║██╔══██
 !██╔╝ ██╗╚██████╔╝██║  ██║
 !╚═╝  ╚═╝ ╚═════╝ ╚═╝  ╚═╝      
 
 ?███████╗███╗   ██╗ ██████╗██████╗ ██╗   ██╗██████╗ ████████╗██╗ ██████╗ ███╗   ██╗
 ?██╔════╝████╗  ██║██╔════╝██╔══██╗╚██╗ ██╔╝██╔══██╗╚══██╔══╝██║██╔═══██╗████╗  ██║
 ?█████╗  ██╔██╗ ██║██║     ██████╔╝ ╚████╔╝ ██████╔╝   ██║   ██║██║   ██║██╔██╗ ██║
 ?██╔══╝  ██║╚██╗██║██║     ██╔══██╗  ╚██╔╝  ██╔═══╝    ██║   ██║██║   ██║██║╚██╗██║
 ?███████╗██║ ╚████║╚██████╗██║  ██║   ██║   ██║        ██║   ██║╚██████╔╝██║ ╚████║
 ?╚══════╝╚═╝  ╚═══╝ ╚═════╝╚═╝  ╚═╝   ╚═╝   ╚═╝        ╚═╝   ╚═╝ ╚═════╝ ╚═╝  ╚═══╝
                                                                                   
*/


#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include "colors.h"
#define MAX_LENGTH 20
#define DASH_LINE puts("+------------------------+")
#define NEW_LINE puts("\n")
#define PROGRESS_BAR_LENGTH 30

void Update_Bar(int percent_done){

    int num_chars = percent_done * PROGRESS_BAR_LENGTH / 100;
    printf(BHGRN "\r[" reset);
    
    for(int i = 0; i < num_chars; i++){

        printf(BHGRN "#" reset);
    }

    for(int i = 0; i < PROGRESS_BAR_LENGTH - num_chars; i++){

        printf(" ");
    }
    printf(BHGRN "] %d%% " reset,percent_done);
    fflush(stdout);
}

void Progress_Bar(){

    for(int i = 0; i <= 100; i++){

        Update_Bar(i);
        usleep(1500);
    }
    printf("\n");
}

int main(){

    char key[MAX_LENGTH] = "";
    char message[MAX_LENGTH];
    char encrypted_message[MAX_LENGTH];
    char decrypted_message[MAX_LENGTH] = "";
    int i;

    printf(BHMAG "Message User Input" reset "\n");
    DASH_LINE;
    printf("Write your message \n \u2193 \n");  
    printf("Message: ");
    i = 0;
    do{

        message[i++] = getchar();
        if(i > MAX_LENGTH){

            break;
        }

    }while(message[i - 1] != 10);
    message[i] = '\0';
    DASH_LINE;

    NEW_LINE;

    printf(HBLU "Key User Input" reset "\n");
    DASH_LINE;
    printf("Write your key \n \u2193 \n");
    printf("Key: ");  
    i = 0;
    do{

        key[i++] = getchar();
        if(i > MAX_LENGTH){

            break;
        }

    }while(key[i - 1] != 10);
    key[i] = '\0';
    DASH_LINE;
    
        NEW_LINE;

    Progress_Bar();
    printf(BHGRN "\t\t\t\t Encrypted" reset);

    NEW_LINE;
        
    printf(REDHB "Message Encryption" reset "\n");
    DASH_LINE;
    

    for(i = 0; i < strlen(message) - 1; i++){

        encrypted_message[i] = message[i] ^ key[i%(strlen(key) - 1)];
    }
    encrypted_message[i] = '\0';
        
    printf("Encrypted Message \n \u2193 \n");
    printf("%s\n",encrypted_message);
    
    DASH_LINE;
    
    printf(BHRED "PRESS ANY KEY TO DECRYPT THE MESSAGE\n" reset);
    getchar();
    Progress_Bar();
    printf(BHGRN "\t\t\t\t Decrypted" reset);

    NEW_LINE;


    printf(BLUHB "Message Decryption" reset "\n");
    DASH_LINE;
    for(i = 0; i < strlen(message) - 1; i++){

        decrypted_message[i] = encrypted_message[i] ^ key[i%(strlen(key) - 1)];
    }
    decrypted_message[i] = '\0';
        
    printf("Decrypted Message \n \u2193 \n");
    printf("%s\n",decrypted_message);
    DASH_LINE;

    printf(BHRED "PRESS ANY KEY TO EXIT\n" reset);
    getchar();
    system("clear");
    printf(BHMAG "-----------------------------------------\n" reset);
    printf(BHMAG "\t\tGoodbye\n" reset);
    printf(BHMAG "-----------------------------------------\n" reset);
    usleep(2000);

    return 0;
}
```

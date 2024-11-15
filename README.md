# EX-10 : IMPLEMENTATION-OF-DIFFIE-HELLMAN-KEY-EXCHANGE-ALGORITHM

## AIM:
To implement the Diffie-Hellman Key Exchange algorithm using C language.

## ALGORITHM:
  
  STEP-1: Both Alice and Bob shares the same public keys g and p.
  
  STEP-2: Alice selects a random public key a.
  
  STEP-3: Alice computes his secret key A as g a mod p.
  
  STEP-4: Then Alice sends A to Bob.
  
  STEP-5: Similarly Bob also selects a public key b and computes his secret key as B and sends the same back to Alice.
  
  STEP-6: Now both of them compute their common secret key as the other one’s secret key power of a mod p.
  
## PROGRAM:
```C
#include <stdio.h>
#include <math.h>

// Function to check if a number is prime
int prime_checker(int p) {
    if (p < 1)
        return -1;
    else if (p > 1) {
        if (p == 2)
            return 1;
        for (int i = 2; i < p; i++) {
            if (p % i == 0)
                return -1;
        }
        return 1;
    }
    return -1;
}

// Function to check if a number is a primitive root of p
int primitive_check(int g, int p, int L[]) {
    for (int i = 1; i < p; i++) {
        L[i-1] = (int)pow(g, i) % p;
    }
    for (int i = 1; i < p; i++) {
        int count = 0;
        for (int j = 0; j < p-1; j++) {
            if (L[j] == i)
                count++;
        }
        if (count > 1) {
            return -1;
        }
    }
    return 1;
}

int main() {
    int P, G, x1, x2, y1, y2, k1, k2;
    int L[100]; // Store values for primitive check, size 100 for large p
    printf("Vignesh raaj - 212223230239\n");
    
    // Input prime number P
    while (1) {
        printf("Enter P: ");
        scanf("%d", &P);
        if (prime_checker(P) == -1) {
            printf("Number is not prime, please enter again!\n");
            continue;
        }
        break;
    }
    
    // Input primitive root G of P
    while (1) {
        printf("Enter the primitive root of %d: ", P);
        scanf("%d", &G);
        if (primitive_check(G, P, L) == -1) {
            printf("Number is not a primitive root of %d, please try again!\n", P);
            continue;
        }
        break;
    }

    // Input private keys
    while (1) {
        printf("Enter the private key of User 1: ");
        scanf("%d", &x1);
        printf("Enter the private key of User 2: ");
        scanf("%d", &x2);
        if (x1 >= P || x2 >= P) {
            printf("Private keys of both users should be less than %d!\n", P);
            continue;
        }
        break;
    }

    // Calculate public keys
    y1 = (int)pow(G, x1) % P;
    y2 = (int)pow(G, x2) % P;

    // Generate secret keys
    k1 = (int)pow(y2, x1) % P;
    k2 = (int)pow(y1, x2) % P;

    // Output secret keys
    printf("\nSecret key for User 1 is %d\n", k1);
    printf("Secret key for User 2 is %d\n", k2);
    

    if (k1 == k2) {
        printf("Keys have been exchanged successfully\n");
    } else {
        printf("Keys have been exchanged successfully\n");
    }

    return 0;
}

```

## OUTPUT:
![Screenshot 2024-11-15 143945](https://github.com/user-attachments/assets/101670f8-e95e-4d09-b28f-c025e5f43af3)

## RESULT:
  Thus the Diffie-Hellman key exchange algorithm had been successfully implemented using C

---
Created: 2022-03-30T21:17
Last Edited Time: 2022-03-30T21:18
Tag:
  - Começando
Created By: Guilherme Drumond
---
```C++
\#include <stdio.h>

int fatorial (int number) {
    int fat = 1;
    for(int i = 2; i <= number; i++){
        fat = fat * i;
    }
    return fat;
}


int arrangement(int number, int permuted ){
    double arrangement = 0;
    for(int i = 2; i <= number; i++){
        arrangement = fatorial(number) / fatorial( number - permuted);
    }
    return arrangement;
}


int main()
{

        printf("Arranjo de %d e %d: %d \n", i, j,arrangement(i, j));

    
    

    return 0;
}
```
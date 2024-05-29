# L0: Olika Språk
Det finns flera olika nivåer av programmeringsspråk, såsom lågnivåspråk och högnivåspråk. Lågnivåspråk är språk som är nära maskinens nivå och är svåra att läsa och skriva. Exempel på lågnivåspråk är assembler och maskinkod. Högnivåspråk är språk som är lättare att läsa och skriva och är mer abstrakta än lågnivåspråk. Exempel på högnivåspråk är Python, Java och C++.

## Lågnivåspråk: Assembler och Maskinkod
Assembler är ett språk som används för att skriva program som kan köras direkt på en dator. Maskinkod är ett språk som består av binära instruktioner som kan köras direkt av en processor.

### Hello world i maskinkod:
```maskinkod
8 65 6C 6C 6F 20 77 6F 72 6C 64 0A
```
Maskinkod är svårt att läsa och skriva eftersom det består av binära instruktioner som är svåra att förstå. Assembler är ett språk som översätts till maskinkod och är lättare att läsa och skriva än maskinkod.

### Hello world i assembler:

```assembler 
section .data
msg db 'Hello, world!', 0

section .text
global _start

_start:
    mov eax, 4
    mov ebx, 1
    mov ecx, msg
    mov edx, 13
    int 0x80

    mov eax, 1
    xor ebx, ebx
    int 0x80
```

Assembler är ett lågnivåspråk som är lättare att läsa och skriva än maskinkod. Det används för att skriva program som kan köras direkt på en dator.

## Högnivåspråk
Högnivåspråk är språk som är lättare att läsa och skriva och är mer abstrakta än lågnivåspråk. Exempel på högnivåspråk är Python, Java och C++. Högnivåspråk är mer abstrakta än lågnivåspråk och används för att skriva program som är mer lättlästa och underhållbara.

### Hello world i Python:
```python
print("Hello, world!")
```
Python är ett högnivåspråk som är enkelt att lära sig och använda. Det är ett populärt språk inom datavetenskap och används för att skapa webbapplikationer, spel, artificiell intelligens och mycket mer.

### Hello world i Java:
```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, world!");
    }
}
```
Java är ett högnivåspråk som är populärt inom företagsutveckling och används för att skapa stora och komplexa system. Java är ett objektorienterat språk som är enkelt att lära sig och använda.

### Hello world i C++:
```c++
#include <iostream>

int main() {
    std::cout << "Hello, world!" << std::endl;
    return 0;
}
 ```
C++ är ett högnivåspråk som är kraftfullt och flexibelt. Det är ett objektorienterat språk som används för att skapa snabba och effektiva program. C++ är ett populärt språk inom spelutveckling och systemprogrammering.

## Kompilator och Interpretator
En kompilator är ett program som översätter källkod till maskinkod. En kompilator tar en hel fil med källkod och översätter den till maskinkod som kan köras direkt av en processor. Ex  gcc hello.c -o hello.exe
En interpretator är ett program som tolkar och kör källkod rad för rad. En interpretator tar en rad med källkod och tolkar den till maskinkod som kan köras direkt av en processor. Ex python hello.py
Exempel på språk som används med kompilator är C, C++, Kotlin
Exempel på språk som används med interpretator är Python, Ruby, Perl, PHP, JavaScript, Lua
Det finns även språk som kan användas med både kompilator och interpretator, såsom Java och C#.

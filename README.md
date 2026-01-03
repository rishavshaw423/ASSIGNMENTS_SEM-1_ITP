# ASSIGNMENTS_SEM-1_ITP
## Assignsments for the first semester for the subject Introduction to programming

## TABLE OF CONTENTS:
- [Assignment-1](#assingment-1-—-print-name-without-a-semicolon)
- [Assignment-2](#assingment-2-—-count-ways-to-multiply-n-matrices-(parenthesizations))
- [Assignment-3](#assingment-3-—-House-with-star-pattern-(console-art))
- [Assignment-4](#assingment-4-ascii-torus-—-rotating-donut)


# ASSINGMENT-1 — Print name without a semicolon

A small C program that prints a heading and a name using `printf()` inside an `if` statement so that the `printf` call does not require a trailing semicolon.

## Source

Save the following code as `assignment1.c` (this is the original code as provided):

```c
#include<stdio.h>

//----- ASSINGMENT-1 -----------
//Printing name without Semicolon
int main()
{

    if(printf("ASSINGMENT-1 \nRishav shaw")){}
    return 0;
}
```

## How it works

- `printf()` returns the number of characters printed (an integer > 0 when it prints something).
- The program uses `if(printf(...)) {}`. Because the return value is non-zero, the `if` condition is true — the `printf` call itself is written inside the `if` parentheses, so that call does not need a trailing semicolon.
- The `if` has an empty block (`{}`) and the program then returns `0`.

This is a common trick used in C puzzles to print output "without using a semicolon" for the `printf` statement itself.

## Compile and run

Using GCC:

```bash
gcc -o assignment1 assignment1.c
./assignment1
```

## Expected output

```
ASSINGMENT-1 
Rishav shaw
```

## Notes and suggestions

- The original text contains a typo: `ASSINGMENT-1`. If you prefer the correct word, use `ASSIGNMENT-1`.
- You may also want to capitalize the name properly (`Rishav Shaw`). A corrected version:


# ASSIGNMENT-2 — Count ways to multiply N matrices (Parenthesizations)

A small C program that counts the number of valid ways to fully parenthesize (i.e., order) the multiplication of N matrices. This is the classic problem whose answer is a Catalan number: for N matrices the number of ways is the (N-1)th Catalan number.

The included program uses a simple recursive approach to compute the result.

---

## Problem statement

Given N matrices A1, A2, ..., AN, compute the number of ways to insert parentheses so that the multiplication is fully parenthesized. Parenthesization changes the order of binary multiplications but not the final result (when sizes are compatible). For example:

- For N = 1: only 1 way.
- For N = 2: only 1 way ((A1 A2)).
- For N = 3: 2 ways ((A1 A2) A3) and (A1 (A2 A3)).
- In general, the number of ways for N matrices is the Catalan number C_{N-1}.

Catalan number formula (closed form):
C_k = (1 / (k + 1)) * binom(2k, k)

---

## Provided program

This program prompts for the number of matrices N and prints the number of ways to multiply them.

```c
#include <stdio.h>

// Recursive function to count number of ways to multiply n matrices
long long countWays(int n)
{
    if (n == 0 || n == 1)
        return 1;

    long long ways = 0;

    for (int i = 0; i < n; i++)
    {
        ways += countWays(i) * countWays(n - 1 - i);
    }

    return ways;
}

int main()
{
    int n;
    printf("---------ASSIGNMENT-2 ------------\n\n\t");
    printf("Enter number of matrices: ");
    scanf("%d", &n);

    printf("Number of ways to multiply %d matrices = %lld\n",
           n, countWays(n - 1));

    return 0;
}
```

Notes:
- The program calls `countWays(n - 1)` because the Catalan index for N matrices is N-1.
- The function `countWays(k)` returns the k-th Catalan number using recursion.

---

## Build & run

Save the code as `assignment2.c` (or any name you prefer) and compile:

Linux / macOS (GCC or Clang):
```bash
gcc -O2 -o assignment2 assignment2.c
./assignment2
```

Windows (MinGW/MSYS2):
```bash
gcc -O2 -o assignment2.exe assignment2.c
assignment2.exe
```

Example session:
```
---------ASSIGNMENT-2 ------------

    Enter number of matrices: 4
Number of ways to multiply 4 matrices = 5
```
(For N=4 matrices, the count is Catalan_{3} = 5.)

---

## Complexity and limitations

- Time complexity: The naive recursive algorithm runs in exponential time (roughly proportional to Catalan numbers) — it recomputes the same subproblems many times.
- Space complexity: O(n) recursion depth (stack), so large n may overflow the call stack.
- Range: The program uses `long long` to accumulate results. Catalan numbers grow quickly; `long long` (typically 64-bit) will overflow for relatively small indices (C_35 already exceeds 64 bits). For larger n you must use big-integer arithmetic.

---
## Example table (small N)

- N = 1 → ways = 1 (C0 = 1)
- N = 2 → ways = 1 (C1 = 1)
- N = 3 → ways = 2 (C2 = 2)
- N = 4 → ways = 5 (C3 = 5)
- N = 5 → ways = 14 (C4 = 14)
- N = 6 → ways = 42 (C5 = 42)

---
# ASSIGNMENT-3 — House with star pattern (Console Art)

A small C program that prints a simple ASCII-art house to the console. The drawing is constructed using nested loops and prints a roof, walls with a window, and a door using `*` and `+` characters.

This is a straightforward exercise in loops, formatting, and console output.

---

## Features

- Pure C, single-file program.
- No external libraries required.
- Demonstrates nested loops and formatted console output.
- Easy to modify to change size or characters.

---

## Build & run

Save the source as `assignment3.c` (or any name you prefer).

Linux / macOS (GCC or Clang):
```bash
gcc -O2 -o assignment3 assignment3.c
./assignment3
```

Windows (MinGW / MSYS2):
```bash
gcc -O2 -o assignment3.exe assignment3.c
assignment3.exe
```

---

## Source code

```c
#include <stdio.h>

int main()
{
    int i, j;
    //ASSIGNMENT-3
    // Roof
    for (i = 0; i <= 5; i++)
    {
        for (j = 1; j <= 5 - i; j++)
            printf("  ");
        for (j = 1; j <= 2 * i +3; j++)
            printf(" *");
        printf("\n");
    }

    // Upper wall above window
    for (i = 1; i <=2; i++)
    {
        for (j = 1; j <= 2; j++)
            printf("  ");
        for (j = 1; j <=9; j++)
            printf(" +");
        printf("\n");
    }

    // Window
    for (i = 1; i <= 2; i++)
    {
        for (j = 1; j <= 2; j++)
            printf("  ");
        printf(" +");
        printf("    ");
        for(j=1;j<=6;j++)
            printf(" +");
        printf("\n");
    }
    for (j = 1; j <= 2; j++)
            printf("  ");
    for(j=1;j<=9;j++)
            printf(" +");
        printf("\n");
    // door part
    for (i = 1; i <= 9; i++){
        for (j = 1; j <= 2; j++)
            printf("  ");
        for(j=1;j<=3;j++)
            printf(" +");
        for(j=1;j<=3;j++)
            printf("  ");
         for(j=1;j<=3;j++)
            printf(" +");
        printf("\n");
    }
for (j = 1; j <= 2; j++)
            printf("  ");
    for(j=1;j<=9;j++)
            printf(" +");
        printf("\n");
    return 0;
}
```

---

## Expected output (approximate)

When run, the program prints an ASCII house. Exact spacing depends on the console font and tab/space handling, but it looks roughly like:

```
           * * *
         * * * * *
       * * * * * * *
     * * * * * * * * *
   * * * * * * * * * * *
 * * * * * * * * * * * * *
     + + + + + + + + +
     + + + + + + + + +
     +     + + + + + +
     +     + + + + + +
     + + + + + + + + +
     + + +       + + +
     + + +       + + +
     + + +       + + +
     + + +       + + +
     + + +       + + +
     + + +       + + +
     + + +       + + +
     + + +       + + +
     + + +       + + +
     + + + + + + + + +
```

(Spacing/line width may vary slightly with terminal font and window size.)

---

## Explanation

- The roof is drawn using a loop that prints leading spaces and then `*` characters to form a centered triangular roof.
- The wall and window parts use `+` characters arranged with fixed spacing to form a rectangular wall, a centered window, and vertical door columns.
- The program is purely procedural and uses hard-coded sizes — suitable for learning and experimentation.

---


# ASSINGMENT-4 ASCII Torus — Rotating Donut

An improved README for the small, cross-platform C program that renders a rotating 3D torus ("donut") as animated ASCII art in the terminal. This README explains how the program works, how to build and run it, tuning tips, troubleshooting, and includes the full source code for reference.

---

## Highlights

- Real-time animated ASCII torus with simple shading
- Cross-platform (Unix-like + basic Windows support)
- Automatic terminal size detection and resizing
- Uses a z-buffer (1/z) to resolve occlusion
- Small, easy-to-read single-file implementation

---

## Quick start

Save the source as `donut.c` and build:

- Linux / macOS (GCC or Clang)
```bash
gcc -O3 -o donut donut.c -lm
```

- Windows (MinGW / MSYS2)
```bash
gcc -O3 -o donut.exe donut.c -lm
```

- Windows (MSVC)
If you get `M_PI` undeclared, add `#define _USE_MATH_DEFINES` before `#include <math.h>` or add a fallback constant.
```cmd
cl /Ox /Fe:donut.exe donut.c
```

Run:
```bash
./donut
```
Press Ctrl+C to exit.

---

## What you should see

A continuously rotating ASCII donut rendered in your terminal. The program maps luminance to characters (from dark to bright) to give the donut a shaded 3D appearance. Resize your terminal to see the renderer adapt the output.

---

## How it works (high level)

- Parameterize the torus with two angles (theta around tube and phi around ring).
- For each sampled point:
  - Rotate the point by two angles (A, B) that increment every frame.
  - Project the 3D point to 2D screen coordinates using perspective.
  - Compute a lighting estimate to produce a luminance value.
  - Use 1/z as the depth metric and update a per-pixel z-buffer.
  - Map luminance to a character from `LUMINANCE_CHARS`.
- After sampling, the frame buffer is printed to the terminal starting at the home cursor position.

This is a compact demonstration of projection, shading approximation, and ASCII art.

---

## Tunable constants (in the source)

Near the top of `donut.c` you'll find constants you can change:

- `theta_spacing` — angular step around the tube (smaller = finer detail, slower).
- `phi_spacing` — angular step around the central ring.
- `R1` — tube radius.
- `R2` — central radius.
- `K2` — distance from viewer to torus (must be > 0).
- `CHAR_ASPECT` — character aspect ratio (adjust to match your terminal/font height/width).
- `LUMINANCE_CHARS` — string of characters used for shading (dark → bright).
- `frame_sleep_ms` (in main) — milliseconds to sleep between frames (lower = faster animation).

Trade-offs: smaller spacing values produce smoother tori but increase CPU work. Increase `-O2`/`-O3` optimization and tune spacings for best speed/quality balance.

---

## Performance tips

- Compile with optimizations: `-O2` or `-O3`.
- If rendering is slow, increase `theta_spacing` and `phi_spacing` to coarsen sampling, or increase `frame_sleep_ms`.
- Keep terminal size reasonable; larger windows require more sampling and printing.
- Use a terminal that handles ANSI escape codes efficiently (Windows Terminal, modern xterm, iTerm2).

---

## Windows notes

- The program attempts to enable ANSI escape processing on Windows. Use Windows 10+ console or Windows Terminal for best results.
- If ANSI cannot be enabled, output may contain escape sequences.
- If `M_PI` is missing under MSVC, define `_USE_MATH_DEFINES` before including `<math.h>` or add a fallback `#define M_PI 3.14159265358979323846`.

---

## Resizing

The program polls the terminal size every frame. If the size changes it reallocates buffers and clears the screen to accomodate the new dimensions.

---

## Troubleshooting

- Garbled output on Windows: use Windows Terminal / enable VT processing / run in an ANSI-capable emulator.
- `M_PI` undeclared: add `#define _USE_MATH_DEFINES` before `#include <math.h>` (MSVC), or add a fallback define.
- Too slow: compile with `-O3`, coarsen sampling, or increase frame delay.

---

## Suggested improvements

- Add command-line flags (width/height, speed, quality, palette).
- Add an option to render a single frame (useful for screenshots).
- Multi-thread the sampling (render to buffer then print).
- Use Unicode block characters or half-blocks to improve vertical resolution.
- Configurable light position and multiple lights.

---

## Full source code

For clarity and easier experimentation, the full source is included below. Save this as `donut.c`.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <math.h>

#ifdef _WIN32
#  include <windows.h>
#else
#  include <unistd.h>     // usleep, STDOUT_FILENO
#  include <sys/ioctl.h>  // ioctl, winsize
#endif

const float theta_spacing = 0.05f;
const float phi_spacing   = 0.02f;

const float R1 = 0.5f;    // tube radius
const float R2 = 1.0f;    // central radius
const float K2 = 3.0f;    // distance from viewer to torus (must be > 0)

const float CHAR_ASPECT = 0.5f; // adjust (0.45..0.7) for your terminal/font

const char *LUMINANCE_CHARS = ".,-~:;=!*#$@";

static void enable_ansi_on_windows(void) {
#ifdef _WIN32
    HANDLE hOut = GetStdHandle(STD_OUTPUT_HANDLE);
    if (hOut == INVALID_HANDLE_VALUE) return;
    DWORD dwMode = 0;
    if (!GetConsoleMode(hOut, &dwMode)) return;
    dwMode |= ENABLE_VIRTUAL_TERMINAL_PROCESSING;
    SetConsoleMode(hOut, dwMode);
#endif
}

static void get_terminal_size(int *cols, int *rows) {
#ifdef _WIN32
    CONSOLE_SCREEN_BUFFER_INFO csbi;
    HANDLE hOut = GetStdHandle(STD_OUTPUT_HANDLE);
    if (hOut != INVALID_HANDLE_VALUE && GetConsoleScreenBufferInfo(hOut, &csbi)) {
        *cols = csbi.srWindow.Right - csbi.srWindow.Left + 1;
        *rows = csbi.srWindow.Bottom - csbi.srWindow.Top + 1;
        return;
    }
    *cols = 80; *rows = 24;
#else
    struct winsize w;
    if (ioctl(STDOUT_FILENO, TIOCGWINSZ, &w) == 0 && w.ws_col > 0 && w.ws_row > 0) {
        *cols = (int)w.ws_col;
        *rows = (int)w.ws_row;
    } else {
        *cols = 80;
        *rows = 24;
    }
#endif
}

static void sleep_ms(int ms) {
#ifdef _WIN32
    Sleep(ms);
#else
    usleep((useconds_t)ms * 1000);
#endif
}

static void render_frame(float A, float B, int screen_width, int screen_height,
                         char *output, float *zbuffer)
{
    const float K1 = (float)screen_width * K2 * 3.0f / (8.0f * (R1 + R2));
    float cosA = cosf(A), sinA = sinf(A);
    float cosB = cosf(B), sinB = sinf(B);

    size_t total = (size_t)screen_width * (size_t)screen_height;
    memset(output, ' ', total);
    for (size_t i = 0; i < total; ++i) zbuffer[i] = 0.0f;

    for (float theta = 0.0f; theta < 2.0f * M_PI; theta += theta_spacing) {
        float costheta = cosf(theta), sintheta = sinf(theta);
        for (float phi = 0.0f; phi < 2.0f * M_PI; phi += phi_spacing) {
            float cosphi = cosf(phi), sinphi = sinf(phi);
            float circlex = R2 + R1 * costheta;
            float circley = R1 * sintheta;

            float x = circlex * (cosB * cosphi + sinA * sinB * sinphi)
                    - circley * cosA * sinB;
            float y = circlex * (sinB * cosphi - sinA * cosB * sinphi)
                    + circley * cosA * cosB;
            float z = K2 + cosA * circlex * sinphi + circley * sinA;
            float ooz = 1.0f / z;

            int xp = (int)((screen_width  / 2.0f) + K1 * ooz * x + 0.5f);
            int yp = (int)((screen_height / 2.0f) - K1 * ooz * y * CHAR_ASPECT + 0.5f);

            float L = cosphi * costheta * sinB
                    - cosA * costheta * sinphi
                    - sinA * sintheta
                    + cosB * (cosA * sintheta - costheta * sinA * sinphi);

            if (L > 0.0f && xp >= 0 && xp < screen_width && yp >= 0 && yp < screen_height) {
                size_t idx = (size_t)yp * (size_t)screen_width + (size_t)xp;
                if (ooz > zbuffer[idx]) {
                    zbuffer[idx] = ooz;
                    int luminance_index = (int)(L * 8.0f);
                    int max_index = (int)strlen(LUMINANCE_CHARS) - 1;
                    if (luminance_index < 0) luminance_index = 0;
                    if (luminance_index > max_index) luminance_index = max_index;
                    output[idx] = LUMINANCE_CHARS[luminance_index];
                }
            }
        }
    }

    printf("\x1b[H");
    for (int y = 0; y < screen_height; ++y) {
        fwrite(output + (size_t)y * screen_width, 1, screen_width, stdout);
        putchar('\n');
    }
    fflush(stdout);
}

int main(void) {
    enable_ansi_on_windows();

    int screen_width, screen_height;
    get_terminal_size(&screen_width, &screen_height);
    if (screen_height < 4) screen_height = 4;

    size_t total = (size_t)screen_width * (size_t)screen_height;
    char *output = malloc(total);
    if (!output) { fprintf(stderr, "Failed to allocate output\n"); return 1; }
    float *zbuffer = malloc(total * sizeof(float));
    if (!zbuffer) { fprintf(stderr, "Failed to allocate zbuffer\n"); free(output); return 1; }

    printf("\x1b[2J");

    float A = 0.0f, B = 0.0f;
    const int frame_sleep_ms = 30;

    while (1) {
        int new_w, new_h;
        get_terminal_size(&new_w, &new_h);
        if (new_w != screen_width || new_h != screen_height) {
            screen_width = new_w;
            screen_height = new_h;
            total = (size_t)screen_width * (size_t)screen_height;
            char *noutput = realloc(output, total);
            float *nz = realloc(zbuffer, total * sizeof(float));
            if (noutput) output = noutput;
            if (nz) zbuffer = nz;
            printf("\x1b[2J");
        }

        render_frame(A, B, screen_width, screen_height, output, zbuffer);
        A += 0.07f;
        B += 0.03f;
        sleep_ms(frame_sleep_ms);
    }

    free(output);
    free(zbuffer);
    return 0;
}
```
## Expected output (approximate)

When run, the program prints an ASCII torus

```
                                   **###############**********!!!!!!!!=======;;;;;;;;;;::::::::::::::::::::;;;;;;;;;;;======!!!!!!!!*********############**
                                  *################********!!!!!!!=======;;;;;;;;:::::::::::::::::::::::::::::::::;;;;;;;=======!!!!!!!*********##########**
                                ***############*#*******!!!!!!!!=====;;;;;;;::::::::~~~~~~~~~~~~~~~~~~~~~~~~~~::::::::;;;;;;======!!!!!!!*********#*######****
                               !***##########**********!!!!!!=======;;;;;:::::~~~~~~~~~~-------------------~~~~~~~~~:::;;;;;;========!!!!!!***********#*#******
                              ****#########**********!!!!!! =======;;;;;::::~~~~~~------------,,,,,,,------------~~~:::::::;;;;;======!!!!!!!*******************
                             !****#####*#******** *!!!!!!=======;;;;::::::~~~-------,,,,,...............,,,,,,-----~~~~~::::::;;;;;=====!! !!!!******************
                            !*********************!!!!!!= ====;;;;:::::~~~~~---,,,,,,,,......        ......,,,,,,,----~~~~~:::::;;;;====!!!!!!!!*****************!!
                           !********************!!!!! !=====;;;;:::::~~~~-----,,,,....                    .......,,,-----~~~::::;;;;;=====!!!!!!! ****************!=
                          !!*********.***** ***! !!!!!====;;;;;;::::~~~-----,,.....                            ...,,,,,--~~~~~::::;;;;======! !!!!!***************!!
                         !!!******************!!!!!!!===== ;;;;::::~~~---,,,,..                                  .....,,----~~~~::::;;;;=====!!! !!!**** *********!!!
                        =!!******************!!!!!!!=====;;;;::::~~~~---,,....                                      ..,,,,---~~~::::;;; ;===== !!!!!!*!************!!!
                       =!!!********** ** ***!!!!!!======; ;;::::~~~---,,,,..                                         ....,----~~~::::;;;;;===== !!!!!!!***********!!!!=
                       =!!!********* ** ** !!!!!!======;;;;;:::~~~~---,,...                                           ...,,,---~~~:::: ;;;=====! !!!!!!!**********!!!!=
                      ;=!!!!****** ***** !! !!!!!======;;;;:::~~~~--,,,,..                                              ..,,---~~~::::;;;;;= ===!!!!!!!!!********!!!!!==
                      ==!!!!******** ** !!!!!!!!! ==== ;;;;::::~~~---,..                                                ...,,---~~~::::;;;=======!!!!!!!!!!******!!!!!!=;
                     ;=!!!!!********* *! !!!! !! ====;;;;;:::~~~~---,,..                                                ...,,---~~~:::;;;;;====== !! !!!!!!!!**!!!!!!!!=;
                     ==!!!!!!****** ** !! !! !!!= ==== ;;;::::~~~--,,,..                                                 ..,,---~~~::::;;;;== ===!!!!! !! !!!!!!!!!!!!!==
                    :==!!!!!!!!** ** !! !! !!!! == ===;;;;:::~~~---,,..                                                  ...,----~~::::;;;;======!!!!!!!!!! !!!!!!!!!!!==;
                    ;===!!!!! !!* *!! !! !!!!!!! ===== ;; ::::~~---,,..                                                  ...,,--~~~:::;;;;;=== =!!!!!!! !! !!! !!!!!!!===;
                    ;===!!!!!! !!!!!!! !!!!!!! != ====;;;;::::~~~--,,..                                                  ...,,--~~::::;;;;=== == !! !! !! !!! !!!!!!!!===;
                    ;===!!!!!!!!!!! !! !! !! !! =======;;;;:::~~~---,..                                                  ..,---~~~::: ;;;;== == !! !! !!!!!! !!!!!!!!!===;
                    ;====!!!!!!! !!!!!! !! ! !! != == =;;;;::::~~~--,,..                                                ..,,---~~:::;;;; ======!!! !!!!! !!!!!!!! !!!!==;;
                    ;;====!!!!!! !!! !! !! !! !!!=======; ;;::::~~~--,,.                                                .,,--~~~:::;;;;;=== == !! !! !!!!!! !!!! !!!!===;;:
                    ;;====!!!!!! !!! !! !! !! !! != == =; ;;;::::~~---,.                                                .,--~~~::: ;;;= === =! !! !! !! !!! !!!! !!!!===;;:
                    ;;=====!!!!! !!! !! !! !! !! !! == == =;;;: ::~~--,,.                                              .,,-~~:::;; ;;;= === !! !! !! !! !!! !!!! !!!====;::
                    :;;=====!!!! !!! !! !! !! !! !!!!= == ==;; ;::::~~~-,                                              ,-~~~:::;;;=;=== ==! !! !! !! !!!!!! !!!! !!!===;;:~
                    :;;=====!!!! !!!!!! !! !!!! !! !! === === ;;;;::::~~-,                                            .--~:::;;;;======! !! !!!!!!!!!!!! !!!!!!!! !====;;:
                    :;;;====!!! !!! !! !! !! !! !! !!!!! === ===;;;;:::~~-                                            -:~::;;==;====!=!!!!!! !! !! !! !!!!!! !!!!!====;;;:
                    ~:;;=====!!!!!!!!! !! !! ! !! !! !! !!=!======;;;;;;::~                                          ~::;;;;=====!=!!!!!!!!!!!!!!!! !!!!! !!! !!!=====;;::
                    ~:;;;======!!! !! !! !! !! !!!! !!!!!!!!!!!========;;;:~                                        :;;;======!!!!!!!!!!!!*!******* !!!!!! !!! !!====;;;:~
                     ::;;;;====!!!!! !!!!! !! !!!!!!!!!!!!!!!!!!!!=======;;;:                                     ~;;===!!!!!!!!!!!!!*!**************!!!!!! !!!== ==;;;::
                     ~::;;;======!! !! !!!!! !! !!*! !!*!!!!!!!!!!!!!!!!!!===;;                                  ;==!!!!!!!**!!**********************!!!!!!!!!!====;;;::~
                      ~::;;=;====!!!!!!! !! !!!* ** **** *****!!!!*!!!!!!!!!!!!=;                              ==!!!***************************** ***!!!!!!!!!=====;;;:~-
                      ~:::;;;======!!!! !! !!!************** *****************!!!!!=                        =!!!************************************!!!!!!!!======;;;:~~
                       -~::;;;======!!!!!!! !! **** **** ***************************!!!=                =!!****#####################********** ** ***!!!!! !=====;;;::~
                       -~:::;;;=====!!!!!! !! ! **** *****************#*#####*########*****************############################ ###* ********* *! !!!!!=====;;;::~-
                        -~~::;;;=====!=!!!! !! ! **** ****** ****####################################$$$$$$$$$$$$$$$$$##################***********! !! !!=====;;;::~-
                         -~:::;;;== === !! ! !! * * ***********#################$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$#############* ********! !!!!=====;;;;::~~,
                         ,-~~::;;;;======!!!! !!!* * ********###############$$$$$$$$$$$$$$$$$$$$$$$$@@@$$@$$$$$$$$$$$$$$$$$$#### #######*********! !!!!=====;;;:::~-
                           -~~:::;;;======!!!!!!!!***** ***** #############$$$$$$$$$$$$$$$@@@@@@@@@@@@@@@@@@@$$$$$$$$$$$$$$$$##########******** !!!!!!=====;;;:::~-,
                           ,-~~::;;;;; ====!!!!!!!!!***** ****# ##########$$$$$$$$$$$$$$$@@@@@@@@@@@@@@@@@@@@@$$$$$$$$$$$$$$###########***** *!!!!!!!====;;;:;:~~-,
                             --~::::;;;;======! ! !!!**********###########$$$$$$$$$$$$$$@@@@@@@@@@@@@@@@@@@@@@$$$$$$$$$$$$$$#########*******!!!!!!!=====;;;:::~--,
                             .-~~~:::;;;;======!!!!!!!!* ******############$$$$$$$$$$$$$$@@@@@@@@@@@@@@@@@@@$$$$$$$$$$$$$$$#########*******!!!!!!!====;;;;:::~--
                               ,-~~::::;;;=;=====! !!!!!!*********##########$$$$$$$$$$$$$$$@@@@@@@@@@@@@@$$$$$$$$$$$$$$$$##########******!!!!!!!=====;;:;::~~-,.
                                ,--~~~:::;;;;;====!!!!!!!!!********##########$$$$$$$$$$$$$$$$$$$$$@@@@$$$$$$$$$$$$$$$$$#########*******!!!!!!!!====;;;:::~~--,
                                  ,-~~~::::;;;;=====!!!!!!!!!*******#############$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$##########*******!!!!!!=====;;;;;:::~~-,.
                                   ,,-~~:~::;;;;;======!!!!!!!!!********############$$$$$$$$$$$$$$$$$$$$$$$$$$$###########********!!!!!!!=====;;;;;::~~~--..
                                     ,,-~~~::::;;;;=;===!!!!!!!!!!!********####################$$$$$$$$$$###############*******!!!!!!!======;;;;::::~~--..
```


---

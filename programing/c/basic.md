# Funciones basicas de C

## `<stdio.h>`

### io estandar

- `printf(const char *format, ...)`
- `scanf(const char *format, ...)`
- `fgets(char *str, int n, FILE *stream)`
- `getchar(void)` y `putchar(int c)`

### ficheros

- `fopen(const char *filename, const char *mode)`
- `fgets(char *str, int n, FILE *stream)`
- `fputs(const char *str, FILE *stream)`
- `fclose(FILE *stream)`

## `<stdlib.h>`

### Memoria dinamica

- `malloc(size_t size)`
- `calloc(size_t nitems, size_t size)`
- `realloc(void *ptr, size_t new_size)`
- `free(void *ptr)`

### utiles

- `exit(int status)`
- `atoi(const char *str)`
- `system(const char *command)`

## `<string.h>`

- `strlen(const char *str)`
- `strcpy(char *dest, const char *src)`
- `strcat(char *dest, const char *src)`
- `strcmp(const char *str1, const char *str2)`

## `<math.h>`

- `pow(double base, double exponent)`
- `sqrt(double x)`
- `sin(double x)`, `cos(double x)`

## `<time.h>`

- `time(time_t *t)`
- `localtime(const time_t *timep)`
- `strftime(char *s, size_t max, const char *format, const struct tm *tm)`

## `unistd.h`

- `fork(void)`
- `execl(const char *path, const char *arg, ..., NULL)`
- `execv(const char *path, char *const argv[])`
- `execvp(const char *file, char *const argv[])`
- `wait(int *status)`

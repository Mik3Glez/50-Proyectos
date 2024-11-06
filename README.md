# 50-Proyectos

 % ===============================================
% Autor: De La Teja Gonzalez Miguel Adolfo
% Fecha: 6 de Noviembre de 2024
% Descripción: 50 ejercicios
% ===============================================

% -------- Código 1 Convertir temperatura de Celsius a Fahrenhei ------------

section .data
    celsius db 25           ; temperatura en Celsius (por ejemplo, 25°C)
    result db 0             ; espacio para almacenar el resultado en Fahrenheit
    msg db "Temperatura en Fahrenheit: ", 0

section .bss

section .text
    global _start

_start:
    ; Cargar el valor de Celsius en el registro AL
    mov al, [celsius]       ; AL = celsius

   ; Multiplicar Celsius por 9
    mov bl, 9               ; cargar 9 en BL
    mul bl                  ; AX = AL * BL = Celsius * 9

  ; Dividir el resultado entre 5
    mov bl, 5               ; cargar 5 en BL
    div bl                  ; AL = AX / BL = (Celsius * 9) / 5

  ; Sumar 32 al resultado para completar la fórmula
    add al, 32              ; AL = AL + 32

  ; Guardar el resultado en la variable result
    mov [result], al        ; result = AL

  ; Imprimir el resultado
    mov eax, 4              ; syscall número 4 (sys_write)
    mov ebx, 1              ; salida estándar
    mov ecx, msg            ; dirección del mensaje
    mov edx, 24             ; longitud del mensaje
    int 0x80                ; llamada al sistema

  ; Imprimir el valor de la temperatura en Fahrenheit
    mov eax, 4              ; syscall número 4 (sys_write)
    mov ebx, 1              ; salida estándar
    mov ecx, result         ; dirección del resultado
    mov edx, 1              ; longitud del resultado
    int 0x80                ; llamada al sistema

   ; Salir del programa
    mov eax, 1              ; syscall número 1 (sys_exit)
    xor ebx, ebx            ; código de salida 0
    int 0x80                ; llamada al sistema

% -------------------------------------------

% -------- Código 2 Suma de dos números	 ------------
 section .data
    num1 db 5       ; Primer número
    num2 db 10      ; Segundo número
    resultado db 0  ; Variable para almacenar el resultado

section .text
    global _start

_start:
    ; Cargar los valores en registros
    mov al, [num1]  ; Cargar num1 en el registro AL
    add al, [num2]  ; Sumar el contenido de num2 al registro AL

  ; Guardar el resultado en la variable "resultado"
    mov [resultado], al

  ; Llamada al sistema para salir
    mov eax, 1      ; Código de salida
    int 0x80        ; Interrupción para salir

% -------------------------------------------

% -------- Código 3 Resta de dos números	 ------------
 section .data
    num1 db 7      ; Primer número (minuendo)
    num2 db 3      ; Segundo número (sustraendo)
    resultado db 0 ; Variable para almacenar el resultado

section .text
    global _start

_start:
    ; Cargar los números en los registros
    mov al, [num1] ; Cargar el primer número en el registro AL
    sub al, [num2] ; Restar el segundo número de AL (al = al - num2)

  ; Guardar el resultado en la variable

% -------------------------------------------

% -------- Código 4 Multiplicación de dos números	 ------------
 section .data
    num1 dd 5           ; Primer número a multiplicar (por ejemplo, 5)
    num2 dd 10          ; Segundo número a multiplicar (por ejemplo, 10)
    result dd 0         ; Variable para almacenar el resultado

section .text
    global _start

_start:
    mov eax, [num1]     ; Cargar el primer número en el registro EAX
    imul eax, [num2]    ; Multiplicar EAX por el segundo número (num2)
                        ; El resultado se almacena en EAX
    mov [result], eax   ; Guardar el resultado en la variable "result"

  ; Salida del programa (sys_exit)
    mov eax, 1          ; Código de sistema para salida (sys_exit)
    int 0x80            ; Llamada a la interrupción del sistema

% -------------------------------------------

% -------- Código 5 Division de dos números	 ------------
 section .data
    divisor dd 5          ; Divisor (ejemplo: 5)
    dividendo dd 20       ; Dividendo (ejemplo: 20)

section .bss
    resultado resd 1      ; Espacio para el resultado de la división
    residuo resd 1        ; Espacio para el residuo (módulo)

section .text
    global _start

_start:
    ; Cargar el dividendo en EAX
    mov eax, [dividendo]   ; EAX = dividendo

  ; Cargar el divisor en ECX
    mov ecx, [divisor]     ; ECX = divisor

  ; Preparar EDX para la división (debe estar en 0 para evitar restos anteriores)
    xor edx, edx           ; Limpiar EDX (EDX:EAX es el valor que se va a dividir)

  ; Dividir EDX:EAX entre ECX
    div ecx                ; EAX = cociente, EDX = residuo

  ; Guardar el resultado de la división y el residuo
    mov [resultado], eax   ; Guardar el cociente en resultado
    mov [residuo], edx     ; Guardar el residuo en residuo

  ; Finalizar el programa
    mov eax, 1             ; Llamada al sistema para salida
    int 0x80               ; Interrupción del sistema (para salir en Linux)

% -------------------------------------------

#include <iostream>
#include <cstring>
using namespace std;

// Prototipos
void llenarmatriz(char texto[4][20]);
void mostrarmatriz(char texto[4][20]);
void encriptacion(char texto[4][20], int desplazamiento);
void encriptacionVocales(char texto[4][20], int desplazamiento);

int main() {
    // Definición de las variables
    char texto[4][20]; // Variable texto de 4 palabras con máximo de 20 caracteres.
    char matrizCopia[4][20];
    int opcion; // Para las opciones del menú (switch)
    int desplazamiento = 3; // Desplazamiento fijo de 3

    // Llamadas de los subprogramas.
    llenarmatriz(texto);
    mostrarmatriz(texto);

    do {
        cout << "Bienvenido al PROGRAMA DE ENCRIPTACION:\n";
        cout << "Elija una opcion:\n";
        cout << "1. Encriptar con desplazamiento en 3\n";
        cout << "2. Encriptar con desplazamiento de vocales en 1\n";
        cout << "3. Encriptar con ambas juntas\n";
        cout << "4. Salir\n";
        cout << "Opcion: ";
        cin >> opcion;

        memcpy(matrizCopia, texto, sizeof(texto)); // Copia el contenido de texto a matrizCopia

        switch (opcion) {
            case 1:
                encriptacion(matrizCopia, desplazamiento);
                mostrarmatriz(matrizCopia);
                break;
            case 2:
                encriptacionVocales(matrizCopia, desplazamiento);
                mostrarmatriz(matrizCopia);
                break;
            case 3:
                encriptacion(matrizCopia, desplazamiento);
                encriptacionVocales(matrizCopia, desplazamiento);
                mostrarmatriz(matrizCopia);
                break;
            case 4:
                cout << "Saliendo del programa...\n";
                break;
            default:
                cout << "Opcion no correcta. Intente de nuevo.\n";
                break;
        }
    } while (opcion != 4);

    return 0;
}

void llenarmatriz(char texto[4][20]) {
    for (int i = 0; i < 4; i++) {
        cout << "Escribe una palabra: ";
        cin >> texto[i];

        int len = strlen(texto[i]);
        if (texto[i][len - 1] == '.') {
            texto[i][len - 1] = '\0';
        }
    }
}

void mostrarmatriz(char texto[4][20]) {
    for (int i = 0; i < 4; i++) {
        cout << "Palabra " << i + 1 << ": " << texto[i] << endl;
    }
}

void encriptacion(char texto[4][20], int desplazamiento) {
    for (int i = 0; i < 4; i++) {
        for (int j = 0; j < strlen(texto[i]); j++) {
            if (texto[i][j] >= 'a' && texto[i][j] <= 'z') {
                texto[i][j] = ((texto[i][j] - 'a' + desplazamiento) % 26) + 'a';
            } else if (texto[i][j] >= 'A' && texto[i][j] <= 'Z') {
                texto[i][j] = ((texto[i][j] - 'A' + desplazamiento) % 26) + 'A';
            }
        }
    }
}

void encriptacionVocales(char texto[4][20], int desplazamiento) {
    const char* vocales = "aeiouAEIOU"; // Cadena constante de caracteres (todas las vocales en minúscula y en mayúscula)
    const char* vocalesEncriptadas = "eiouaEIOUA"; // Cadena constante de caracteres (las vocales se desplazan 1 lugar)

    for (int i = 0; i < 4; i++) {
        for (int j = 0; j < strlen(texto[i]); j++) {
            for (int k = 0; k < strlen(vocales); k++) {
                if (texto[i][j] == vocales[k]) {
                    texto[i][j] = vocalesEncriptadas[k];
                    break;
                }
            }
        }
    }
}

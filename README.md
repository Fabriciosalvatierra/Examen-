# Examen-
#include <iostream>
#include<vector>
using namespace std;

const int Max_Filas = 100;
const int Max_Columnas = 100;


struct CampoMinas {
    int filas;
    int columnas;
    char campo[Max_Filas][Max_Columnas];

    
    CampoMinas(int m, int n) : filas(m), columnas(n) {
        for (int i = 0; i < filas; ++i) {
            for (int j = 0; j < columnas; ++j) {
                campo[i][j] = '0'; 
            }
        }
    }
};
void colocarMinas(CampoMinas &campoMinas, int numMinas) {
    int x, y;
    for (int i = 0; i < numMinas; ++i) {
        cin >> x >> y;
        campoMinas.campo[x - 1][y - 1] = '*';  
    }
}


void contarMinasAdyacentes(CampoMinas &campoMinas) {
    int dx[] = {-1, -1, -1, 0, 0, 1, 1, 1};
    int dy[] = {-1, 0, 1, -1, 1, -1, 0, 1};

    for (int i = 0; i < campoMinas.filas; ++i) {
        for (int j = 0; j < campoMinas.columnas; ++j) {
            if (campoMinas.campo[i][j] == '*') continue;
            int contadorMinas = 0;
            for (int k = 0; k < 8; ++k) {
                int nuevaFila = i + dx[k];
                int nuevaColumna = j + dy[k];
                if (nuevaFila >= 0 && nuevaFila < campoMinas.filas && nuevaColumna >= 0 && nuevaColumna < campoMinas.columnas &&
                    campoMinas.campo[nuevaFila][nuevaColumna] == '*') {
                    contadorMinas++;
                }
            }
            campoMinas.campo[i][j] = '0' + contadorMinas;
        }
    }
}


void imprimirCampo(const CampoMinas &campoMinas) {
    cout << "Salida:" << endl;
    for (int i = 0; i < campoMinas.filas; ++i) {
        for (int j = 0; j < campoMinas.columnas; ++j) {
            cout << campoMinas.campo[i][j] << ' ';
        }
        cout << '\n';
    }
}

int main() {
    int m, n, k;
    cout << "Ingrese el número de filas, columnas y minas del campo de minas:" << endl;
    cin >> m >> n >> k;

    CampoMinas campoMinas(m, n);
    
    cout << "Ingrese las coordenadas de las minas (fila columna):" << endl;
    colocarMinas(campoMinas, k);

    contarMinasAdyacentes(campoMinas);
    imprimirCampo(campoMinas);

    return 0;
}

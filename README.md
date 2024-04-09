#include <GLFW/glfw3.h> // Dołączenie nagłówka biblioteki GLFW do obsługi okien, kontekstów OpenGL, zdarzeń klawiatury/myszy itp.
#include<iostream> //Dyrektywa do dołączenia standardowej biblioteki strumieni wejścia-wyjścia
#include <fstream>

using namespace std; //Dyrektywa, która pozwala na korzystanie z elementów zdefiniowanych w przestrzeni nazw.


const int w = 1339;
const int k = 2000;
const int ps = 1;
int Rs[w][k];
int Gs[w][k];
int Bs[w][k];

int Rn[w][k];
int Gn[w][k];
int Bn[w][k];

int lw, lk;
int a = 10;


void display(float size) {
    // Ustawienie koloru rysowania na czerwony.
    glColor3d(1.0, 0.0, 0.0);

    glPushMatrix();
    glTranslated(0, 0, -6);
    glPointSize(ps);
    glBegin(GL_POINTS);
    for (int i = 0; i < lw; i++)
    {
        for (int j = 0; j < lk; j++)
        {
            glColor3f((Rn[i][j]) / 255., (Gn[i][j]) / 255., (Bn[i][j]) / 255.);
            glVertex3f(j, i, 0);

        }
    }
    glEnd();
    glPopMatrix();


}


void key_callback(GLFWwindow* window, int key, int scancode, int action, int mods) {
    if (action == GLFW_PRESS) {
        switch (key) {
        case GLFW_KEY_ESCAPE:
            glfwSetWindowShouldClose(window, GLFW_TRUE);
            break;
        case GLFW_KEY_D:
        {
            int M[3][3] = { {1,1,1},{1,1,1},{1,1,1} };
            for (int i = 1; i < lw - 1; ++i)
                for (int j = 1; j < lk - 1; ++j)
                {
                    Rn[i][j] = (Rs[i - 1][j - 1] * M[0][0] + Rs[i - 1][j] * M[0][1] + Rs[i - 1][j + 1] * M[0][2] +
                        Rs[i][j - 1] * M[1][0] + Rs[i][j] * M[1][1] + Rs[i][j + 1] * M[1][2] +
                        Rs[i + 1][j - 1] * M[2][0] + Rs[i + 1][j] * M[2][1] + Rs[i + 1][j + 1] * M[2][2])
                        / (M[0][0] + M[0][1] + M[0][2] + M[1][0] + M[1][1] + M[1][2] + M[2][0] + M[2][1] + M[2][2]);
                    Gn[i][j] = (Gs[i - 1][j - 1] * M[0][0] + Gs[i - 1][j] * M[0][1] + Gs[i - 1][j + 1] * M[0][2] +
                        Gs[i][j - 1] * M[1][0] + Gs[i][j] * M[1][1] + Gs[i][j + 1] * M[1][2] +
                        Gs[i + 1][j - 1] * M[2][0] + Gs[i + 1][j] * M[2][1] + Gs[i + 1][j + 1] * M[2][2])
                        / (M[0][0] + M[0][1] + M[0][2] + M[1][0] + M[1][1] + M[1][2] + M[2][0] + M[2][1] + M[2][2]);

                    Bn[i][j] = (Bs[i - 1][j - 1] * M[0][0] + Bs[i - 1][j] * M[0][1] + Bs[i - 1][j + 1] * M[0][2] +
                        Bs[i][j - 1] * M[1][0] + Rs[i][j] * M[1][1] + Bs[i][j + 1] * M[1][2] +
                        Bs[i + 1][j - 1] * M[2][0] + Bs[i + 1][j] * M[2][1] + Bs[i + 1][j + 1] * M[2][2])
                        / (M[0][0] + M[0][1] + M[0][2] + M[1][0] + M[1][1] + M[1][2] + M[2][0] + M[2][1] + M[2][2]);
                }
        }
        break;
        case GLFW_KEY_G:
        {
            int M[3][3] = { { -1, -1, -1 },{ -1, 8, -1 },{ -1, -1, -1 } };
            for (int i = 1; i < lw - 1; ++i) {
                for (int j = 1; j < lk - 1; ++j) {
                    Rn[i][j] = (Rs[i - 1][j - 1] * M[0][0] + Rs[i - 1][j] * M[0][1] + Rs[i - 1][j + 1] * M[0][2] +
                        Rs[i][j - 1] * M[1][0] + Rs[i][j] * M[1][1] + Rs[i][j + 1] * M[1][2] +
                        Rs[i + 1][j - 1] * M[2][0] + Rs[i + 1][j] * M[2][1] + Rs[i + 1][j + 1] * M[2][2]);
                    Gn[i][j] = (Gs[i - 1][j - 1] * M[0][0] + Gs[i - 1][j] * M[0][1] + Gs[i - 1][j + 1] * M[0][2] +
                        Gs[i][j - 1] * M[1][0] + Gs[i][j] * M[1][1] + Gs[i][j + 1] * M[1][2] +
                        Gs[i + 1][j - 1] * M[2][0] + Gs[i + 1][j] * M[2][1] + Gs[i + 1][j + 1] * M[2][2]);
                    Bn[i][j] = (Bs[i - 1][j - 1] * M[0][0] + Bs[i - 1][j] * M[0][1] + Bs[i - 1][j + 1] * M[0][2] +
                        Bs[i][j - 1] * M[1][0] + Bs[i][j] * M[1][1] + Bs[i][j + 1] * M[1][2] +
                        Bs[i + 1][j - 1] * M[2][0] + Bs[i + 1][j] * M[2][1] + Gs[i + 1][j + 1] * M[2][2]);
                }
            }
        }
        break;
        case GLFW_KEY_K:
        {
            int M[3][3] = { {-1,-1,-1},{-1,9,-1},{-1,-1,-1} };
            for (int i = 1; i < lw - 1; ++i)
                for (int j = 1; j < lk - 1; ++j)
                {
                    Rn[i][j] = (Rs[i - 1][j - 1] * M[0][0] + Rs[i - 1][j] * M[0][1] + Rs[i - 1][j + 1] * M[0][2] +
                        Rs[i][j - 1] * M[1][0] + Rs[i][j] * M[1][1] + Rs[i][j + 1] * M[1][2] +
                        Rs[i + 1][j - 1] * M[2][0] + Rs[i + 1][j] * M[2][1] + Rs[i + 1][j + 1] * M[2][2])
                        / (M[0][0] + M[0][1] + M[0][2] + M[1][0] + M[1][1] + M[1][2] + M[2][0] + M[2][1] + M[2][2]);
                    Gn[i][j] = (Gs[i - 1][j - 1] * M[0][0] + Gs[i - 1][j] * M[0][1] + Gs[i - 1][j + 1] * M[0][2] +
                        Gs[i][j - 1] * M[1][0] + Gs[i][j] * M[1][1] + Gs[i][j + 1] * M[1][2] +
                        Gs[i + 1][j - 1] * M[2][0] + Gs[i + 1][j] * M[2][1] + Gs[i + 1][j + 1] * M[2][2])
                        / (M[0][0] + M[0][1] + M[0][2] + M[1][0] + M[1][1] + M[1][2] + M[2][0] + M[2][1] + M[2][2]);

                    Bn[i][j] = (Bs[i - 1][j - 1] * M[0][0] + Bs[i - 1][j] * M[0][1] + Bs[i - 1][j + 1] * M[0][2] +
                        Bs[i][j - 1] * M[1][0] + Bs[i][j] * M[1][1] + Bs[i][j + 1] * M[1][2] +
                        Bs[i + 1][j - 1] * M[2][0] + Bs[i + 1][j] * M[2][1] + Bs[i + 1][j + 1] * M[2][2])
                        / (M[0][0] + M[0][1] + M[0][2] + M[1][0] + M[1][1] + M[1][2] + M[2][0] + M[2][1] + M[2][2]);
                }
        }
        break;

        case GLFW_KEY_Q:
        {
            int M[3][3] = { {1,1,1},{1,1,1},{1,1,1} };
            for (int i = 1; i < lw - 1; ++i)
                for (int j = 1; j < lk - 1; ++j)
                {
                    Rn[i][j] += 10;
                    Gn[i][j] += 10;
                    Bn[i][j] += 10;
                }
        }
        break;
        case GLFW_KEY_W:
        {
            int M[3][3] = { {1,1,1},{1,1,1},{1,1,1} };
            for (int i = 1; i < lw - 1; ++i)
                for (int j = 1; j < lk - 1; ++j)
                {
                    Rn[i][j] -= 10;
                    Gn[i][j] -= 10;
                    Bn[i][j] -= 10;
                }
        }
        break;
        case GLFW_KEY_E:
        {
            for (int i = 0; i < lw; i++)
            {
                for (int j = 0; j < lk; j++)
                {
                    Rn[i][j] = Rs[i][j];
                    Gn[i][j] = Gs[i][j];
                    Bn[i][j] = Bs[i][j];
                }
            }
        }
        break;
        case GLFW_KEY_Z:
        {
            int M[3][3] = { {1,1,1},{1,1,1},{1,1,1} };
            for (int i = 1; i < lw - 1; ++i)
                for (int j = 1; j < lk - 1; ++j)
                {
                    Bn[i][j] = 0;
                    Rn[i][j] = 0;
                    Gn[i][j] = Gs[i][j];
                }
        }
        break;
        case GLFW_KEY_C:
        {
            int M[3][3] = { {1,1,1},{1,1,1},{1,1,1} };
            for (int i = 1; i < lw - 1; ++i)
                for (int j = 1; j < lk - 1; ++j)
                {
                    Bn[i][j] = 0;
                    Rn[i][j] = Rs[i][j];
                    Gn[i][j] = 0;
                }
        }
        break;
        case GLFW_KEY_N:
        {
            int M[3][3] = { {1,1,1},{1,1,1},{1,1,1} };
            for (int i = 1; i < lw - 1; ++i)
                for (int j = 1; j < lk - 1; ++j)
                {
                    Bn[i][j] = Bs[i][j];
                    Rn[i][j] = 0;
                    Gn[i][j] = 0;
                }
        }
        break;
        case GLFW_KEY_1:
        {
            for (int i = 1; i < lw - 1; ++i) {
                for (int j = 1; j < lk - 1; ++j) {
                    int maxVal = max(max(Rs[i - 1][j - 1], Rs[i - 1][j]), Rs[i - 1][j + 1]);
                    maxVal = max(maxVal, max(Rs[i][j - 1], Rs[i][j]));
                    maxVal = max(maxVal, max(Rs[i][j + 1], Rs[i + 1][j - 1]));
                    maxVal = max(maxVal, max(Rs[i + 1][j], Rs[i + 1][j + 1]));

                    Rn[i][j] = maxVal;

                    int maxValG = max(max(Gs[i - 1][j - 1], Gs[i - 1][j]), Gs[i - 1][j + 1]);
                    maxValG = max(maxValG, max(Gs[i][j - 1], Gs[i][j]));
                    maxValG = max(maxValG, max(Gs[i][j + 1], Gs[i + 1][j - 1]));
                    maxValG = max(maxValG, max(Gs[i + 1][j], Gs[i + 1][j + 1]));

                    Gn[i][j] = maxValG;

                    int maxValB = max(max(Bs[i - 1][j - 1], Bs[i - 1][j]), Bs[i - 1][j + 1]);
                    maxValB = max(maxValB, max(Bs[i][j - 1], Bs[i][j]));
                    maxValB = max(maxValB, max(Bs[i][j + 1], Bs[i + 1][j - 1]));
                    maxValB = max(maxValB, max(Bs[i + 1][j], Bs[i + 1][j + 1]));

                    Bn[i][j] = maxValB;
                }
            }
        }
        break;
        case GLFW_KEY_2:
        {
            for (int i = 1; i < lw - 1; ++i) {
                for (int j = 1; j < lk - 1; ++j) {
                    int minVal = min(min(Rs[i - 1][j - 1], Rs[i - 1][j]), Rs[i - 1][j + 1]);
                    minVal = min(minVal, min(Rs[i][j - 1], Rs[i][j]));
                    minVal = min(minVal, min(Rs[i][j + 1], Rs[i + 1][j - 1]));
                    minVal = min(minVal, min(Rs[i + 1][j], Rs[i + 1][j + 1]));

                    Rn[i][j] = minVal;

                    int minValG = min(min(Gs[i - 1][j - 1], Gs[i - 1][j]), Gs[i - 1][j + 1]);
                    minValG = min(minValG, min(Gs[i][j - 1], Gs[i][j]));
                    minValG = min(minValG, min(Gs[i][j + 1], Gs[i + 1][j - 1]));
                    minValG = min(minValG, min(Gs[i + 1][j], Gs[i + 1][j + 1]));

                    Gn[i][j] = minValG;

                    int minValB = min(min(Bs[i - 1][j - 1], Bs[i - 1][j]), Bs[i - 1][j + 1]);
                    minValB = min(minValB, min(Bs[i][j - 1], Bs[i][j]));
                    minValB = min(minValB, min(Bs[i][j + 1], Bs[i + 1][j - 1]));
                    minValB = min(minValB, min(Bs[i + 1][j], Bs[i + 1][j + 1]));

                    Bn[i][j] = minValB;
                }
            }
        }
        break;
        }

    }
}


// Definiowanie stałych dla właściwości światła
const GLfloat light_ambient[] = { 0.0f, 0.0f, 0.0f, 1.0f };
const GLfloat light_diffuse[] = { 1.0f, 1.0f, 1.0f, 1.0f };
const GLfloat light_specular[] = { 1.0f, 1.0f, 1.0f, 1.0f };
const GLfloat light_position[] = { 2.0f, 5.0f, 5.0f, 0.0f };

// Definiowanie stałych dla właściwości materiału
const GLfloat mat_ambient[] = { 0.7f, 0.7f, 0.7f, 1.0f };
const GLfloat mat_diffuse[] = { 0.8f, 0.8f, 0.8f, 1.0f };
const GLfloat mat_specular[] = { 1.0f, 1.0f, 1.0f, 1.0f };
const GLfloat high_shininess[] = { 100.0f };

int main(void)
{
    ifstream plik("C:\\Users\\Komputer\\Desktop\\Frafika\\zd5.txt");
    plik >> lw >> lk;
    cout << "wiersze=" << lw << " kolumny=" << lk << endl;
    for (int i = 0; i < lw; ++i)
        for (int j = 0; j < lk; ++j)
        {
            plik >> Rs[i][j];
            plik >> Gs[i][j];
            plik >> Bs[i][j];
        }
    plik.close();
    for (int i = 0; i < lw; ++i)
        for (int j = 0; j < lk; ++j)
        {
            Rn[i][j] = Rs[i][j];
            Gn[i][j] = Gs[i][j];
            Bn[i][j] = Bs[i][j];
        }


    GLFWwindow* window; // Deklaracja wskaźnika na obiekt okna GLFW.


    // Inicjalizacja biblioteki GLFW. Jeśli inicjalizacja się nie powiedzie, program zakończy działanie z kodem -1.
    if (!glfwInit())
        return -1;

    // Utworzenie okna o rozmiarach 800x600 pikseli i tytule "Przykladowe Okno GLFW". 
    // Ostatnie dwa argumenty dotyczą okna dzielonego i atrybutów kontekstu OpenGL, które są tutaj ustawione na NULL.
    window = glfwCreateWindow(800, 600, "Przykladowe Okno GLFW", NULL, NULL);
    // Jeśli utworzenie okna się nie powiedzie, zakończenie działania GLFW i zwolnienie zasobów.
    if (!window)
    {
        glfwTerminate();
        return -1;
    }

    // Ustawienie bieżącego kontekstu renderowania na utworzone okno.
    glfwMakeContextCurrent(window);
    glfwSetKeyCallback(window, key_callback);

    // Pętla renderowania, wykonuje się dopóki okno nie zostanie zamknięte.
    while (!glfwWindowShouldClose(window))
    {
        int width, height;
        // Pobranie rozmiaru bufora ramki dla bieżącego okna.
        glfwGetFramebufferSize(window, &width, &height);
        // Ustawienie widoku portu do rozmiaru bufora ramki.
        glViewport(0, 0, width, height);
        // Czyszczenie bufora kolorów.
        glClear(GL_COLOR_BUFFER_BIT);

        // Ustawienie macierzy projekcji.
        glMatrixMode(GL_PROJECTION);
        glLoadIdentity(); // Zresetowanie macierzy projekcji do macierzy jednostkowej.
        // Ustawienie ortogonalnego widoku z proporcjami zależnymi od rozmiaru okna.
        glOrtho(0 + a, k - a, 0 + a, w - a, 2.0, 100.0);

        // Powrót do modelowania transformacji macierzy.
        glMatrixMode(GL_MODELVIEW);

        // Obliczenie proporcjonalnego rozmiaru kwadratu.
        float squareSize = static_cast<float>(std::min(width, height)) * 0.2f;

        // Wywołanie funkcji rysującej obiekty.
        display(squareSize);

        // Ustawienie koloru tła.
        glClearColor(1, 1, 1, 1);
        // Zamiana buforów w oknie.
        glfwSwapBuffers(window);

        // Włączenie światła, normalizacji normalnych i materiałów koloru
        glEnable(GL_LIGHT0);
        glEnable(GL_NORMALIZE);
        glEnable(GL_COLOR_MATERIAL);
        glEnable(GL_LIGHTING);

        // Ustawienie właściwości światła
        glLightfv(GL_LIGHT0, GL_AMBIENT, light_ambient);
        glLightfv(GL_LIGHT0, GL_DIFFUSE, light_diffuse);
        glLightfv(GL_LIGHT0, GL_SPECULAR, light_specular);
        glLightfv(GL_LIGHT0, GL_POSITION, light_position);

        // Ustawienie właściwości materiału
        glMaterialfv(GL_FRONT, GL_AMBIENT, mat_ambient);
        glMaterialfv(GL_FRONT, GL_DIFFUSE, mat_diffuse);
        glMaterialfv(GL_FRONT, GL_SPECULAR, mat_specular);
        glMaterialfv(GL_FRONT, GL_SHININESS, high_shininess);

        // Przetwarzanie zdarzeń w kolejce zdarzeń.
        glfwPollEvents();
    }
    // Zakończenie działania GLFW i zwolnienie przydzielonych zasobów.
    glfwTerminate();
    return 0; // Zakończenie programu z kodem powrotu 0.
}

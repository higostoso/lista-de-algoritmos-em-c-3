# lista-de-algoritmos-em-c-3
QUETÃO 31- 
#include <stdio.h>

void bubbleSort(int arr[], int n) {
    int i, j, temp;
    for (i = 0; i < n-1; i++) {
        for (j = 0; j < n-i-1; j++) {
            if (arr[j] > arr[j+1]) {
                temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }
}

void printArray(int arr[], int size) {
    int i;
    for (i = 0; i < size; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

int main() {
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr)/sizeof(arr[0]);
    
    printf("Array antes da ordenação: \n");
    printArray(arr, n);

    bubbleSort(arr, n);

    printf("Array depois da ordenação: \n");
    printArray(arr, n);
    
    return 0;
}
QUESTÃO 32- 
#include <stdio.h>

void selectionSort(int arr[], int n) {
    int i, j, min_idx, temp;
    
    for (i = 0; i < n-1; i++) {
        min_idx = i;
        for (j = i+1; j < n; j++) {
            if (arr[j] < arr[min_idx]) {
                min_idx = j;
            }
        }
        
        if (min_idx != i) {
            temp = arr[i];
            arr[i] = arr[min_idx];
            arr[min_idx] = temp;
        }
    }
}

void printArray(int arr[], int size) {
    int i;
    for (i = 0; i < size; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

int main() {
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr)/sizeof(arr[0]);
    
    printf("Array antes da ordenação: \n");
    printArray(arr, n);

    selectionSort(arr, n);

    printf("Array depois da ordenação: \n");
    printArray(arr, n);
    
    return 0;
}
QUESTÃO 33-
#include <stdio.h>

void insertionSort(int arr[], int n) {
    int i, key, j;

    for (i = 1; i < n; i++) {
        key = arr[i]; 
        j = i - 1;

        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }

        arr[j + 1] = key;
    }
}

void printArray(int arr[], int size) {
    int i;
    for (i = 0; i < size; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

int main() {
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr)/sizeof(arr[0]);
    
    printf("Array antes da ordenação: \n");
    printArray(arr, n);

    insertionSort(arr, n);

    printf("Array depois da ordenação: \n");
    printArray(arr, n);
    
    return 0;
}
QUESTÃO 34- 
#include <stdio.h>
#include <stdlib.h>

void merge(int arr[], int l, int m, int r) {
    int n1 = m - l + 1;
    int n2 = r - m;

    int *L = (int *)malloc(n1 * sizeof(int));
    int *R = (int *)malloc(n2 * sizeof(int));
    
    int i, j, k;

    for (i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (j = 0; j < n2; j++)
        R[j] = arr[m + 1 + j];

    i = 0; 
    j = 0; 
    k = l; 
    
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        } else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }

    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }

    free(L);
    free(R);
}

void mergeSort(int arr[], int l, int r) {
    if (l < r) {
        int m = l + (r - l) / 2;

        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);

        merge(arr, l, m, r);
    }
}

void printArray(int arr[], int size) {
    int i;
    for (i = 0; i < size; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

int main() {
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr)/sizeof(arr[0]);
    
    printf("Array antes da ordenação: \n");
    printArray(arr, n);

    mergeSort(arr, 0, n - 1);

    printf("Array depois da ordenação: \n");
    printArray(arr, n);
    
    return 0;
}
QUESTÃO 35-
#include <stdio.h>

void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = low - 1; 
    
    for (int j = low; j < high; j++) {
        if (arr[j] <= pivot) {
            i++; 
            swap(&arr[i], &arr[j]);
        }
    }
    swap(&arr[i + 1], &arr[high]); 
    return (i + 1); 
}

void quickSort(int arr[], int low, int high) {
    if (low < high) {

        int pi = partition(arr, low, high);

        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

void printArray(int arr[], int size) {
    for (int i = 0; i < size; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

int main() {
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr) / sizeof(arr[0]);
    
    printf("Array antes da ordenação: \n");
    printArray(arr, n);

    quickSort(arr, 0, n - 1);

    printf("Array depois da ordenação: \n");
    printArray(arr, n);
    
    return 0;
}
QUESTÃO 36-
#include <stdio.h>
#include <stdlib.h>

#define MAX 100

typedef struct {
    int top;
    int array[MAX];
} Stack;

void initStack(Stack *s) {
    s->top = -1;
}

int isEmpty(Stack *s) {
    return s->top == -1;
}

int isFull(Stack *s) {
    return s->top == MAX - 1;
}

void push(Stack *s, int value) {
    if (isFull(s)) {
        printf("Pilha cheia! Não é possível empurrar o valor %d\n", value);
        return;
    }
    s->array[++(s->top)] = value;
    printf("Empurrou %d para a pilha\n", value);
}

int pop(Stack *s) {
    if (isEmpty(s)) {
        printf("Pilha vazia! Não é possível remover um valor\n");
        return -1;
    }
    return s->array[(s->top)--];
}

int peek(Stack *s) {
    if (isEmpty(s)) {
        printf("Pilha vazia! Não há valor no topo\n");
        return -1;
    }
    return s->array[s->top];
}

void printStack(Stack *s) {
    if (isEmpty(s)) {
        printf("Pilha vazia!\n");
        return;
    }
    printf("Elementos na pilha: ");
    for (int i = 0; i <= s->top; i++) {
        printf("%d ", s->array[i]);
    }
    printf("\n");
}

int main() {
    Stack s;
    initStack(&s);

    push(&s, 10);
    push(&s, 20);
    push(&s, 30);

    printStack(&s);

    printf("Topo da pilha: %d\n", peek(&s));

    printf("Removido da pilha: %d\n", pop(&s));
    printf("Removido da pilha: %d\n", pop(&s));

    printStack(&s);

    return 0;
}
QUESTÃO 37- 
#include <stdio.h>
#include <stdlib.h>

#define MAX 100

typedef struct {
    int front, rear, size;
    int array[MAX];
} Queue;

void initQueue(Queue *q) {
    q->front = 0;
    q->rear = -1;
    q->size = 0;
}

int isEmpty(Queue *q) {
    return q->size == 0;
}

int isFull(Queue *q) {
    return q->size == MAX;
}

void enqueue(Queue *q, int value) {
    if (isFull(q)) {
        printf("Fila cheia! Não é possível adicionar o valor %d\n", value);
        return;
    }
    q->rear = (q->rear + 1) % MAX;
    q->array[q->rear] = value;
    q->size++;
    printf("Adicionou %d na fila\n", value);
}

int dequeue(Queue *q) {
    if (isEmpty(q)) {
        printf("Fila vazia! Não é possível remover um valor\n");
        return -1;
    }
    int value = q->array[q->front];
    q->front = (q->front + 1) % MAX;
    q->size--;
    return value;
}

int peek(Queue *q) {
    if (isEmpty(q)) {
        printf("Fila vazia! Não há valor na frente\n");
        return -1;
    }
    return q->array[q->front];
}

void printQueue(Queue *q) {
    if (isEmpty(q)) {
        printf("Fila vazia!\n");
        return;
    }
    printf("Elementos na fila: ");
    for (int i = 0; i < q->size; i++) {
        printf("%d ", q->array[(q->front + i) % MAX]);
    }
    printf("\n");
}

int main() {
    Queue q;
    initQueue(&q);

    enqueue(&q, 10);
    enqueue(&q, 20);
    enqueue(&q, 30);

    printQueue(&q);

    printf("Frente da fila: %d\n", peek(&q));

    printf("Removido da fila: %d\n", dequeue(&q));
    printf("Removido da fila: %d\n", dequeue(&q));

    printQueue(&q);

    return 0;
}
QUESTÃO 38-
#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>
#include <string.h>

#define MAX 100

typedef struct {
    int top;
    char items[MAX];
} Stack;

void initStack(Stack *s) {
    s->top = -1;
}

int isEmpty(Stack *s) {
    return s->top == -1;
}

int isFull(Stack *s) {
    return s->top == MAX - 1;
}

void push(Stack *s, char c) {
    if (isFull(s)) {
        printf("Pilha cheia!\n");
        return;
    }
    s->items[++(s->top)] = c;
}

char pop(Stack *s) {
    if (isEmpty(s)) {
        printf("Pilha vazia!\n");
        return '\0'; 
    }
    return s->items[(s->top)--];
}

char peek(Stack *s) {
    if (isEmpty(s)) {
        return '\0'; 
    }
    return s->items[s->top];
}

int precedence(char op) {
    switch (op) {
        case '+':
        case '-':
            return 1;
        case '*':
        case '/':
            return 2;
        case '^':
            return 3;
        default:
            return 0;
    }
}

void infixToPostfix(const char *infix, char *postfix) {
    Stack s;
    initStack(&s);

    int i = 0;
    int k = 0; 

    while (infix[i] != '\0') {
        char c = infix[i];
        
        if (isalnum(c)) { 
            postfix[k++] = c;
        } else if (c == '(') { 
            push(&s, c);
        } else if (c == ')') { 
            while (!isEmpty(&s) && peek(&s) != '(') {
                postfix[k++] = pop(&s);
            }
            pop(&s);
        } else { 
            while (!isEmpty(&s) && precedence(c) <= precedence(peek(&s))) {
                postfix[k++] = pop(&s);
            }
            push(&s, c);
        }
        i++;
    }

    while (!isEmpty(&s)) {
        postfix[k++] = pop(&s);
    }

    postfix[k] = '\0'; 
}

int main() {
    char infix[MAX];
    char postfix[MAX];

    printf("Digite a expressão infixa: ");
    fgets(infix, MAX, stdin);

    size_t len = strlen(infix);
    if (len > 0 && infix[len - 1] == '\n') {
        infix[len - 1] = '\0';
    }

    infixToPostfix(infix, postfix);

    printf("Expressão pós-fixa: %s\n", postfix);

    return 0;
}
QUESTÃO 39-
#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>
#include <string.h>

#define MAX 100

typedef struct {
    int top;
    int items[MAX];
} Stack;

void initStack(Stack *s) {
    s->top = -1;
}

int isEmpty(Stack *s) {
    return s->top == -1;
}

int isFull(Stack *s) {
    return s->top == MAX - 1;
}

void push(Stack *s, int value) {
    if (isFull(s)) {
        printf("Pilha cheia!\n");
        return;
    }
    s->items[++(s->top)] = value;
}

int pop(Stack *s) {
    if (isEmpty(s)) {
        printf("Pilha vazia!\n");
        return -1;
    }
    return s->items[(s->top)--];
}

int evaluatePostfix(const char *postfix) {
    Stack s;
    initStack(&s);

    int i = 0;
    while (postfix[i] != '\0') {
        char c = postfix[i];

        if (isdigit(c)) {
            push(&s, c - '0');
        } else if (c == ' ') {
        } else {
            int val2 = pop(&s);
            int val1 = pop(&s);
            int result;

            switch (c) {
                case '+':
                    result = val1 + val2;
                    break;
                case '-':
                    result = val1 - val2;
                    break;
                case '*':
                    result = val1 * val2;
                    break;
                case '/':
                    result = val1 / val2;
                    break;
                default:
                    printf("Operador inválido: %c\n", c);
                    return -1; 
            }
            push(&s, result);
        }
        i++;
    }

    return pop(&s);
}

int main() {
    char postfix[MAX];

    printf("Digite a expressão pós-fixa: ");
    fgets(postfix, MAX, stdin);

    size_t len = strlen(postfix);
    if (len > 0 && postfix[len - 1] == '\n') {
        postfix[len - 1] = '\0';
    }

    int result = evaluatePostfix(postfix);

    printf("Resultado da expressão pós-fixa: %d\n", result);

    return 0;
}
QUESTÃO 40-
#include <stdio.h>

#define SIZE 3

void printBoard(char board[SIZE][SIZE]) {
    printf("\n");
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            printf(" %c ", board[i][j]);
            if (j < SIZE - 1) printf("|");
        }
        printf("\n");
        if (i < SIZE - 1) {
            for (int j = 0; j < SIZE; j++) {
                printf("---");
                if (j < SIZE - 1) printf("|");
            }
            printf("\n");
        }
    }
    printf("\n");
}

int checkWin(char board[SIZE][SIZE], char player) {
    for (int i = 0; i < SIZE; i++) {
        if ((board[i][0] == player && board[i][1] == player && board[i][2] == player) ||
            (board[0][i] == player && board[1][i] == player && board[2][i] == player)) {
            return 1;
        }
    }

    if ((board[0][0] == player && board[1][1] == player && board[2][2] == player) ||
        (board[0][2] == player && board[1][1] == player && board[2][0] == player)) {
        return 1;
    }
    
    return 0;
}

int isBoardFull(char board[SIZE][SIZE]) {
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            if (board[i][j] == ' ') {
                return 0;
            }
        }
    }
    return 1;
}

int main() {
    char board[SIZE][SIZE];
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            board[i][j] = ' ';
        }
    }
    
    char player = 'X';
    int row, col;
    int moves = 0;
    
    while (1) {
        printBoard(board);
        printf("Jogador %c, insira a linha e a coluna (0-2) separados por espaço: ", player);
        scanf("%d %d", &row, &col);
        
        if (row < 0 || row >= SIZE || col < 0 || col >= SIZE || board[row][col] != ' ') {
            printf("Movimento inválido. Tente novamente.\n");
            continue;
        }
        
        board[row][col] = player;
        moves++;
        
        if (checkWin(board, player)) {
            printBoard(board);
            printf("Jogador %c venceu!\n", player);
            break;
        }
        
        if (isBoardFull(board)) {
            printBoard(board);
            printf("O jogo terminou em empate!\n");
            break;
        }

        player = (player == 'X') ? 'O' : 'X';
    }
    
    return 0;
}
QUESTÃO 41-
#include <stdio.h>
#include <ctype.h>
#include <string.h>

#define MAX 100

void cifraCesar(char *mensagem, int chave) {
    int i;
    for (i = 0; mensagem[i] != '\0'; i++) {
        char c = mensagem[i];
        
        if (isalpha(c)) {
            char base = isupper(c) ? 'A' : 'a';
            mensagem[i] = (c - base + chave) % 26 + base;
        }
    }
}

void decifraCesar(char *mensagem, int chave) {
    cifraCesar(mensagem, 26 - (chave % 26));
}

int main() {
    char mensagem[MAX];
    int chave;
    char escolha;
    
    printf("Digite a mensagem (máximo %d caracteres): ", MAX - 1);
    fgets(mensagem, MAX, stdin);

    size_t len = strlen(mensagem);
    if (len > 0 && mensagem[len - 1] == '\n') {
        mensagem[len - 1] = '\0';
    }
    
    printf("Digite a chave (número de posições para deslocar): ");
    scanf("%d", &chave);

    printf("Digite 'e' para criptografar ou 'd' para descriptografar: ");
    scanf(" %c", &escolha);
    
    if (escolha == 'e') {
        cifraCesar(mensagem, chave);
        printf("Mensagem criptografada: %s\n", mensagem);
    } else if (escolha == 'd') {
        decifraCesar(mensagem, chave);
        printf("Mensagem descriptografada: %s\n", mensagem);
    } else {
        printf("Escolha inválida.\n");
    }
    
    return 0;
}
QUESTÃO 42-
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main() {
	
    srand(time(NULL));

    int numeroAleatorio = (rand() % 100) + 1;
    
    printf("Número aleatório entre 1 e 100: %d\n", numeroAleatorio);
    
    return 0;
}
QUESTÃO 43-
#include <stdio.h>
#include <stdlib.h>

void encontrarLIS(int vetor[], int n) {
    int i, j, maior, indice;

    int *lis = (int *)malloc(n * sizeof(int));
    int *pai = (int *)malloc(n * sizeof(int));

    for (i = 0; i < n; i++) {
        lis[i] = 1;
        pai[i] = -1; 
    }

    for (i = 1; i < n; i++) {
        for (j = 0; j < i; j++) {
            if (vetor[i] > vetor[j] && lis[i] < lis[j] + 1) {
                lis[i] = lis[j] + 1;
                pai[i] = j;
            }
        }
    }

    maior = 0;
    indice = 0;
    for (i = 0; i < n; i++) {
        if (lis[i] > maior) {
            maior = lis[i];
            indice = i;
        }
    }

    int *subsequencia = (int *)malloc(maior * sizeof(int));
    int k = maior - 1;
    while (pai[indice] != -1) {
        subsequencia[k--] = vetor[indice];
        indice = pai[indice];
    }
    subsequencia[k] = vetor[indice];

    printf("Maior subsequência crescente é: ");
    for (i = 0; i < maior; i++) {
        printf("%d ", subsequencia[i]);
    }
    printf("\n");

    free(lis);
    free(pai);
    free(subsequencia);
}

int main() {
    int vetor[] = {10, 22, 9, 33, 21, 50, 41, 60, 80};
    int n = sizeof(vetor) / sizeof(vetor[0]);

    encontrarLIS(vetor, n);

    return 0;
}
QUESTÃO 44- 
#include <stdio.h>
#include <stdbool.h>

#define N 8

typedef struct {
    int x;
    int y;
} Posicao;

bool dentroDoTabuleiro(int x, int y) {
    return (x >= 0 && x < N && y >= 0 && y < N);
}

void imprimirTabuleiro(bool tabuleiro[N][N]) {
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            if (tabuleiro[i][j]) {
                printf(" K ");
            } else {
                printf(" . ");
            }
        }
        printf("\n");
    }
}

void movimentosCavalo(int x, int y) {
    int movimentos[8][2] = {
        {2, 1}, {2, -1}, {-2, 1}, {-2, -1},
        {1, 2}, {1, -2}, {-1, 2}, {-1, -2}
    };

    bool tabuleiro[N][N] = {false}; 

    if (dentroDoTabuleiro(x, y)) {
        tabuleiro[x][y] = true;
    }

    for (int i = 0; i < 8; i++) {
        int novoX = x + movimentos[i][0];
        int novoY = y + movimentos[i][1];
        if (dentroDoTabuleiro(novoX, novoY)) {
            tabuleiro[novoX][novoY] = true;
        }
    }

    imprimirTabuleiro(tabuleiro);
}

int main() {
    int x, y;

    printf("Digite a posição inicial do cavalo (x y): ");
    scanf("%d %d", &x, &y);

    if (!dentroDoTabuleiro(x, y)) {
        printf("Posição inicial fora do tabuleiro.\n");
        return 1;
    }

    movimentosCavalo(x, y);

    return 0;
}
QUESTÃO 45-
#include <stdio.h>
#include <stdbool.h>

#define N 9

void imprimirSudoku(int sudoku[N][N]) {
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            printf("%d ", sudoku[i][j]);
        }
        printf("\n");
    }
}

bool ehSeguro(int sudoku[N][N], int linha, int coluna, int num) {

    for (int x = 0; x < N; x++) {
        if (sudoku[linha][x] == num) {
            return false;
        }
    }
    for (int x = 0; x < N; x++) {
        if (sudoku[x][coluna] == num) {
            return false;
        }
    }

    int inicioLinha = linha - linha % 3;
    int inicioColuna = coluna - coluna % 3;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (sudoku[i + inicioLinha][j + inicioColuna] == num) {
                return false;
            }
        }
    }

    return true;
}

bool resolverSudoku(int sudoku[N][N]) {
    int linha, coluna;

    bool vazio = false;
    for (linha = 0; linha < N; linha++) {
        for (coluna = 0; coluna < N; coluna++) {
            if (sudoku[linha][coluna] == 0) {
                vazio = true;
                break;
            }
        }
        if (vazio) {
            break;
        }
    }

    if (!vazio) {
        return true;
    }

    for (int num = 1; num <= 9; num++) {
        if (ehSeguro(sudoku, linha, coluna, num)) {
            sudoku[linha][coluna] = num;

            if (resolverSudoku(sudoku)) {
                return true;
            }
            sudoku[linha][coluna] = 0;
        }
    }

    return false;
}

int main() {

    int sudoku[N][N] = {
        {5, 3, 0, 0, 7, 0, 0, 0, 0},
        {6, 0, 0, 1, 9, 5, 0, 0, 0},
        {0, 9, 8, 0, 0, 0, 0, 6, 0},
        {8, 0, 0, 0, 6, 0, 0, 0, 3},
        {4, 0, 0, 8, 0, 3, 0, 0, 1},
        {7, 0, 0, 0, 2, 0, 0, 0, 6},
        {0, 6, 0, 0, 0, 0, 2, 8, 0},
        {0, 0, 0, 4, 1, 9, 0, 0, 5},
        {0, 0, 0, 0, 8, 0, 0, 7, 9}
    };

    if (resolverSudoku(sudoku)) {
        printf("Sudoku resolvido:\n");
        imprimirSudoku(sudoku);
    } else {
        printf("Não há solução para o Sudoku fornecido.\n");
    }

    return 0;
}
QUESTÃO 46-
#include <stdio.h>
#include <limits.h>
#include <stdbool.h>

#define V 9 

int minDistance(int dist[], bool sptSet[]) {
    int min = INT_MAX, min_index;
    
    for (int v = 0; v < V; v++) {
        if (!sptSet[v] && dist[v] <= min) {
            min = dist[v];
            min_index = v;
        }
    }
    
    return min_index;
}

void printSolution(int dist[], int n) {
    printf("Vértice \t Distância da origem\n");
    for (int i = 0; i < n; i++) {
        printf("%d \t\t %d\n", i, dist[i]);
    }
}

void dijkstra(int graph[V][V], int src) {
    int dist[V]; 
    bool sptSet[V]; 

    for (int i = 0; i < V; i++) {
        dist[i] = INT_MAX;
        sptSet[i] = false;
    }

    dist[src] = 0;

    for (int count = 0; count < V - 1; count++) {
 
        int u = minDistance(dist, sptSet);

        sptSet[u] = true;

        for (int v = 0; v < V; v++) {
            if (!sptSet[v] && graph[u][v] && dist[u] != INT_MAX && dist[u] + graph[u][v] < dist[v]) {
                dist[v] = dist[u] + graph[u][v];
            }
        }
    }

    printSolution(dist, V);
}

int main() {
	
    int graph[V][V] = {
        {0, 4, 0, 0, 0, 0, 0, 8, 0},
        {4, 0, 8, 0, 0, 0, 0, 11, 0},
        {0, 8, 0, 7, 0, 4, 0, 0, 2},
        {0, 0, 7, 0, 9, 14, 0, 0, 0},
        {0, 0, 0, 9, 0, 10, 0, 0, 0},
        {0, 0, 4, 14, 10, 0, 2, 0, 0},
        {0, 0, 0, 0, 0, 2, 0, 1, 6},
        {8, 11, 0, 0, 0, 0, 1, 0, 7},
        {0, 0, 2, 0, 0, 0, 6, 7, 0}
    };

    dijkstra(graph, 0);

    return 0;
}
QUESTÃO 47-
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    int src, dest, weight;
} Edge;

typedef struct {
    int parent;
    int rank;
} Subset;

int compare(const void *a, const void *b) {
    return ((Edge*)a)->weight - ((Edge*)b)->weight;
}

int find(Subset subsets[], int i) {
    if (subsets[i].parent != i) {
        subsets[i].parent = find(subsets, subsets[i].parent);
    }
    return subsets[i].parent;
}

void Union(Subset subsets[], int x, int y) {
    int xroot = find(subsets, x);
    int yroot = find(subsets, y);

    if (subsets[xroot].rank < subsets[yroot].rank) {
        subsets[xroot].parent = yroot;
    } else if (subsets[xroot].rank > subsets[yroot].rank) {
        subsets[yroot].parent = xroot;
    } else {
        subsets[yroot].parent = xroot;
        subsets[xroot].rank++;
    }
}

void kruskal(Edge edges[], int V, int E) {
    Edge result[V]; 
    int e = 0;
    int i = 0; 
    qsort(edges, E, sizeof(edges[0]), compare);

    Subset *subsets = (Subset*)malloc(V * sizeof(Subset));
    for (int v = 0; v < V; ++v) {
        subsets[v].parent = v;
        subsets[v].rank = 0;
    }

    while (e < V - 1 && i < E) {

        Edge next_edge = edges[i++];
        int x = find(subsets, next_edge.src);
        int y = find(subsets, next_edge.dest);

        if (x != y) {
            result[e++] = next_edge;
            Union(subsets, x, y);
        }
    }

    printf("Aresta \t Peso\n");
    for (i = 0; i < e; ++i) {
        printf("%d - %d \t %d\n", result[i].src, result[i].dest, result[i].weight);
    }

    free(subsets);
}

int main() {
    int V = 4; 
    int E = 5; 
    
    Edge edges[] = {
        {0, 1, 10},
        {0, 2, 6},
        {0, 3, 5},
        {1, 3, 15},
        {2, 3, 4}
    };

    kruskal(edges, V, E);

    return 0;
}
QUESTÃO 48-
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

#define NUM_ANDARES 10

typedef struct {
    int andar_atual;
    int destino;
    bool em_movimento;
} Elevador;

void inicializa_elevador(Elevador *elevador) {
    elevador->andar_atual = 0; 
    elevador->destino = -1; 
    elevador->em_movimento = false;
}

void mover_elevador(Elevador *elevador) {
    if (elevador->destino == -1) {
        printf("O elevador não tem destino definido.\n");
        return;
    }

    elevador->em_movimento = true;

    if (elevador->andar_atual < elevador->destino) {
        printf("O elevador está subindo.\n");
        while (elevador->andar_atual < elevador->destino) {
            elevador->andar_atual++;
            printf("Elevador no andar %d.\n", elevador->andar_atual);
        }
    } else if (elevador->andar_atual > elevador->destino) {
        printf("O elevador está descendo.\n");
        while (elevador->andar_atual > elevador->destino) {
            elevador->andar_atual--;
            printf("Elevador no andar %d.\n", elevador->andar_atual);
        }
    }

    elevador->em_movimento = false;
    elevador->destino = -1; 
    printf("O elevador chegou ao andar %d.\n", elevador->andar_atual);
}

void chamar_elevador(Elevador *elevador, int andar_destino) {
    if (andar_destino < 0 || andar_destino >= NUM_ANDARES) {
        printf("Andar inválido!\n");
        return;
    }

    if (elevador->em_movimento) {
        printf("O elevador já está em movimento. Por favor, espere.\n");
        return;
    }

    elevador->destino = andar_destino;
    printf("Chamando o elevador para o andar %d.\n", andar_destino);
    mover_elevador(elevador);
}

int main() {
    Elevador elevador;
    inicializa_elevador(&elevador);

    chamar_elevador(&elevador, 3); 
    chamar_elevador(&elevador, 7);
    chamar_elevador(&elevador, 2);  

    return 0;
}
QUESTÃO 49-
#include <stdio.h>
#include <stdbool.h>

bool verifica_padrao(int vetor[], int tamanho_vetor, int padrao[], int tamanho_padrao, int posicao) {
    if (posicao + tamanho_padrao > tamanho_vetor) {
        return false;
    }

    for (int i = 0; i < tamanho_padrao; i++) {
        if (vetor[posicao + i] != padrao[i]) {
            return false; 
        }
    }

    return true;
}

void encontrar_padrao(int vetor[], int tamanho_vetor, int padrao[], int tamanho_padrao) {
    bool encontrado = false;
    for (int i = 0; i <= tamanho_vetor - tamanho_padrao; i++) {
        if (verifica_padrao(vetor, tamanho_vetor, padrao, tamanho_padrao, i)) {
            printf("Padrão encontrado na posição %d\n", i);
            encontrado = true;
        }
    }

    if (!encontrado) {
        printf("Padrão não encontrado.\n");
    }
}

int main() {

    int vetor[] = {1, 2, 3, 4, 2, 3, 4, 5, 6, 2, 3, 4};
    int tamanho_vetor = sizeof(vetor) / sizeof(vetor[0]);

    int padrao[] = {2, 3, 4};
    int tamanho_padrao = sizeof(padrao) / sizeof(padrao[0]);

    encontrar_padrao(vetor, tamanho_vetor, padrao, tamanho_padrao);

    return 0;
}
QUESTÃO 50-
	#include <stdio.h>
#include <string.h>

void compressao_rle(const char *input, char *output) {
    int n = strlen(input);
    int j = 0;
    
    for (int i = 0; i < n; i++) {

        int count = 1;
        while (i < n - 1 && input[i] == input[i + 1]) {
            i++;
            count++;
        }

        output[j++] = input[i];
        output[j++] = count + '0'; 
    }
    
    output[j] = '\0'; 
}

void descompressao_rle(const char *input, char *output) {
    int n = strlen(input);
    int j = 0;
    
    for (int i = 0; i < n; i += 2) {
        char ch = input[i];
        int count = input[i + 1] - '0'; 
        
        for (int k = 0; k < count; k++) {
            output[j++] = ch;
        }
    }
    
    output[j] = '\0';

int main() {
    char input[] = "aaaabbbccdaa";
    char comprimido[100];

    compressao_rle(input, comprimido);
    printf("Comprimido: %s\n", comprimido);

    descompressao_rle(comprimido, descomprimido);
    printf("Descomprimido: %s\n", descomprimido);
    
    return 0;
}

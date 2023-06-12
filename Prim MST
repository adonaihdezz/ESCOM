#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

#define MAXN 30001
#define INF INT_MAX
//alamcenar los dos enteros 
typedef struct {
    int first;
    int second;
} pii;
//vector dinamico de pares 
//almacena las aristas del grafo en una lista de adyacencia 
typedef struct {
    pii* array; //puntero a un arreglo de parejas
    size_t size; //tamano del vector 
    size_t capacity;//cuantos elementos puede almacenar el vector 
} Vector;

void vectorInit(Vector* vec) {
    vec->capacity = 2; //evitar asignar demasiada memoria innecesari si el vector contiene pocos elementos
    vec->size = 0;
    vec->array = (pii*)malloc(vec->capacity * sizeof(pii));
}
//si se alcanza el tope se duplica la capacidad del vector 
//para permitir mas elementos
void vectorPushBack(Vector* vec, pii value) { // recibe un puntero al vector en que va a agregar el elemento y el elemento a agregar
    if (vec->size == vec->capacity) {
        vec->capacity *= 2;
        vec->array = (pii*)realloc(vec->array, vec->capacity * sizeof(pii)); //actualizar el puntero al arreglo
    }
    vec->array[vec->size++] = value; //se asigna el valor al final del vector y se incrementa el tamano 
}

void vectorFree(Vector* vec) {
    free(vec->array);
    vec->array = NULL;
    vec->size = 0;
    vec->capacity = 0;
}

Vector adj[MAXN]; // grafo almacenado en una lista de adyacencia
int visited[MAXN]; //arreglo de nodos visitados

int prim(int start) { //recibe el nodo inicial
    Vector pq; //cola de prioridad para almacenar los nodos y sus costos
    vectorInit(&pq); //inicia la cola 
    int minimumCost = 0;

    pii startPair; //
    startPair.first = 0; //costo del nodo start
    startPair.second = start; // nodo de inicio del algoritmo 

    vectorPushBack(&pq, startPair); // se agrega el nodo inicial a la cola de prioridad

    while (pq.size > 0) { //mientras la cola no este vacia
        int u = pq.array[0].second; //se obtiene el nodo con menor costo
        int cost = pq.array[0].first; //se obtiene el costo de ese nodo

        // Remove the minimum element from the priority queue
        for (size_t i = 0; i < pq.size - 1; i++) {
            pq.array[i] = pq.array[i + 1]; // se dezplazan los elementos de la cola de prioridad hacia la izquierda
        }
        pq.size--; // se decrementa el tamano de la cola de prioridad

        if (visited[u])//inicialmente todos  son 0, 
        //u puede ser A, si es verdadero 1, se omite el resto del bucle y se continua con la siguiente iteracion 
            continue;
   // si visited[u] es falso, se marca como visitado y se suma el costo de la arista
        visited[u] = 1; //se marca el nodo como visitado
        minimumCost += cost;
//si el costo actual de la arista AyB es 3, se actualiza el costo minimo
//garantiza que el nodo solo sea visitado una vez 

        for (size_t i = 0; i < adj[u].size; i++) {//se recorre la lista de adyacencia del nodo u, nodos vecinos y sus costos
            int v = adj[u].array[i].first; // se obtiene el nodo vecino
            int weight = adj[u].array[i].second; // se obtiene el costo de la union entre u y v
            if (!visited[v]) { //si no ha sido visitado
                pii newPair; //se crea una nueva pareja para agregar a la cola de prioridad
                newPair.first = weight; //crea una nueva pareja con el costo de la arista
                newPair.second = v; //crea una nueva pareja con el nodo vecino v 
                vectorPushBack(&pq, newPair); //se agrega la nueva pareja a la cola de prioridad
            }
        }
    }

    vectorFree(&pq);

    return minimumCost;
}

int main() {
    int n, m;
    scanf("%d %d", &n, &m);
//forma el grafo 
    for (int i = 0; i < m; i++) {
        int a, b, c;
        scanf("%d %d %d", &a, &b, &c);
//par conecta el nodo a con el nodo b y el costo de la arista es c
        pii pair1;
        pair1.first = b;
        pair1.second = c;
        vectorPushBack(&adj[a], pair1);
//par conecta el nodo b con el nodo a y el costo de la arista es c
        pii pair2;
        pair2.first = a;
        pair2.second = c;
        vectorPushBack(&adj[b], pair2);
    }

    int minimumCost = prim(1); //se llama al algoritmo de prim con el nodo 1 como nodo inicial
    printf("%d\n", minimumCost);

    return 0;
}

#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

class Graph {
private:
    int Vcount;
    int Ecount;
    bool directed;

    // adjacency list: pair = (neighbor, weight)
    vector<vector<pair<int,int>>> adj;

public:
    // constructor
    Graph(int vertices, bool isDirected) {
        Vcount = vertices;
        Ecount = 0;
        directed = isDirected;
        adj.resize(vertices);
    }

    // add vertex
    void addVertex() {
        adj.push_back({});
        Vcount++;
    }

    // add edge 
    void addEdge(int u, int v, int weight = 1) {
        adj[u].push_back({v, weight});
        if (!directed)
            adj[v].push_back({u, weight});
        Ecount++;
    }

    // remove edge
    void removeEdge(int u, int v) {
        adj[u].erase(
            remove_if(adj[u].begin(), adj[u].end(),
                      [v](pair<int,int> p){ return p.first == v; }),
            adj[u].end()
        );

        if (!directed) {
            adj[v].erase(
                remove_if(adj[v].begin(), adj[v].end(),
                          [u](pair<int,int> p){ return p.first == u; }),
                adj[v].end()
            );
        }
        Ecount--;
    }

    // neighbors of u
    vector<int> neighbors(int u) {
        vector<int> res;
        for (auto p : adj[u])
            res.push_back(p.first);
        return res;
    }

    // number of vertices
    int V() {
        return Vcount;
    }

    // number of edges
    int E() {
        return Ecount;
    }

    // build adjacency matrix
    vector<vector<int>> buildAdjMatrix() {
        vector<vector<int>> matrix(Vcount, vector<int>(Vcount, 0));

        for (int u = 0; u < Vcount; u++) {
            for (auto p : adj[u]) {
                int v = p.first;
                matrix[u][v] = p.second;
            }
        }
        return matrix;
    }

    // print adjacency list
    void printAdjList() {
        for (int i = 0; i < Vcount; i++) {
            cout << i << ": ";
            for (auto p : adj[i])
                cout << "(" << p.first << ", w=" << p.second << ") ";
            cout << endl;
        }
    }
};

int main() {
    Graph g(4, false); // undirected graph

    g.addEdge(0, 1);
    g.addEdge(0, 2, 5); // weighted edge
    g.addEdge(1, 3);

    cout << "Adjacency List:\n";
    g.printAdjList();

    cout << "\nNumber of vertices: " << g.V();
    cout << "\nNumber of edges: " << g.E() << endl;

    cout << "\nAdjacency Matrix:\n";
    vector<vector<int>> matrix = g.buildAdjMatrix();
    for (auto row : matrix) {
        for (int x : row)
            cout << x << " ";
        cout << endl;
    }

    return 0;
}

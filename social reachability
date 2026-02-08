#include <iostream>
#include <vector>
#include <queue>
#include <algorithm>
using namespace std;

int main() {
    int n = 6; // number of people (vertices)
    vector<vector<int>> adj(n);

    // friendships (undirected graph)
    adj[0] = {1, 2};
    adj[1] = {0, 3};
    adj[2] = {0, 3, 4};
    adj[3] = {1, 2, 5};
    adj[4] = {2};
    adj[5] = {3};

    int S = 0; // start person
    int T = 5; // target person

    vector<bool> visited(n, false);
    vector<int> dist(n, -1);
    vector<int> parent(n, -1);
    queue<int> q;

    // BFS initialization
    visited[S] = true;
    dist[S] = 0;
    q.push(S);

    // BFS traversal
    while (!q.empty()) {
        int u = q.front();
        q.pop();

        for (int v : adj[u]) {
            if (!visited[v]) {
                visited[v] = true;
                dist[v] = dist[u] + 1;
                parent[v] = u;
                q.push(v);
            }
        }
    }

    // Part (i): people within distance ≤ 2
    cout << "People within distance <= 2 from " << S << ": ";
    for (int i = 0; i < n; i++) {
        if (dist[i] != -1 && dist[i] <= 2)
            cout << i << " ";
    }
    cout << endl;

    // Part (ii): shortest path S -> T
    cout << "Shortest path from " << S << " to " << T << ": ";
    if (dist[T] == -1) {
        cout << "No path\n";
    } else {
        vector<int> path;
        for (int v = T; v != -1; v = parent[v])
            path.push_back(v);
        reverse(path.begin(), path.end());

        for (int x : path)
            cout << x << " ";
        cout << endl;
    }

    return 0;
}

#include <iostream>
#include <vector>
#include <queue>
#include <algorithm> //sort и reverse
using namespace std;

// BFS: returns order, dist, parent
void BFS(int start,
         const vector<vector<int>> &adj,
         vector<int> &order,
         vector<int> &dist,
         vector<int> &parent)
{
    int n = (int)adj.size();
    vector<bool> visited(n, false);
    queue<int> q;

    visited[start] = true;
    dist[start] = 0;
    parent[start] = -1;
    q.push(start);

    while (!q.empty()) {
        int u = q.front(); q.pop();
        order.push_back(u);

        for (int v : adj[u]) {
            if (!visited[v]) {
                visited[v] = true;
                dist[v] = dist[u] + 1;
                parent[v] = u;
                q.push(v);
            }
        }
    }
}

// Shortest path in unweighted graph using parent+dist from BFS
vector<int> shortestPathUnweighted(int s, int t,
const vector<int> &dist,
const vector<int> &parent)
{
    vector<int> path;

    // If unreachable, return empty path
    if (t < 0 || t >= (int)dist.size() || dist[t] == -1) return path;

    // Reconstruct from t back to s
    for (int v = t; v != -1; v = parent[v]) {
        path.push_back(v);
        if (v == s) break;
    }

    // If we did not reach s, something is wrong (shouldn't happen if dist is correct)
    if (path.back() != s) return vector<int>();

    reverse(path.begin(), path.end());
    return path;
}

int main() {
    int n = 6;
    vector<vector<int>> adj(n);

    adj[0] = {1, 2};
    adj[1] = {3};
    adj[2] = {3, 5};
    adj[3] = {4};
    adj[4] = {5};

    for (auto &lst : adj) sort(lst.begin(), lst.end());

    int start = 0;
    vector<int> order;
    vector<int> dist(n, -1);
    vector<int> parent(n, -1);

    BFS(start, adj, order, dist, parent);

    cout << "BFS order: ";
    for (int x : order) cout << x << " ";
    cout << "\n";

    int t = 5;
    vector<int> path = shortestPathUnweighted(start, t, dist, parent);

    cout << "Distance " << start << " -> " << t << ": " << dist[t] << "\n";
    cout << "Shortest path " << start << " -> " << t << ": ";
    if (path.empty()) {
        cout << "No path\n";
    } else {
        for (int x : path) cout << x << " ";
        cout << "\n";
    }

    return 0;
}

#include<bits/stdc++.h>
using namespace std;

// Recursive function to find all paths in a rat maze
void solve(vector<vector<int>>& m, int n, int i, int j, string path, vector<string>& ans, vector<vector<bool>>& vis) {
    // If the rat has reached the destination cell and it's not blocked
    if (i == n - 1 && j == n - 1 && m[n - 1][n - 1] != 0) {
        ans.push_back(path); // Add the path to the list of solutions
        return; // Return to backtrack
    }

    // Check if the current cell is within the bounds of the maze, not visited, and not blocked
    if (i < n && i >= 0 && j < n && j >= 0 && !vis[i][j] && m[i][j] != 0) {
        vis[i][j] = true; // Mark the current cell as visited

        // Explore all possible directions (up, down, left, right)
        solve(m, n, i + 1, j, path + 'D', ans, vis); // Down
        solve(m, n, i, j - 1, path + 'L', ans, vis); // Left
        solve(m, n, i, j + 1, path + 'R', ans, vis); // Right
        solve(m, n, i - 1, j, path + 'U', ans, vis); // Up

        vis[i][j] = false; // Mark the current cell as unvisited for backtracking
    }
}

// Main function to find all paths in a rat maze
vector<string> ratMaze(vector<vector<int>>& mat) {
    int n = mat.size();
    vector<string> ans; // Initialize a vector to store the paths
    vector<vector<bool>> vis(n, vector<bool>(n, false)); // Initialize a boolean matrix to track visited cells

    // Start the recursive search from the top-left corner
    solve(mat, n, 0, 0, "", ans, vis);

    return ans; // Return the list of paths
}


int main() {
    // Define the maze as a 2D vector
    vector<vector<int>> maze = {
        {1, 0, 0},
        {1, 1, 0},
        {0, 1, 1}
    };

    // Find all paths in the maze
    vector<string> paths = ratMaze(maze);

    // Display the found paths
    cout << "Paths in the maze:" << endl;
    for (const string& path : paths) {
        cout << path << endl;
    }

    return 0;
}

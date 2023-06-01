# KPI_24

bool stoneGame(int* piles, int pilesSize) {
    int dp[pilesSize][pilesSize];
    
    // Initialize the diagonal values of the dp matrix
    for (int i = 0; i < pilesSize; i++) {
        dp[i][i] = piles[i];
    }
    
    // Fill the dp matrix using dynamic programming
    for (int d = 1; d < pilesSize; d++) {
        for (int i = 0; i < pilesSize - d; i++) {
            int j = i + d;
            dp[i][j] = fmax(piles[i] - dp[i + 1][j], piles[j] - dp[i][j - 1]);
        }
    }
    
    // The value in dp[0][pilesSize - 1] will represent the score difference between Alice and Bob
    // If it's positive, Alice wins; otherwise, Bob wins
    return dp[0][pilesSize - 1] > 0;
}

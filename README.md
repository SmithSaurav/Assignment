# Assignment

def attendance_probability(N):
    if N < 1:
        return "0/0"

    # Initialize DP arrays
    dp = [[0] * 4 for _ in range(N + 1)]
    dp[0][0] = 1

    for i in range(1, N + 1):
        # dp[i][0]: Ending with attendance on the ith day
        dp[i][0] = dp[i - 1][0] + dp[i - 1][1] + dp[i - 1][2] + dp[i - 1][3]
        # dp[i][1]: Ending with 1 day of absence on the ith day
        if i >= 1:
            dp[i][1] = dp[i - 1][0]
        # dp[i][2]: Ending with 2 consecutive days of absence on the ith day
        if i >= 2:
            dp[i][2] = dp[i - 1][1]
        # dp[i][3]: Ending with 3 consecutive days of absence on the ith day
        if i >= 3:
            dp[i][3] = dp[i - 1][2]

    # Total number of ways to attend classes over N days
    total_ways = dp[N][0] + dp[N][1] + dp[N][2] + dp[N][3]

    # Number of ways to miss the graduation ceremony
    ways_to_miss_graduation = dp[N][1] + dp[N][2] + dp[N][3]

    # Return the result in the required format
    return f"{ways_to_miss_graduation}/{total_ways}"


# Test cases

print(attendance_probability(5))  # Output: 14/29
print(attendance_probability(10))  # Output: 372/773

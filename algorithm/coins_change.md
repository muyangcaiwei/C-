## leetcode 518 Coin Change 2
<https://leetcode.com/problems/coin-change-2/description/>
```
relationship:
	dp[i] += dp[i - coins[j]]
	i: 0 -> amount
	j: 0->coin.size
```

```
int change(int amount, vector<int>& coins) {
	int cnt = coins.size();
	if(amount <= 0 )
		return 1;
	if(len == 0)
		return 0;
	vector<int> dp(amount + 1, 0);
	dp[0] = 1;
	//dp[coins[0]] = 1;
	for(int i = 0; i < cnt ; i++)
	{
		for(int j = coins[i]; j <= amount; j++)
		{
			dp[j] += dp[j - coins[i]];
		}
	}
	return dp[amount];
}
```
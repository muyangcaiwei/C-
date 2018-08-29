## Separate word
<https://www.geeksforgeeks.org/word-break-problem-dp-32/>

<https://leetcode-cn.com/problems/word-break/description/>

```c++
dp[i] : if str[0,i] could be separated
    dp[i] = true //if dp[j](j < i) is true and str[j to i] is a word
          = false //if not
    dp[0] = true;
eg: 
the str is : ilikemango, 
the word set is:{"mobile","samsung","sam","sung","man","mango","icecream","and","go","i","like","ice","cream"};
the dp[1] is true, because dp[0] is true and "i" is a word
the dp[4] is true, because dp[1] is true and "like" is a word too
```

```c++
bool isSepWord(string str, vector<string> &set_)
{
	for(int i = 0; i < set_.size(); i++)
	{
		if(str == set_[i])
			return true;
	}
	return false;
}

bool sepWord(string &str, vector<string> &set_)
{
	int len = str.size();
	vector<bool> dp(len + 1, false);
	dp[0] = true;
	for(int i = 1 ; i <= len; i++)
	{
		for(int j = 0; j < i ;j ++)
		{
			string t = str.substr(j, i - j );
			dp[i] = dp[j] && isSepWord(t, set_);
			if(dp[i])
				break;
		}
	}
	return dp[len];
}
```
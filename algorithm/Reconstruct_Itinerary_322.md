### 332. Reconstruct Itinerary
***
Given a list of airline tickets represented by pairs of departure and arrival airports [from, to], reconstruct the itinerary in order. All of the tickets belong to a man who departs from JFK. Thus, the itinerary must begin with JFK.
Note:
If there are multiple valid itineraries, you should return the itinerary that has the smallest lexical order when read as a single string. For example, the itinerary ["JFK", "LGA"] has a smaller lexical order than ["JFK", "LGB"].
All airports are represented by three capital letters (IATA code).
You may assume all tickets form at least one valid itinerary.
***

```C++
Example 1:
Input: [["MUC", "LHR"], ["JFK", "MUC"], ["SFO", "SJC"], ["LHR", "SFO"]]
Output: ["JFK", "MUC", "LHR", "SFO", "SJC"]
Example 2:
Input: [["JFK","SFO"],["JFK","ATL"],["SFO","ATL"],["ATL","JFK"],["ATL","SFO"]]
Output: ["JFK","ATL","JFK","SFO","ATL","SFO"]
Explanation: Another possible reconstruction is ["JFK","SFO","ATL","JFK","ATL","SFO"].
But it is larger in lexical order.
```

思想：DFS，借由multiset自动排序，借助stack采用自底向上的方法获取输出

```C++
class Solution {
public:
    vector<string> findItinerary(vector<pair<string, string>> tickets) {
        map<string, multiset<string>> procedure;
		for(int i = 0 ;i < tickets.size(); i++)
		{
			procedure[tickets[i].first].insert(tickets[i].second);
		}
		stack<string> st;
		vector<string> result;
		st.push("JFK");
		while(!st.empty())
		{
			string from = st.top();
			if(procedure[from].empty)
			{
				result.push_back(from);
				st.pop();
			}else
			{
				st.push(*(procedure[from].begin()));
				procedure[from].erase(procedure[from].begin());
			}
		}
		reverse(result.begin(), result.end());
		return result;
    }
};
```
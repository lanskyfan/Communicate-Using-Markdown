# This is the new header written by Yifan Lan
## How about a smaller one
![Image of Yaktocat](https://octodex.github.com/images/yaktocat.png)
```
/// why don't we do some LeetCode
class Leaderboard {
    TreeMap<Integer, Integer> scores;
    Map<Integer, Integer> players;
    public Leaderboard() {
        scores = new TreeMap(Collections.reverseOrder());
        players = new HashMap();
    }
    
    public void addScore(int playerId, int score) {
        int old = players.getOrDefault(playerId, 0);
        players.put(playerId, old + score);
        if (old != 0) {
            scores.put(old, scores.get(old) - 1);
        }
        int newValue = scores.getOrDefault(old + score, 0);
        scores.put(old + score, newValue + 1);
    }
    
    public int top(int K) {
        int total = 0;
        int count = 0;
        for(Map.Entry<Integer, Integer> ent: scores.entrySet()) {
            if (count + ent.getValue() >= K) {
                total += ent.getKey() * (K - count);
                return total;
            }
            total += ent.getValue() * ent.getKey();
            count += ent.getValue();
        }
        return total;
    }
    
    public void reset(int playerId) {
        int score = players.get(playerId);
        players.remove(playerId);
        scores.put(score, scores.get(score) - 1);
    }
}
```

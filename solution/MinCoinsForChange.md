# Min Number Of Coins For Change
## 문제 설명
동전(denoms)들이 주어질 때, 잔돈 n을 만들 수 있는 가장 적은 동전 갯수를 출력하라.

잔돈을 만들 수 없을 경우 `-1`을 출력하라.
## 예제 입출력
- n: `7`
- denoms: `[1, 5, 10]`
- result: `3`

## 풀이
### O(n) 시간, O(n) 메모리 방식
동적 프로그래밍으로 memoization 해서 풀 수 있음.

minNum 벡터(또는 배열)를 INT_MAX최대값으로 초기화.

현재 minNum 값과 동전값 만큼 뺏을 때의 최소 동전수+1(현재 동전을 더한다 가정) 중 작은 값을 선택.
```c++
#include <vector>
#include <climits>
using namespace std;

int minNumberOfCoinsForChange(int n, vector<int> denoms) {
	vector<int> minNum(n+1, INT_MAX);
	
	minNum[0] = 0;
	for (int d: denoms) {
		for (int amount=0; amount<=n; amount++) {
			if (amount == d) {
				minNum[amount] = 1;
			} else if (amount > d) {
				if (minNum[amount-d] != INT_MAX) {
					minNum[amount] = min(minNum[amount-d] + 1, minNum[amount]);
				}
			}
		}
	}
	return minNum[n] != INT_MAX? minNum[n]: -1;
}

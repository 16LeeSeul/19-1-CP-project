## 1번.
수빈이는 TV를 보고 있다. 수빈이는 채널을 돌리려고 했지만, 버튼을 너무 세게 누르는 바람에, 일부 숫자 버튼이 고장 났다.  
리모컨에는 버튼이 0부터 9까지 숫자, +와 -가 있다. +를 누르면 현재 보고 있는 채널에서 +1된 채널로 이동하고, -를 누르면 -1된 채널로 이동한다.  
채널 0에서 -를 누른 경우에는 채널이 변하지 않고, 채널은 무한대 만큼 있다.  
수빈이가 지금 이동하려고 하는 채널은 N이다.  
어떤 버튼이 고장 났는지 주어졌을 때, 채널 N으로 이동하기 위해서 버튼을 최소 몇 번 눌러야 하는지 구하는 프로그램을 작성하시오.  
수빈이가 현재 보고 있는 채널은 100번이다.  
  
  
* 첫째 줄에 수빈이가 이동하려고 하는 채널 N(0<=N<=500,000)이 주어진다.
* 둘째 줄에 고장이 난 버튼의 개수 M(0<=M<=10)가 주어진다.
* 고장이 난 버튼이 있는 경우에는 셋째 줄에 고장이 난 버튼이 주어지며, 이 때 같은 버튼이 여러 번 주어지는 경우는 없다.
  
**출력**
-> 채널 N으로 이동하기 위해 버튼을 최소 몇 번 눌러야 하는지 출력
  
  

```
#include <stdio.h>

typedef struct 
{
	int res;
	int cnt;
}Answer;

Answer find(int N, int wrong[]) 
{
	Answer ans;
	ans.res = 0;
	ans.cnt = 0;

	while (N > 0)
	{
		if (wrong[N % 10] == 1)
		{
			ans.res = 1;
		}
		N = N / 10;
		ans.cnt++;
	}

	return ans;
}

int main()
{
	int N, M, num, cnt = 0, min = 500001, i;
	Answer ans;
	int wrong[10] = { 0 };


	printf("채널 입력 : ");
	scanf("%d", &N);
	printf("고장난 버튼의 개수 입력 : ");
	scanf("%d", &M);
	printf("고장난 버튼 입력 : ");
	for (int i = 0; i < M; i++)
	{
		scanf("%d", &num);
		wrong[num] = 1;
	}


	for (i = 0; i < 1000000; i++)
	{
		ans = find(i, wrong);
		if (ans.res == 0)
		{
			cnt = i - N;
			if (cnt < 0)
				cnt = (-1)*cnt;
			cnt = cnt + ans.cnt;
			if (cnt < min)
				min = cnt;
		}

	}

	cnt = N - 100;
	if (cnt < 0)
		cnt = (-1)*cnt;

	if (cnt < min)
		min = cnt;

	printf("버튼 누르는 최소 횟수 : %d", min);

}
```

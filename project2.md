## 2번.

농부 John은 소들의 저녁식사 줄 세우는 새로운 방법을 개발하였다.  
N(1~15)마리의 소들을 순서대로 세워놓은 후, 각 소들 사이에 +, - , . 셋 중 1가지가 써져 있는 냅킨을 배치해서 최종 결과가 0이 되게 하는 것이다.  
점(.)이 써져 있는 냅킨을 통해 더 큰 수를 만들 수 있게 된다. 점(.) 냅킨은 ‘공백＇이라고 생각하면 된다.  

1 – 2 . 3 – 4 . 5 + 6 . 7  
이와 같은 배치는 1-23-45+67을 나타낸다. 결과는 0이다.  
즉, 10.11은 1011로 해석하면 된다.  

* 힌트) 재귀호출함수 사용

**[입력]**  
소들의 수 N이 입력된다

**[출력]**  
* 처음 20줄에 대해 가능한 20가지 답을 출력하는데, 사전 순으로 앞선 것을 출력한다.
* 순서는 +가 가장 앞서고 –와 .이 순서대로 뒤따른다.
* 답이 20개 미만이면 가능한 답을 각 숫자와 문자 사이에 공백을 두고 출력한다
* 마지막 줄에는 가능한 답의 총 가지 수를 출력한다

  
```
#include <stdio.h>
#include <math.h>

static int arr[20] = { 0 };
static int change[20] = { 0 };
static char cal[15];
static char cal1[15];
static int cow;
static int cnt = 0;


int cowline(int current, int what, int cow, char cal[], int arr[], int change[], char cal1[])   
{
	int j, k;
	int a = 0;
	int all = cow - 1;
	int sum, dec, dec1 = 0;

	if (what == 1) {
		cal[current] = '+'; //+
		current++;
	}
	else if (what == 2) {
		cal[current] = '-'; //-
		current++;
	}
	else if (what == 3) {
		cal[current] = '.'; //.
		current++;
	}


	if (current == (cow - 1))
	{
		//		memcpy(change, arr, sizeof(arr));
		for (j = 0; j < cow; j++)
			change[j] = arr[j];

		for (j = 0; j < cow - 1; j++)
			cal1[j] = cal[j];


		for (j = 0; j < cow - 1; j++)
		{
			if (cal[j] == '.')
			{
				//dec = change[j - a + 1];
				//while (dec)
				//{
				//	dec = dec / 10;
				//	dec1++;
				//}
				if (change[j - a + 1] < 10) // 100마리 이하일 때만 가능
					dec1 = 1;
				else
					dec1 = 2;

				change[j - a] = pow(10, dec1) * change[j - a] + change[j - a + 1];
				for (k = j - a; k < cow; k++)
				{
					change[k + 1] = change[k + 2];
					cal1[k] = cal1[k + 1];
				}
				a++;
				all--;
			}
		}

		sum = change[0];
		for (j = 0; j < all; j++)
		{
			if (cal1[j] == '+')
			{
				sum = sum + change[j + 1];
			}
			else if (cal1[j] == '-')
			{
				sum = sum - change[j + 1];
			}
		}

		if (sum == 0)
		{
			cnt++;
			if (cnt <= 20)
			{
				for (j = 0; j < cow - 1; j++)
				{
					printf("%d ", arr[j]);
					printf("%c ", cal[j]);
				}
				printf("%d\n", arr[cow - 1]);
			}

		}

	}
	else
	{
		cowline(current, 1, cow, cal, arr, change, cal1);
		cowline(current, 2, cow, cal, arr, change, cal1);
		cowline(current, 3, cow, cal, arr, change, cal1);
	}

}

int main()
{
	int cow;
  scanf("%d", &cow);

	for (int i = 0; i < cow; i++)
	{
		arr[i] = i + 1;
		change[i] = i + 1;
	}

	if (cow == 1)
	{
		printf("0");
	}
	else
	{
		cowline(0, 1, cow, cal, arr, change, cal1);
		cowline(0, 2, cow, cal, arr, change, cal1);
		cowline(0, 3, cow, cal, arr, change, cal1);
		printf("%d", cnt);
	}

}
```

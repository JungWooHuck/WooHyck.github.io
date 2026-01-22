#include <stdio.h>
#define ROWS 3
#define COLS 3
//행렬 전치 함수
void matrix_transpose(int A[ROWS][COLS], int B[COLS][ROWS]) { 
	//의문점: 1차원 배열의 경우에는 매개변수로 될 시 포인터 처럼 작동한다. 그럼 2차원 배열도..?
	//의문점: 만약 첫번째 요소의 주소만을 넘긴다면, 한 행에 몇개가 있는지, 혹은 한 열에 몇개가 있는지의 정보가 있어야 하는것 아닌가?
	for (int r = 0; r < ROWS; r++)
		for (int c = 0; c < COLS; c++)
			B[c][r] = A[r][c]; //모든 matrix 요소의 행과 열을 바꾸어, 행렬 전치,
}

void matrix_print(int A[ROWS][COLS]) {
	
	printf("==========================\n");
	for (int r = 0; r < ROWS; r++) {
		for (int c = 0; c < COLS; c++)
			printf("%d ", A[r][c]);
		printf("\n");
	}
	printf("==========================\n");
}

int main() {
	int array1[ROWS][COLS] = {{2,3,0},
								{8,9,1},
								{7,0,5}};
	int array2[COLS][ROWS];

	matrix_transpose(array1, array2);
	matrix_print(array1);
	matrix_print(array2);
	return 0;
}

//2차원 배열을 매개변수로 사용 할 경우.
(자료형 매개변수[][가로 길이]) 혹은
(자료형 (*매개변수)[가로길이]) 으로 한다.
자 우선은 1차원 배열의 경우에는 함수의 매개변수로 사용할 경우, 마치 포인터처럼 취급된다. 
그러나, 2차원 배열의 경우에는 int형 더블포인터로 취급하면 안된다. 이것이 더 괜찮은 해석이다. "행이 고정된 1차원 배열"

전제로 일단
1.
int arr2d[3][3]; 
여기에서 print("%d")를 한다고 가정하였을떄, arr2d = arr2d[0] = &arr2d[0][0]   (이 식은 c언어 문법이 아닌, 단순히 3개가 같다는 뜻이다. 당연히 셋의 타입은 다르다.)
sizeof(arr2d) 로 한다면, sizeof(arr2d) = 36, sizeof(arr2d[0]) = 12 이다. 즉 arr2d는 첫번째 요소를 가르키되, 배열 전체 의미를 내포한다. arr2d[0] 도 첫번째 요소를 가르키지만 1행 만을 의미 내포한다.

2.
int arr[3] 과 double darr[7] 이 있다고 치자 각각 배열명은 int 형, double 형 포인터다.
그렇다면 printf("%p %p", iarr+1, darr+1) 을 한다면 각각 iarr+sizeof(int), darr+sizeof(double) 만큼이 출력된다.

이 두 전제에서 다시 본론으로 돌아가보자.
2차원 배열에 있어서
int arr1[3][2] 과 int arr2[2][3]; 이렇게 다르지만, 같은 요소 수의 배열 두 개가 있다. 하지만
arr 과 arr+1 의 주소 차이는 8, arr2와 arr2+1의 주소차이는 12로 다르다. 즉 열길이에 따라서 달라지는 거다.
결론: 2차원 배열이름의 포인터형에는: 가르키는 대상과 배열명(포인터) 대상으로 1증가시, 실제로는 얼마나 증가? (열의 정보) 가 있어야 한다.
==> int (*ptr)[4] 이런 식이거나 혹은 int ptr[][4] 이렇게 매개변수로 보내야 한다.
(int ptr[2][3] 이렇게 매개변수로 보낼경우, c언어에서는 [2] 즉 행의 정보는 타입에 포함되지 않는다.


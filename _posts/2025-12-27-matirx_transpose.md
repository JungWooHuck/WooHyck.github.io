#include <stdio.h>
#include <stdlib.h>

#define MAX_TERMS 100
typedef struct {
	int row; //행 인덱스
	int col; // 열 인덱스
	int value; // 행,열 에 저장된 0이 아닌 숫자 값.
}element;

typedef struct SparseMatrix {
	element data[MAX_TERMS]; //구조체 안에 구조체 배열을 멤버로 넣었다.
	int rows;   //행의 수
	int cols;   //열의 수
	int terms;  //항의 수
}SparseMatrix;

SparseMatrix matrix_transpose2(SparseMatrix a) { 
	//이 함수는 SprseMatrix 가 반환형이며, 동시에, SparseMatrix a 라는 SparseMatrix반환형 변수 a를 매개변수로 삼았다.
	SparseMatrix b;
	//또 다른 구조체변수를 선언.
	int bindex; //행렬 b에서 현재 저장 위치
	b.rows = a.cols;  //우선 총 행의 수를 열의 수와, 또 열의 수를 행의 수와 바꿔 대입한다. (전치 연산 하기 때문에)
	b.cols = a.rows;

	b.terms = a.terms;

	if (a.terms > 0) { 
		bindex = 0; 
		for (int c = 0; c < a.cols; c++) { //열의 수만큼 반복. ==> 열과 행을 전치 시기는 것과 동시에 오름차순 행으로 저장해야 한다.
			//즉 이 고려점 때문에, 0열 부터 있는 요소를 찾아서 전치행렬의 0행에 저장, 1열에 있는 요소를 찾아서 1행으로,.., 이렇게 하는거다/
			for (int i = 0; i < a.terms; i++) { //이중반복인다 위의 서술처럼, 모든 항을 순회하며 검사하는거다.
				if (a.data[i].col == c) { // ==c 처리를 하는 조건문, 즉 모든 항을 검사하되, 현재 열에 속한 항인지 보는 것이다.
					b.data[bindex].row = a.data[i].col; //만약 맞을 경우, b의 data[bindex]의 행을 a의 data[i].col 의 열과 바꾼다.
					b.data[bindex].col = a.data[i].row;  //이 식들은, 총 수가 아닌, 그 항에 대응되는 행과 열 정보값을 바꾼 값을 b에 저장하는거다. 
					b.data[bindex].value = a.data[i].value;
					bindex++;//bindex가 올라간다. 다음으로 저장할 빈 공간 인덱스를 카르킨다.
				}
			}
		}
	}
	return b;
}

void matrix_print(SparseMatrix a) {
	printf("=====================\n");
	for (int i = 0; i < a.terms; i++) {
		printf("(%d, %d, %d) \n", a.data[i].row, a.data[i].col, a.data[i].value);
	}
	printf("=====================\n");
}

int main() {
	SparseMatrix m = {
		{{0,3,7},{1,0,9},{1,5,8},{3,0,6},{3,1,5},{4,5,1},{5,2,2}}, // 이게 element data[MAX_TERMS]; 에 들어가는 거다. 
		6,
		6,
		7  
	};
	SparseMatrix result;

	result = matrix_transpose2(m);
	matrix_print(result);
	return 0;
}
//이 코드의 경우에는 전치행렬에 대해서, 0인 불필요한 공간을 모두 생략할 수 있는 코드이다.
//전 코드와 달리 0의 공간을 쓰지 않아도 되는 장점이 있으나, 코드가 조금 복잡하다는 단점이 있다.

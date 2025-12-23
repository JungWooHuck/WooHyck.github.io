시스템 스택(System Stack): 컴퓨터 프로그램이 함수를 호출하고 복귀할 때 실행 순서를 관리하기 위해 사용하는 메모리 영역

어떠한 함수든 간에, 함수가 호출된다면, 이 시스템 스택에 
복귀 주소가 저장되고. 매개변수, 지역변수를 할당한다.
즉 중요한 것은 스택의 특징은
: 계속 쌓여나감, 빠질땐 마지막으로 쌓인 것 부터, 순서대로 빠져나감.
이므로 
int factorial(int n){
  if (n<=1) return(1);
  else return (n * factorial(n-1));
}
에서 만약 n = 3 을 대입하였다고 치면, 
factorial(3) -> factorial(2) -> factorial(1) 이렇게 호출되지만.
함수가 끝난다면, 스택의 규칙대로 반대로 factorial(1) 부터 factorial(3) (복귀주소로 통하여) 으로 간다. 

이때, 매 호출마다 C언어는 지역변수가 시스템스택에 계속 독립적으로 새롭게 할당되어 지기 때문에 순환호출이 가능하다. 
COBOL 과 같은 고전적 언어는 불가능하다.

int factorial(int n){
  printf("factorial(%d)\n",n);
  if(n<=1)return(1);
  else return(n * factorial(n-1));
}
이런 경우에는 printf문은 마주치자마자, 실행 되기에 factorial(3) 부터 (1) 까지 순서대로 출력된다.

int factorial(int n){
    if(n <= 0) return 1;

    int result = n * factorial(n-1);
    printf("factorial(%d)\n", n);   
    return result;
} 
이 코드를 보면 재귀 함수 호출 이후에 printf문이 있다. 
즉 이 코드를 실행하면, 의도대로 factorial(1) 부터 factorial(3)까지 순서대로 출력된다.
이를 후입선출법, 스택의 성질인 LIFO 라고도 부른다.

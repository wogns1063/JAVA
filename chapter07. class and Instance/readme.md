# Chapter07. 클래스와 인스턴스
## 07-1 클래스의 정의와 인스턴스의 생성.
#### 7-1.1 객체지향 프로그래밍의 이해
1. 객체 = 물건, 또는 대상
* (ex) 나는 과일장수에게 두 개의 사과를 구매했다.
* (ex)의 객체 : **나, 과일장수, 사과**
<hr>

#### 7-1.2 클래스(class)라는 틀을 기반으로 객체가 생성됩니다.

1. 객체를 생성하기 전에는 클래스를 만들어야 합니다.
2. 클래스의 구성 방식으로는 **변수 선언, 메소드 정의**를 해야 합니다.
3. (ex) 클래스 내의 변수 및 메소드 정의
```
Class FruitSeller
{
    int numOfApple = 20;
    int myMoney = 0;
    
    public int SaleApple(int money)
    {
        int num = money/1000;
        numOfApple -= num;
        myMoney += money;
        return num;
    }
}
```
<hr>

#### 7-1.3 final이란?
1. **(Step1). final int APPLE_PRICE;** 이렇게 선언되면 
다음과 같이 딱 한 번만 초기화 해야 한다.
**(Step2). APPLE_PRICE=1000;**
2. **한 번 값이 결정된 이 변수의 값은 변경이 불가능하다!!!**

<hr>

#### 7-1.4 클래스를 기반으로 객체 생성하기.
1. 다음은 객체를 생성하는 법이다.
* **FruitBuyer buyer = new FruitBuyer();**
2. 위의 내용에서 **buyer는 참조변수(reference)** 라고 한다.
3. 객체를 생성하는 행위를 **인스턴스화(instance)** 라 한다.
4. 객체를 생성하면 메모리가 할당된다.
<hr>

#### 7.1.5 참조변수와 메소드의 관계

```
public void myMethod()
{
    FruitSeller seller1 = new FruitSeller();
    instMethod(seller1)
}
public void instMethod(FruitSeller seller2){
    //생략
}
```
1. 첫 번째 경우.
* 참조변수가 메소드의 인자로 전달되면, **동일한 형태의 객체가 생성**된다.

2. 두 번째 경우.
* 매개변수(parameter) seller2가 seller1의 주소 값이 전달된다.
* 즉, 참조변수 seller1, seller2가 **하나의 객체를 동시에 참조한다.**

3. 둘 중에 무엇이 맞는지 확인해보자!
```
Class Number
{
    int num = 0;
    public void addNum(int n)
    {
        num += n;
    }
    public int getNumber()
    {
        return num;
    }
}
Class PassInstance
{
    public static void main(String[] args)
    {
        Number nInst = new Number();
        System.out.println("메소드 호출 전 : " + nInst.getNumber();
       
       simpleMethod(nInst);
       System.out.println("메소드 호출 후 : " + nInst.getNumber();
    }
    public static void simpleMethod(Number numb)
    {
        numb.addNum(12);
    }
}
```
* 답은 **두 번째 경우이다**
* 실행결과 
   - 메소드 호출 전 : 0 <br>
   메소드 호출 후 : 12
* 참조변수가 메도의 인자로 전달되면 주소값이 넘어간다.<br> 즉,  **하나의 객체를 둘이 참고한다.**
<hr>

## 07-2 생성자(Constructor)
1. 클래스의 이름과 동일한 이름의 메소드
2. 생성자를 이용하면 인스턴스 변수의 초기화를 수월하게 진행할 수 있다.
3. (ex)
```
class Number
{
    int num;
    public Number(int n)
    {
        num = n;
        System.out.println("인자 전달 : " + n);
    }
    public int getNumber()
    {
        return num;
    }
}

class Constructor2
{
    public static void main(String[] args)
    {
        Number num1 = new Number(10);
        System.out.println( "메소드 반환 값 : " +num1.getNumber());
        
        Number num2 = new Number(20);
        System.out.println( "메소드 반환 값 : " +num2.getNumber());
    }
}
```
* 실행결과 
  - 인자 전달 : 10<br>
  메소드 반환 값 : 10<br>
  인자 전달 : 20<br>
  메소드 반환 값 : 20<br>

* 생성자를 쓰면 인스턴스의 변수 초기화를 할 수 있다.

<hr>

## 07-3 과일장수 예제 완성
```

public class Fruit {
	public static void main(String[] args)
	{
		FruitSeller seller1 = new FruitSeller(30, 0, 1500);
		FruitSeller seller2 = new FruitSeller(50, 0, 2000);
		FruitBuyer buyer = new FruitBuyer(20000);
		buyer.buyApple(seller1, 4500);
		buyer.buyApple(seller2, 10000);
		System.out.println("과일 판매자 1 상황");
		seller1.showFruitSeller();
		System.out.println("과일 판매자 2 상황");
		seller2.showFruitSeller();
		System.out.println("구매자 상황");
		buyer.showFruitBuyer();
	}
}

class FruitSeller
{
	int numOfApple;
	int myMoney;
	final int APPLE_PRICE;
	
	public FruitSeller(int num, int money, int price) 
	{
		APPLE_PRICE = price;
		numOfApple = num;
		myMoney = money;
	}
	
	public int saleApple(int money) 
	{
		int num = money/APPLE_PRICE;;
		myMoney+=money;
		numOfApple -= num;
		return num;
	}
	
	public void showFruitSeller()
	{
		System.out.println("현재 남은 사과 수 : " + numOfApple);
		System.out.println("사과장수 돈 : " + myMoney);
	}
}

class FruitBuyer
{
	int numOfApple;
	int myMoney;
	
	public FruitBuyer(int money)
	{
		numOfApple = 0;
		myMoney = money;
	}
	
	public void buyApple(FruitSeller seller, int money)
	{
		numOfApple += seller.saleApple(money);
		myMoney -= money;
	}
	
	public void showFruitBuyer()
	{
		System.out.println("현재 구입한 사과 수 : " + numOfApple);
		System.out.println("구입한 손님 돈 : " + myMoney);
	}
}
```

* 실행결과
  - 과일 판매자1 상황<br>
  현재 남은 사과 수 : 27<br>
  사과장수 돈 : 4500<br>
  과일 판매자2 상황<br>
  현재 남은 사과 수 : 45<br>
  사과장수 돈 : 10000<br>
  구매자 상황<br>
  현재 구입한 사과 수 : 8<br>
  구입한 손님 돈 : 5500




# chapter 11

> ### 연산자 오버로딩

    - 기본적으로 연산자를 이용한 사용자 정의 객체의 사칙연산은 바로 사용 할 수없다.
    - operator연산자() 를 사용하여 연산자를 오버로딩해 사용할 수 있다.
    - 연산자 오버로딩 후 연산자를 사용하면 컴파일러가 연산자를 연산자 함수로 대체한다.
    ex) Stock operator+(const Stock & s) const;
        {
            Stock temp;
            temp.val1 = this->val1 + s.val1;
            temp.val2 = this->val2 + s.val2;

            retrun temp;
        }

> ### 오버로딩 제약

    - 오버로딩된 연산자는 적어도 하나의 피연산자가 사용자 정의 데이터 형이여야 한다.
        -- 이는 표준 데이터형을 위해 사용되는 연산자를 오버로딩 하는것을 막아준다.
    - 오버로딩된 연산자를 오리지널 연산자에 적용되는 문법 규칙을 위반하는 방식으로 사용할 수 없다.
        -- ex)하나의 피연산자에만 적용 가능한 %연산자는 만들 수 없다.
        -- 정해진 연산자 우선순위도 변경 할 수 없다.
    - 연산자 기호를 새로 만들 수 없다.
    - 'sizeof', '.', '.*', '::', '?:' 등의 연산자는 오버로딩 할 수 없다.
    - 'typeid', 'const_cast', 'dynamic_cast', 'reinterpret_cast', 'static_cast'도 마찬가지
    - '=', '()', '[]', '->' 연산자는 멤버 함수만 사용할 수 있다.

> ### 프렌드
    
    - 프렌드 함수, 프렌드 클래스, 프렌드 멤버 함수
    - 클래스의 private 멤버에 접근할 수 있는 권한을 준다.
    - 클래스 선언에 friend를 붙여 함수의 원형을 선언해준다.
    - 이후 함수를 정의할때 외부함수 처럼 범위 지정자 없이 정의하고 사용한다.
    - 멤버 함수와 동등한 접근 권한을 가지는 멤버가 아닌 함수가 된다.
    - operator*을 클래스의 프렌드 함수로 만들어 오버로딩 하는 경우
        -- A = 2.75 * B 와 같은 경우
        -- A = operator*(2.75 * B)와 같이 프렌드 함수가 호출된다.
        -- 첫 번째 피연산자가 클래스 형이 아닐때 프렌드 함수를 사용해보자

> #### note) 프렌드는 oop에 어울리지 않는다?
    
    - 데이터 은닉을 위반하는 것처럼 보인다.
    - 프렌드 함수는 클래스를 위한 확장 인터페이스의 일부라고 생각해야한다.
    - 클래스 함수와 프랜드 함수는 클래스 인터페이스를 나타내는 서로다른 메커니즘이다.

> ### operator<<

    ostream& operator<<(ostream & os, const myclass & t)
    {
        os << myclass.m_one << "something"<<myclass.m_two<<"something2"<<endl;
        return os;
    }
    - 이와 같은 형태로 오버로딩 한다, myclasss의 멤버를 사용하기 때문에 myclass에 프렌드 선언
    -- operator<<(cout, classobject) 형태로 함수 호출이 된다고 생각할것.

> ### 데이터형 변환

    - 클래스형을 다른 클래스형 또는 데이터형으로 변환하는 것을 허용한다.
    - 하나의 매개변수를 사용하는 클래스 생성자는 변환함수 처럼 동작
        -- 매개변수 데이터형의 어떤 값을 클래스형으로 변환한다.
        -- char*형 값을 매개변수로 사용하는 생성자가 string클래스에 있다면
        -- string클래스 객체 bean, bean = "pinto"라는 구문은 char*형을 string형으로 변경한다.
        -- 생성자 선언 앞에 explicit가 있는 경우 bean = string("pinto"); 처럼 명시적으로 표현
    - 클래스를 다른 데이터형으로 변환 하려면 변환 함수를 정의한다.
        -- myclass::operator double()
        {
            ...
            return result_value
        }
        -- myclass형을 vector형으로 변환하는 경우, 리턴값, 매개변수 없이 표현
        -- 암시적 변환 함수는 되도록 사용하지 말자.

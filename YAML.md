# YAML/YML(Yaml Ain't Markup Language)

## 1. What is YAML?
타 시스템 간에 데이터를 주고 받을 필요가 있을때 데이터의 연동과 호환을 위해 포맷에 대한 규칙이 필요하다. 웹에서는 주로 XML과 JSON을 사용하고 자바 프로젝트에서는 properties 파일을 사용해왔다.  
그러나 XML은 사용하기 매우 까다롭고 가독성이 좋지 않고 JSON은 주석을 달 수 없고 쓸데없는 중괄호와 대괄호의 남발로 코드 길이가 강제적으로 길어지는 단점이 있다. 이러한 사용하기 복잡한 점 때문에 2001년에 Clar Evans에 의해 최초로 제안된 새로운 포매팅 방식이 YAML/YML이다.  
![image](https://github.com/choiyun9yu/OperatingSystem/assets/110392046/1ff29897-c412-4a15-b96a-d5eecb520161)

yaml은 xml과 json 포맷과 같이 타 시스템 간에 데이터르 주고 받을 때 약속된 포맷(규칙)이 정의되어 있는 또하나의 파일 형식이다. 다만 좀 더 인간 친화적으로 작성해 가독성을 높였다. 그래서 고급 컴퓨터 언어에 더 친화적이다.

#### .yaml과 .yml의 차이점
사실 차이점은 없다 예전에 windows에서는 파일확장자가 3글자로 제한되는 특성이 있었기 때문에 .yml을 사용했다.

## 2. Grammar of YAML

### 2-1. 기본 문법
- 문서의 시작 표시 ---
- 문서의 끝 표시 ...
- 주석 #
  
#### 기본 표현
key: value 로 표현하며, 콜론(:) 다음에는 무조건 공백 문자가 와야한다.  

    key: value
      key_1:
        key_2:
          key_3:

#### 자료형
int, string, boolean을 지원한다.  

    int_type: 1
    string_type: "1"
    boolean_type: true

#### Object 표현

    key:
      key: value
      key: value

  # 또는

  key: {
    key: value,
    key: value
  }

#### List 표현

    key:
      - item
      - item
    
    # 또는
  
    key: [
      item, item
    ]


#### Text 표현
(|) 기호와 (>) 기호가 있다. (|)는 줄바꿈을 포함하고, (>)는 줄바꿈을 무시한다.  

    comment_line_break: |
      Hello my name is yun.
      Im developer.
  
    comment_single_line: >
      Hello World
      my first yml syntax.

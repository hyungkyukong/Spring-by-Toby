#스프링 부트 시작하기 

*스프링 부트* 
- 스프링 부트는 어떠한 라이브러리, 프레임워크다. 이런 정의가 공식적으로 없다. 
- 스프링을 기반으로 독립실행형 애플리케이션을 고민없이, 빠르게 작성할 수 있게 도와주는 여러가지 
  고두의 모음이다. 
  
##스프링 부트의 핵심 목표 
- 매우 빠르고 광범위 하게  스프링개발 경험을 제공 한다. 
  간단한 설정 만으로 빠르게 스프링 애플리케이션을 띄울 수 있다는 의미가 된다. 
  이전에는 많은 설정을 해야 했지만 스프링부트는 그 해결을 알아서 해준다. 

- 강한 주장을 가지고 즉시 적용 가능한 기술 초합을 제공하면서, 필요에 따라 원하는 방식으로 손쉽게 변경 가능 
  스프링부트가 어떠한 기술응 가지고 어떻게 개발을 하면된다는 식의 강한 자기의 주장이 있어서 
  그 주장에 따라 개발하면은 빠르게 개발이 가능하다.
  하지만 주장믈 우리에 입맛에 맞게 변경해서 사용도 가능하다. 
  
- 프로젝트에서 필요로 하는 다양한 비기능적인 기술(내장형 서버, 보안, 메트릭, 상태 체크, 외부 설정 방식 등) 을 제공한다. 

- 이전에는 스프링의 설정을 xml 파일로 많이 사용해 왔다. 하지만 스프링부트에서는 이런 방식을 추구하지 않도 다른 
  방식으로 진행한다. 이것은 차차 알아 가도록 하자. 
  
  
##스프링 부트의 역사
- 어느 유저가 containerless 웹 애플리케이션 아키텍쳐 스프링 기능을 개선했으면 좋겠다는 
  글을 올리면서 시작됐다. 

- 웹개발을 하려면 전통적인 자바 웹에 대한(웹 컨테이너 같은) 지식을 알아야 개발이 가능했다. 
  유저들은 node, 파이선 같이 지식 없이 빠르게 개발을 시작할 수 있는 것을 원했다. 
  개발자들은 이게 수긍했다. 

- 스프링 개발자들은 스프링에 이거를 녹여 내기보다는 스프링부트라는 새로은 프로젝트를 개발하게 됐다. 
  
  
##Containerless 
- 말그대로 컨테이너 없이 개발하자 이런 의미인거 같은데? 
  Serverless와 비슷한 의미르르 가지는데 Serverless는 설치, 관리 이런 부분을 개발자 들이 신경 쓰지 않고 
  서버 애플리케이션을 개발하고 운영하는것을 의미한다. 
  Containerless도 이것과 의미가 비슷하다. 
  
##Container  
![image](https://github.com/user-attachments/assets/1f8a641e-ab66-4bcf-91aa-29d6ec0e3a04)
Web Client는 요청을 하고 
Web Component는 반환을 한다. 

![image](https://github.com/user-attachments/assets/801b0cf8-0016-4471-913f-bc4355df1641)
web Component는 Web Container안에 항상 들어가 있어야 한다. 

Web Client는 요청을 하고 
Web Component는 반환을 한다. 


Web Container가 하는일은 여러일이 있다. 

- 컴포넌트의 라이프 사이클을 관리한다. 메모리에 생성하고 인스턴스화 하고 이런것들..? 
- web component를 가지고있지 않고 여러개의 컴포넌트를 가지고 있을 수 있다. 
- Web client에서 요청을 어느 컴포넌트가 담당할지에 대해 연결해주는 작업을 한다. 
  이런 행동을 라우팅 또는 매핑이라고 지칭한다. 
  
  
자바에서는 web component-> Servlet이라고 불린다. 
이런 서블릿을 관리해주는 컨테이너가 서블릿 컨테이너로 불린다.
유명한 서블릿 컨테이너 중에는 톰캣이 있다. 

Spring Container는 
아래 이미지 처럼  
서블릿 컨테이너 뒤에 존재하게 되고 서블릿 컨테이너 중 서블릿이 스프링 컨테이너한테 
데이터를 넘겨주면 스프링 컨테이너는 스프링 안에 있는 컨페이너(여기서는 빈을 말한다) 중 적당한 빈에게 
애당 요청을 처리하도록 한다. 

![image](https://github.com/user-attachments/assets/670b2741-e0e2-4d54-863a-94121fc7fedc)


> 우리는 스프링 컨테이너만 생각해서 개발하고 동작하고 싶지만 
> 간단한 스프링 웹을 띄울려고 해도 자바의 서블릿 컨테이너를 알아야 띄울 수 있다. 
> 서블릿 컨테이너는 생각보다 간단하지 않다( 설정하는 방법 등등..)

* 서블릿 컨테이너는 web.xml과 같이 많은 설정과 설치 등 고려해야할 사항들이 많다. 
* 오타가 나거나 설정이 안맞으면 시간도 많이 들고 폼도 많이 들게 된다. 
* 이러한 컨테이너에 대해서 몰라도 알아서 해결해주는 것을, 이러한 수고들을 제거해줬으면 좋겠다라 컨테이너 리스를 의미한다. 


실제로 컨테이너 리스를 적용 하면 아래 이미지와 같다

![image](https://github.com/user-attachments/assets/8351439a-d17e-4a36-9660-1cf44fc18f48)

서블릿 컨테이너에 대해서는 실제로 존재하지 않은 것은 아니지만 신경 쓰지 않고 스프링 컨테이너만을 보고 개발할 수 있도록 해준 것이다. 



> 우리는 스프링 컨테이너만 생각해서 개발하고 동작하고 싶지만 
> 간단한 스프링 웹을 띄울려고 해도 자바의 서블릿 컨테이너를 알아야 띄울 수 있다. 
> 서블릿 컨테이너는 생각보다 간단하지 않다( 설정하는 방법 등등..)

* 서블릿 컨테이너는 web.xml과 같이 많은 설정과 설치 등 고려해야할 사항들이 많다. 
* 오타가 나거나 설정이 안맞으면 시간도 많이 들고 폼도 많이 들게 된다. 
* 이러한 컨테이너에 대해서 몰라도 알아서 해결해주는 것을, 이러한 수고들을 제거해줬으면 좋겠다라 컨테이너 리스를 의미한다. 


실제로 컨테이너 리스를 적용 하면 아래 이미지와 같다

#Opinionated 
*스프링 부트가 자기의 의견을 가지고있다 라는 의미다.* 
>개발을 위한 고민만 하고 그 이외는 알아서 해주겠다라는 의미가 강하다.

##스프링 프레임워크의 설계 철학 
- 극단적으로 유연하다. 
> 이전 EJB와 달리 유용하게 모든거를 포용할 수 있다라는 의미이다. 
- 다양한 관점을 수용한다. 
> java뿐만 아니라 다른 상용 라이브러리도 모든걸 수용하겠다라는 의미. 
- Not opinionateed 
> 위를 보면 알 수 있듯이 모든거를 다 포용하니 강제하지 않고 많은 선택지를 제공하겠다라는 의미. 

> 하지만 다양한 선택지는 초기 프로젝트 개발 시 많은 고민들을 해야 하는 시간이 필요로 하다. 
  예를 들면 어느 기술을 사용해야 하고 그 기술은 어느 버전을 사용해야 하는지 이런것들.. 
  
##스프링 부트의 설계 철악 
-Opinionated - 자기 주장이 강하고 독선적이다. 
> 즉 스프링부트가 주장하는 것을 따라야 한다라는 의미. 
- 정해준 대로 개발하면 빠르게 개발할 수 있다. 그뒤 세부설정은 나중에 한다. 

## 사용 기술과 의존 라이브러리 결정 
> 그렇다면 스프링부트가 결정해주는 것은 무엇이 있을까? 
> 어떤 기술을 사용하하고, 어떤 라이브러리, 어떤 버전을 사용할지 정해준다는 것이다. *

- 업계에서 검증된 스프링 생태계 프로젝트, 표준 사바 기술, 오픈소스 기술의 종류와 의존관계 
  사용 버전을 정해줌. 
- 각 기술을 스프링에 적용하는 방식(DI 구성)과 디폴트 설정값 제공 

## 유연한 확장 
> 스프링 부트는 모든것을 지정해줘서 개발할 때는 빠르지만 실제 개발이 완료 되고 나면은 
> 커스터마이징이 들어가야할 수간이 생긴다. 다른 프로그램들은 강제로 지정된 부분을 수정할 수 없기도 하고, 
> 수정일 하면 이전에 가지고 있던 장점이 없어지는 그런 경우가 생긴다. 
> 하지만 스프링부트는 유연하게 커스텀을 할 수있도록 해준다. 

- 스프링 부트에 내장된 디폴트 구성을 커스터마이징 하는 매우 자연스럽고 유연한 방법제공 
- 스프링 부트가 스프링을 사용하는 방식 이해 한다면 스프링 부트를 제거하고 원하는 방식으로 재구성 가능
- 스프링 부트 처럼 기술과 구성을 간편하게 제공하는 나만의 모듈을 작성할 수 있다. 

#프로젝트 생성 

##Spring Initializr 
- API로 이루어져있으면 유저가 호출하면 API가 그에 대응하는 서비스로 스프링부트 기반의 프로젝트를 
  다운 받을 수 있다. 
  
>2.x 버전의 스프링 부트를 사용하지만 실제로 start.spring.io에서 생성하려 하니 
>최신 기준만 존재 한다. 이전 버전의 스프링을 설치하고 싶다면 아래의 링크대로 실행하자. 
>https://shanepark.tistory.com/492

- start.spring.io를 통해서 초기 프로젝트를 생성할 수 있다. 


생성 후 잘 생성됐는지 확인 차원에서 GET 방식의 API Controller를 생성한다. 
파일이름은 HelloController로 한다. 

```java
package tobyspring.helloboot;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

    @GetMapping("/hello")
    public String hello(String name) {
        return "Hello" + name;
    }
}
```

- GET 방식의 API다 
- path는 /hello이고 파라미터로 name을 가진다. 
- 호출 시 /hello?name=xxx 이렇게 호출이 가능하다. 


#Hello API 테스트 

API로 테스트 하는 방법은 여러가지 방법이 있다. 

- 웹 브라우저 개발자 도구 
- curl 
- HTTPie
- intellij IDEA Ultimate-http request 
- Postman API Plaform 
- JUnit Test 
- 각종 API 테스트 도구 

#HTTP요청과 응답
![image](https://github.com/user-attachments/assets/a4ed8cef-4bd5-4506-945a-88e929d42882)
web client와  web container간의 통신을 어떻게 결정하는거가 
프로토콜이고 그 프로토콜 중 하나가 HTTP 이다

##HTTP 
>HTTP는 공부하기 위해서는 방대한 양의 정보를 습득해야 한다. 
>하지만 그 많은 양을 공부하기에는 너무 비효율적이다. 그래서 웹개발에서 정말 필요한 부분만 
>정리한것이다. 

웹 Request와 Response의 기본 구조를 이해하고 내용을 확인할 수 있어야 한다. 

*헤더
- http 첫줄에는 어떤 메소드를 이용하겠다라는 정보가 나온다 
  예를들면 post, delete, get 이런것을 말한다. 
  
- 그 뒤에는 host와 포트를 제외한 나머지 경로가 나온다. 
- 마지막으로는 http 버전이 붙어서 나온다.   


응답
- http 버전이 앞에 나온다. 
- 그리고 상태 코드 값이 나온다. 200,400 이런것들 
![image](https://github.com/user-attachments/assets/69e9667f-176d-426d-af05-919eeba2599f)


#Containerless 개발 준비 
- 서블릿 컨테이너에 작업에대 관련된것들은 신경쓰지 않는다. 
- Spring Container에 대한 신경만 쓰도록 한다. 
- 이런것들을 스프링 부트에서 해주는 것이다. 

예를 들면 web.xml, 서블릿 컨테이너 설치 이런것 없이 간단한 방법으러 서버를 띄우고 싶은것이다. 


기존에 만들었던 HelloController를 보면 
```java
package tobyspring.helloboot;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

    @GetMapping("/hello")
    public String hello(String name) {
        return "Hello" + name;
    }
}

```

return 타입에 따라 HTTP에 타입이 결정 되어진다. 
여기서는 String 타입으로 리턴이 되어서 실제로 http로 리스폰을 던질때  
해당 타입에 맞게 스프링이 던져 준다. 


HellobootApplication를 보게 되면 
@SpringBootApplication과 
main메소드 안에 SpringApplcation.run이라는 함수를 통해  
스프링이 톰캣을 띄우고 웹페이지에 접속이 되게끔 한다. 

이런것 없이 일단은 스프링부트의 도움없이 띄워보는 작업을 할것이다. 
그러기에앞서 HellobootApplication에서 어노테이션과 메소드를 다 지울것이다. 
아래처럼 
```java
package tobyspring.helloboot;


public class HellobootApplication {

	public static void main(String[] args) {
		System.out.println("Hello Containerless Standalone Application");
	}

}

```


#서블릿 컨테이너 띄우기 

이런 서블릿은 자바의 표준 기술이고 이 표준 기술을 구현한 컨테이너 제품들이 많이 나와있다. 
그 중 대중적인것이 톰캣이다. 

톰캣을 메인메소드를 이용해서 띄울 것이다. 
톰캣도 자바로 만들어진 제품이다. 

톰캣은 설치를 통해 사용하는 것도 있지만 
build in 처럼 내장해서 사용하는하는 내장형 톰캣이 존재한다. 
그것을 임베디드 톰캣이라고 부른다. 

initailizer를 통해 스프링은 만들 때 이미 임베디드 톰캣은 들어가 있다. 

원래는 Tomcat이라는 클래스를 사용해서 톰캣을 띄울 수는 있지만 이 안에는 무수한 정보들이있고 
이 정보들을 이용해서 많은 설정을을 다뤄야 한다. 하지만 스프링 부트에서는 이런 과정을 도와주는 것이 있다. 
그것이 TomcatServletWebServerFactory 클래스다. 

```java
public static void main(String[] args) {
	TomcatServletWebServerFactory serverFactory = new TomcatServletWebServerFactory();
	WebServer webServer = serverFactory.getWebServer();// 서블릿 컨테이너를 만드는 생성 함수를 의미한다. 
	
}
```

이것은 WebServer라는 클래스로 받을 수 있다. 톰캣 말고도 다른 웹서버들이 존재하기에 추상화를 통해 클래스명이 WebServer인것이다. 


```java
public static void main(String[] args) {
	ServletWebServerFactory serverFactory = new TomcatServletWebServerFactory();
	WebServer webServer = serverFactory.getWebServer();// 서블릿 컨테이너를 만드는 생성 함수를 의미한다.
	webServer.start();
	
}
```
위에 처처럼 ServletWebServerFatory라는 클래스로도 받을 수 있다. 
그리고 webServer.start()라는 함수를 실행해서 톰캣 서블릿 테이너가 동작을 한다. 


#서블릿 등록 

```java
public static void main(String[] args) {
	ServletWebServerFactory serverFactory = new TomcatServletWebServerFactory();
	WebServer webServer = serverFactory.getWebServer(servletContext ->{
		servletContext.addServlet("hello", new HttpServlet(){
			@Override
			protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
				resp.setStatus(200);
				resp.setHeader("Content-Type", "text/plain");
				resp.getWriter().println("Hello Servlet");
			}
		}).addMapping("/hello");
	});
	webServer.start();

}
```
![image](https://github.com/user-attachments/assets/9cf02527-45f5-4634-8aa7-525ed35c365d)

- getWebServer 함수는파라미터로  ServletContextInitializer형식의 파람을 받을 수 있다. 
   ServletContextInitializer는 서블릿 컨테이너에다가 서블릿을 등록하는데 필요한 작업을 수행하는 오브젝트를 만들때 
   쓴다 
-  ServletContextInitializer는 인터페이스여서 여기서는 익명 클래스로 만든다. 
   ServletContextInitializer는 메소드가 하나인 인터페이스이고 이것은 람다식으로 대체가 가능하다. 
- 람다식에는 메소드가 하나이므로 여기서는 void onStartup(ServletContext servletContext)이다. 
  servletContext이것을 받아서 구현한 것이라고 생각하면 된다. 
- 두번째 인자로 HeepServlet을 받는다. 이것은 공통적인 부분을 구현해 놓고 이걸 상속해서 쓰도록 하는 어뎁터 클래스이다. 
  그 상속받은 클래스에서 필요한 부분만 오버라이딩해서 사용하면 된다. 
- 여기서 실제 Servlet 기능을 구현한것은 service이다. 
- 이 서블릿은 어떻게 요청 받아 처리할지는 addMapping("/hello")를 통해 처리 한다 즉 url이 /hello이면 여기서 
  HttpServlet에서의  service가 처리해서 응답을 리턴해준다고 생각하면 된다. 
- 그 응답 처리로 resp 변수에 있는 응답코드, 헤더, body 부분을 처리해서 리턴해준다. 

#서블릿 요청 처리 
```java
public static void main(String[] args) {
	ServletWebServerFactory serverFactory = new TomcatServletWebServerFactory();
	WebServer webServer = serverFactory.getWebServer(servletContext ->{
		servletContext.addServlet("hello", new HttpServlet(){
			@Override
			protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
				resp.setStatus(HttpStatus.OK.value());
				resp.setHeader(HttpHeaders.CONTENT_TYPE, MediaType.TEXT_PLAIN_VALUE);
				resp.getWriter().println("Hello Servlet");
			}
		}).addMapping("/hello");
	});
	webServer.start();

}

}
```
- resp.setHeader에 있는 2개의 인자는 오타가 날 상황이 많기 때문에 enum으로 값을 세팅할 수 있다.  
  이걸을 권장한다. 
  
```java
public static void main(String[] args) {
	ServletWebServerFactory serverFactory = new TomcatServletWebServerFactory();
	WebServer webServer = serverFactory.getWebServer(servletContext ->{
		servletContext.addServlet("hello", new HttpServlet(){
			@Override
			protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
				String name = req.getParameter("name");

				resp.setStatus(HttpStatus.OK.value());
				resp.setHeader(HttpHeaders.CONTENT_TYPE, MediaType.TEXT_PLAIN_VALUE);
				resp.getWriter().println("Hello " + name);
			}
		}).addMapping("/hello");
	});
	webServer.start();

}
```  
- req.getParameter를 사용해서 GET방식의 바라미터를 받아서 처리할 수 있다. 


#프론트 컨트롤러 

이전에는 앞에서 소개했던 것처럼 서블릿에서 어느 url을 통해서 처리하고 리턴하는지에 대해서 
모든 프로젝트 전반에 걸쳐서 소스 코딩을 해야 했다. 
이런 코드는 중복된 코드가 생길 수밖에 없었다. 

그래서 이런 중복된 코드를 없앨 수 없을까가 pain point였다. 

모든 요청을 각각의 서블릿이 받아서 처리하는게 아닌 공통적으로 받는 부분을 프론트 컨트롤러가 받아서 
이거를 실제 로직을 처리하는 것은 다른 오브젝트에 넘겨주는 방식을 하길 원했다. 
이러한 방식으로 프론트 프레임워크를 내장한 웹프레임워크들이 등장하기 시작했다. 

프론트 컨트롤러가 공통적으로 처리해주는 작업 
- 인증, 보안, 다국어 처리 
- 모든 요청에 대해서 공통적으로 리턴해줘야 하는 내용이 있는 것 


#프론트 컨트롤러로 전환 
```java
public static void main(String[] args) {
	ServletWebServerFactory serverFactory = new TomcatServletWebServerFactory();
	WebServer webServer = serverFactory.getWebServer(servletContext ->{
		servletContext.addServlet("frotcontroller", new HttpServlet(){
			@Override
			protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
				String name = req.getParameter("name");

				resp.setStatus(HttpStatus.OK.value());
				resp.setHeader(HttpHeaders.CONTENT_TYPE, MediaType.TEXT_PLAIN_VALUE);
				resp.getWriter().println("Hello " + name);
			}
		}).addMapping("/*");
	});
	webServer.start();

}
```

이전 소스를 프론트 컨트롤러로 전환하는 방법에 대해 알아보자 

일단 서블릿 이름은 frontcontroller로 변경했고 
모든 요청에 대해 이 서블릿이 처리를 해야 하니 addMapping에서 /*으로 url 패턴을 변경했다. 


```java
protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
				//인증, 보완, 다국어, 공통기능 처리
				if (req.getRequestURI().equals("/hello") && req.getMethod().equals(HttpMethod.GET.name())) {
					String name = req.getParameter("name");

					resp.setStatus(HttpStatus.OK.value());
					resp.setHeader(HttpHeaders.CONTENT_TYPE, MediaType.TEXT_PLAIN_VALUE);
					resp.getWriter().println("Hello " + name);
				} else if (req.getRequestURI().equals("/user")) {
					//
				} else {
					resp.setStatus(HttpStatus.NOT_FOUND.value());
				}
			}
```
- 이러헥 모든 거를 처리하는 로직이 인증, 보완, 다국어 이렇게 처리하고 나서 각각 처리해야 할 부분은 
  url의 경로를 이용해서 각기 다르게 처리하도록하면된다. 
- 만약 경로에 매핑 되는 것이 없다면은 404 에러를 발생하면 된다. 
- 위의 코드는 한 소스 안에 표현했지만 각각 처리해야 하는 부분은 다른 파일로 뺄 수가 있다. 
- req.getMethod를 통해 GET 방식의 메소드만 받아 처리할 수도있다. 


#Hello 컨트롤러 매핑과 바인딩 
```java
public class HelloController {

    public String hello(String name) {
        return "Hello" + name;
    }
}
```

- 스프링이 없었을 때 각각 서블릿이 처리하는 파일을 만든다는 가정할 해야 하므로 이전에 만들었던 HelloController에서 
  어노테이션 관련 부분을 모두 제거했다. 
  
  
  
```java
HelloController helloController = new HelloController();
```  
HellobootApplication.java에서  싱글톤 형식 마냥 인스턴스를 만들어서 처리한다. 


```java
protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
	//인증, 보완, 다국어, 공통기능 처리
	if (req.getRequestURI().equals("/hello") && req.getMethod().equals(HttpMethod.GET.name())) {
		String name = req.getParameter("name");

		String ret = helloController.hello(name);

		resp.setStatus(HttpStatus.OK.value());
		resp.setHeader(HttpHeaders.CONTENT_TYPE, MediaType.TEXT_PLAIN_VALUE);
		resp.getWriter().println(ret);
	} else if (req.getRequestURI().equals("/user")) {
		//
	} else {
		resp.setStatus(HttpStatus.NOT_FOUND.value());
	}
}
```

- helloController에서 hello함수를 이용해 처리한 데이터를(ret) 다시 리턴해주는 기능을 구현했다. 

#스프링 컨테이너 사용 

기존에는 프론트 컨트롤러가 모든것을 처리하고 그 뒤로 오브젝트인 Hello Controller에게 책임을 위임해주는 방식이었다면 
이번에는 Spring Container 안에 집어 넣는걸로 해보겠다. 

컨테이너는 여러개의 오브젝트를 가지고있다가 필요할 때 이 오브젝트가 사용되어지도록 관리해주는 것이다. 

스프링의 컨테이너가 동작하기 위해서는 2가지가 필요 하다. 
1.우리의 비즈니스를 담고 있는 비즈니스 오브젝트 
  즉 우리가 개발한 옵젝트를 말한다 
  
2.위의 것을 어떤식으로 구성할지에 대한 구성 정보를 담고 있는 Configuration Metadata 정보 

이 두가지를 조합해서 사용 가능한 시스템으로 만들어 내는 것이다. 

 
```java
protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
	//인증, 보완, 다국어, 공통기능 처리
	if (req.getRequestURI().equals("/hello") && req.getMethod().equals(HttpMethod.GET.name())) {
		String name = req.getParameter("name");

		String ret = helloController.hello(name);

		resp.setContentType(MediaType.TEXT_PLAIN_VALUE);
		resp.getWriter().println(ret);
	}
	else {
		resp.setStatus(HttpStatus.NOT_FOUND.value());
	}
}
```
- 다른 경로의 것은 안쓸거기 때문에 /user 관련 소스코드는 줄였다. 
- setHeader 대신 setContentType을 사용해서 인자로 하나만 받도록 수정했다. 
- 또한 프론트 컨트롤러에서 직접 빈을 생성할 것이 아니기 때문에 HelloController 인스턴스를 제거했다. 


그 후에 스프링 컨테이너를 만들어 보자 
스프링 컨테이너를 대표하는 인터페이스 이름이 있다. ApplicationContext라는 것이다. 
이것을 구현한 것 중에 대표적인게 GenericApplicationContext이다. 

```java
GenericApplicationContext applicationContext = new GenericApplicationContext();
```

- 서블릿 컨테이너에서는 책임을 건가할 오브젝트를 new 생성자로 생성해서 addServlet으로 서블릿을 추가해줬다면 
- 스프링에서는 오브젝트를 생성하는것이 아닌 어떤 클래스를 이용해서 Bean 오브젝트를 생성할것인가에 대한 메타 정보를 넣어주는 
  방식으로 구성을 한다. 
  
- 그렇게 정보를 구성해주는건 registerBean이라는 함수를 통해 만들 수 있으며 
- 인자는 Bean에 대항하는 클래스 정보가 해당된다.
```java
GenericApplicationContext applicationContext = new GenericApplicationContext();
applicationContext.registerBean(HelloController.class);
```

- 위의 소스 코드를 가지고 스프링은 Bean을 만들것이다. 
- applicationContext.refresh();를 하면 다시 Bean을 만들어주는 기능을 할것이다. 

```java
HelloController helloController = applicationContext.getBean(HelloController.class);
	String ret = helloController.hello(name);
```
- 기존에 helloController는 오브젝트를 생성해서 가져왔다면 이제는 스프링이 Bean을 만들어서 거기에서 Bean을 가져와 쓰게끔 해준다. 

아래는 모든 코드가 적용된 모습이다. 
```java
public static void main(String[] args) {
	GenericApplicationContext applicationContext = new GenericApplicationContext();
	applicationContext.registerBean(HelloController.class);
	applicationContext.refresh();

	ServletWebServerFactory serverFactory = new TomcatServletWebServerFactory();
	WebServer webServer = serverFactory.getWebServer(servletContext ->{
		servletContext.addServlet("frotcontroller", new HttpServlet(){
			@Override
			protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
				//인증, 보완, 다국어, 공통기능 처리
				if (req.getRequestURI().equals("/hello") && req.getMethod().equals(HttpMethod.GET.name())) {
					String name = req.getParameter("name");

					HelloController helloController = applicationContext.getBean(HelloController.class);
					String ret = helloController.hello(name);

					resp.setContentType(MediaType.TEXT_PLAIN_VALUE);
					resp.getWriter().println(ret);
				}
				else {
					resp.setStatus(HttpStatus.NOT_FOUND.value());
				}
			}
		}).addMapping("/*");
	});
	webServer.start();

}
```

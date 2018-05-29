---


---

<h2 id="junit-5-의-아키텍쳐">JUnit 5 의 아키텍쳐</h2>
<blockquote>
<p>작성자 : Kakao Corp 비즈개발실 &gt; 비즈플랫폼팀 &gt; 톡비즈 서버 파트 eDell.LEE(이남희)</p>
</blockquote>
<p>Java Ecosystem 내에서 가장 인기있는 단위 테스트 프레임워크 로써 아래의 3개의 서브 프로젝트로 구성 되어 있다.</p>
<ul>
<li>JUnit Platform</li>
<li>JUnit Jupiter</li>
<li>JUnit Vintage</li>
</ul>
<p>Platform은  JVM 위에서 테스트 프레임워크를 가동시킨다.<br>
Jupiter는 테스트 코드 작성을 위한 어노테이션이 포함 되어 있다.<br>
마지막으로 Vintage 는 하위 모듈 (JUnit3, JUnit4) 테스트 실행을 지원한다.</p>
<blockquote>
<p>테스트 실행 환경 구성<br>
JDK 1.8 이상<br>
JUnit 5 이상<br>
IntelliJ 2018</p>
</blockquote>
<img src="https://www.safaribooksonline.com/library/view/building-web-apps/9781787284661/assets/b71cb504-5ebd-4e7e-b793-8b676200121a.png" width="800px">
<p>즉, JUnit4 에서 작성한 코드는 Vintage 엔진에 의해 Platform을 통해서 구동되며, Jupiter API 호출하는 테스트는 Jupiter 엔진을 통해 Platform 의 TestEngine을 통해 테스트 케이스를 실행하게 된다.</p>
<blockquote>
<p>참고<br>
JUnit 5 사용자 가이드  <a href="https://junit.org/junit5/docs/current/user-guide/">JUnit5</a>.<br>
Git Repository <a href="https://github.com/junit-team/junit5/">https://github.com/junit-team/junit5</a></p>
</blockquote>
<p>현재 (2018.05) GA 버전은 5.2.0 이다</p>
<p>Gradle 설정은 아래와 같다.</p>
<pre class=" language-bash"><code class="prism  language-bash">dependencies <span class="token punctuation">{</span>  
    testCompile<span class="token punctuation">(</span><span class="token string">'org.junit.jupiter:junit-jupiter-api:5.2.0'</span><span class="token punctuation">)</span>  
    testRuntime<span class="token punctuation">(</span><span class="token string">'org.junit.jupiter:junit-jupiter-engine:5.2.0'</span><span class="token punctuation">)</span>  
<span class="token punctuation">}</span>
</code></pre>
<h3 id="annotation">Annotation</h3>
<p><code>Jupiter</code> 에서 지원하는 테스트 구성 어노테이션은 아래와 같다.<br>
<code>Annotation Discription</code></p>

<table>
<thead>
<tr>
<th>Annotation</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>@Test</strong></td>
<td>테스트 메소드임을 선언</td>
</tr>
<tr>
<td><strong>@ParameterizedTest</strong></td>
<td>매개 변수를 통해 여러 인수를 테스함</td>
</tr>
<tr>
<td><strong>@RepeatedTest</strong></td>
<td>메소드 반복 테스트</td>
</tr>
<tr>
<td><strong>@TestFactory</strong></td>
<td>메소드가 런타임에 생성되는 동적 테스트를위한 테스트 팩토리</td>
</tr>
<tr>
<td><strong>@TestInstance</strong></td>
<td>해당 어노테이션이 달린 테스트 클래스에 대한 테스트 인스턴스 수명주기를 구성</td>
</tr>
<tr>
<td><strong>@TestTemplate</strong></td>
<td>TestTemplateInvocationContextProvider 에 의해 복수 호출되는 테스트 케이스의 템플릿</td>
</tr>
<tr>
<td><strong>@DisplayName</strong></td>
<td>테스트 클래스 또는 테스트 메서드에 대한 사용자 지정 표시 이름을 선언하여 표기</td>
</tr>
<tr>
<td><strong>@BeforeEach</strong></td>
<td>각 @Test, @RepeatedTest, @ParameterizedTest 또는 @TestFactory 메소드보다 먼저 실행되는 어노테이션 (akka @Before in junit4)</td>
</tr>
<tr>
<td><strong>@AfterEach</strong></td>
<td>각 @Test, @RepeatedTest, @ParameterizedTest 또는 @TestFactory 메소드 다음에 실행되는 어노테이션 (@After 와 비슷)</td>
</tr>
<tr>
<td><strong>@BeforeAll</strong></td>
<td>해당 메소드는 현재 클래스의 모든 @Test, @RepeatedTest, @ParameterizedTest 및 @TestFactory 메소드보다 먼저 실행되어야 함 (@BeforeClass 와 유사)</td>
</tr>
<tr>
<td><strong>@AfterAll</strong></td>
<td>해당 메소드는 현재 클래스의 모든 @Test, @RepeatedTest, @ParameterizedTest 및 @TestFactory 메소드 다음에 실행되어야 함 (@AfterClass)</td>
</tr>
<tr>
<td><strong>@Nested</strong></td>
<td>중첩 된 비 정적 테스트 클래스임</td>
</tr>
<tr>
<td><strong>@Tag</strong></td>
<td>클래스 또는 메서드 수준에서 필터링 테스트 용 태그를 선언하는 데 사용</td>
</tr>
<tr>
<td><strong>@Disabled</strong></td>
<td>테스트 케이스 비활성화 (@Ignore)</td>
</tr>
<tr>
<td><strong>@ExtendWith</strong></td>
<td>사용자 지정 확장을 등록</td>
</tr>
</tbody>
</table><blockquote>
<p>@Test, @TestTemplate, @RepeatedTest, @BeforeAll, @AfterAll, @BeforeEach 또는 @AfterEach 어노테이션 메소드는 값을 반환하면 안됌.</p>
</blockquote>
<p>실제 자주 사용되는 코드들을 통해 샘플을 아래와 같이 작성하여 실행해본다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">package</span> com<span class="token punctuation">.</span>libqa<span class="token punctuation">.</span>junit<span class="token punctuation">;</span>  
  
<span class="token keyword">import</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>AfterAll<span class="token punctuation">;</span>  
<span class="token keyword">import</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>AfterEach<span class="token punctuation">;</span>  
<span class="token keyword">import</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>BeforeAll<span class="token punctuation">;</span>  
<span class="token keyword">import</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>BeforeEach<span class="token punctuation">;</span>  
<span class="token keyword">import</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Disabled<span class="token punctuation">;</span>  
<span class="token keyword">import</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Test<span class="token punctuation">;</span>  
  
<span class="token keyword">import</span> <span class="token keyword">static</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Assertions<span class="token punctuation">.</span>fail<span class="token punctuation">;</span>  
  
<span class="token keyword">class</span> <span class="token class-name">StandardTests</span> <span class="token punctuation">{</span>  
  
  <span class="token annotation punctuation">@BeforeAll</span>  
  <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">initAll</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"@BeforeAll"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
  <span class="token punctuation">}</span>  
  
  <span class="token annotation punctuation">@BeforeEach</span>  
  <span class="token keyword">void</span> <span class="token function">init</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"@BeforeEach"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
  <span class="token punctuation">}</span>  
  
  <span class="token annotation punctuation">@Test</span>  
  <span class="token keyword">void</span> <span class="token function">succeedingTest1</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"Success Test first!!"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
  <span class="token punctuation">}</span>  
  
  <span class="token annotation punctuation">@Test</span>  
  <span class="token keyword">void</span> <span class="token function">succeedingTest2</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"Success Test second!!"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
  <span class="token punctuation">}</span>  
  
  <span class="token annotation punctuation">@Test</span>  
  <span class="token keyword">void</span> <span class="token function">failingTest</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        <span class="token function">fail</span><span class="token punctuation">(</span><span class="token string">"a failing test"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
  <span class="token punctuation">}</span>  
  
  <span class="token annotation punctuation">@Test</span>  
  <span class="token annotation punctuation">@Disabled</span><span class="token punctuation">(</span><span class="token string">"skip this "</span><span class="token punctuation">)</span>  
  <span class="token keyword">void</span> <span class="token function">skippedTest</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"## Disabled for demonstration purposes"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
  <span class="token punctuation">}</span>  
  
  <span class="token annotation punctuation">@AfterEach</span>  
  <span class="token keyword">void</span> <span class="token function">tearDown</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"@AfterEach"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
  <span class="token punctuation">}</span>  
  
  <span class="token annotation punctuation">@AfterAll</span>  
  <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">tearDownAll</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"@AfterAll"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
  <span class="token punctuation">}</span> 
<span class="token punctuation">}</span>
</code></pre>
<p><code>Annotation Discription</code>  에 나온데로, 위 코드를 실행하면 최초 한번과 최종 한번은 @BeforeAll 어노테이션과 @AfterAll이 실행되는 것을 알 수 있다. 또한 이 두 어노테이션은 static 으로 선언 되어야 한다.</p>
<p>succeedingTest1 메소드나 succeedingTest2 각 실행 이전 이후로 @BeforeEach  와 @AfterEach 가 각각 실행된 것을 확인할 수 있다.<br>
실패하는 테스트(failingTest)의 경우 역시 @BeforeEach  와 @AfterEach 가 실행 되었다.<br>
@Disabled 의 경우 skip this 라는 메서드만 실행될 뿐 @BeforeEach  와 @AfterEach 실행되지는 않는다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token annotation punctuation">@DisplayName</span><span class="token punctuation">(</span><span class="token string">"succeedingTest1 was passed"</span><span class="token punctuation">)</span>  
<span class="token annotation punctuation">@Test</span>  
<span class="token keyword">void</span> <span class="token function">succeedingTest1</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
    System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"Success Test first!!"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
<span class="token punctuation">}</span>
</code></pre>
<p>@DisplayName 어노테이션의 경우 JUnit run 실행시 노출되는 명을 지정하 수 있는 어노테이션이다.</p>
<img src="https://lh3.googleusercontent.com/tiWURxG4YHvRu4utiF-ikssci13jNySzMsWRTdcpTZ_zNjrzZ5oN_bee-gAfT8J9yzP4HL4qLMyjcg" width="800px">
<h3 id="exception">Exception</h3>
<p>JUnit 5 에서는 주어진 유형의 Exception을 던지는지 확인하는 assertThrows () 메소드가 추가 되었다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token annotation punctuation">@Test</span>  
<span class="token annotation punctuation">@DisplayName</span><span class="token punctuation">(</span><span class="token string">"Throw 한 익셉션의 메시지를 비교한다."</span><span class="token punctuation">)</span>  
<span class="token keyword">void</span> <span class="token function">shouldThrowException</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
    Throwable exception <span class="token operator">=</span> <span class="token function">assertThrows</span><span class="token punctuation">(</span>UnsupportedOperationException<span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">,</span> <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token punctuation">{</span>  
        <span class="token keyword">throw</span> <span class="token keyword">new</span> <span class="token class-name">UnsupportedOperationException</span><span class="token punctuation">(</span><span class="token string">"Not supported"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
  <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
  <span class="token function">assertEquals</span><span class="token punctuation">(</span>exception<span class="token punctuation">.</span><span class="token function">getMessage</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token string">"Not supported"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
<span class="token punctuation">}</span>
</code></pre>
<p>실행해보면 정상적으로 테스트를 통과하는 것을 확인할 수 있다.</p>
<img src="https://lh3.googleusercontent.com/wxFa3gABqg2OamJBVfCYIyBQJ7BwgUvn36I_a6NuJMJr8aS3mWKN-gzLjnBJF0rCpDxE382aiFh3cg" width="800px">
<h3 id="tagging">Tagging</h3>
<p>테스트 클래스와 메소드는 @Tag 주석을 통해 태크 마킹을 할 수 있으며 나중에 테스트 검색 및 실행을 필터링하는 데 사용할 수 있다. 이는 계획된 테스트만을 추가하거나, 테스트 실행 계획에서 제외하는 테스트 집합을 만들어 낼 수 있다.</p>
<p><code>tagging</code> package를 만들어서 아래와 같은 테스트 케이스를 작성한다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">package</span> com<span class="token punctuation">.</span>libqa<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>tagging<span class="token punctuation">;</span>  
  
<span class="token keyword">import</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Tag<span class="token punctuation">;</span>  
<span class="token keyword">import</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Test<span class="token punctuation">;</span>  
  
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">TagTests</span> <span class="token punctuation">{</span>  
  
    <span class="token annotation punctuation">@Test</span>  
    <span class="token annotation punctuation">@Tag</span><span class="token punctuation">(</span><span class="token string">"development"</span><span class="token punctuation">)</span>  
    <span class="token annotation punctuation">@Tag</span><span class="token punctuation">(</span><span class="token string">"production"</span><span class="token punctuation">)</span>  
    <span class="token keyword">void</span> <span class="token function">allTestCase</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"Development and Production Test !"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
    <span class="token punctuation">}</span>  
  
    <span class="token annotation punctuation">@Test</span>  
    <span class="token annotation punctuation">@Tag</span><span class="token punctuation">(</span><span class="token string">"development"</span><span class="token punctuation">)</span>  
    <span class="token keyword">void</span> <span class="token function">developmentTest</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"Only evelopment Test !"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
    <span class="token punctuation">}</span>   
<span class="token punctuation">}</span>
</code></pre>
<p>development 라는 태그와 production 이라는 태그를 구분해서 메소드에 적용하였다.</p>
<p>build.gradle 에  platform-runner 를 디펜던시에 추가해준다.</p>
<pre class=" language-java"><code class="prism  language-java">apply plugin<span class="token operator">:</span> <span class="token string">'java'</span>  
  
group <span class="token string">'JUnit5'</span>  
version <span class="token string">'1.0-SNAPSHOT'</span>  
  
sourceCompatibility <span class="token operator">=</span> <span class="token number">1.8</span>  
  
repositories <span class="token punctuation">{</span>  
    <span class="token function">mavenCentral</span><span class="token punctuation">(</span><span class="token punctuation">)</span>  
<span class="token punctuation">}</span>  
  
dependencies <span class="token punctuation">{</span>  
    <span class="token function">testCompile</span><span class="token punctuation">(</span><span class="token string">'org.junit.jupiter:junit-jupiter-api:5.2.0'</span><span class="token punctuation">)</span>  
    <span class="token function">testRuntime</span><span class="token punctuation">(</span><span class="token string">'org.junit.jupiter:junit-jupiter-engine:5.2.0'</span><span class="token punctuation">)</span>  
    <span class="token function">testCompile</span><span class="token punctuation">(</span><span class="token string">'org.junit.platform:junit-platform-runner:1.2.0'</span><span class="token punctuation">)</span>  
<span class="token punctuation">}</span>
</code></pre>
<p>IncludeTags를 통해 Production 태그만 호출해본다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">package</span> com<span class="token punctuation">.</span>libqa<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>tagging<span class="token punctuation">;</span>  
  
<span class="token keyword">import</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>Test<span class="token punctuation">;</span>  
<span class="token keyword">import</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>platform<span class="token punctuation">.</span>runner<span class="token punctuation">.</span>JUnitPlatform<span class="token punctuation">;</span>  
<span class="token keyword">import</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>platform<span class="token punctuation">.</span>suite<span class="token punctuation">.</span>api<span class="token punctuation">.</span>IncludeTags<span class="token punctuation">;</span>  
<span class="token keyword">import</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>platform<span class="token punctuation">.</span>suite<span class="token punctuation">.</span>api<span class="token punctuation">.</span>SelectPackages<span class="token punctuation">;</span>  
<span class="token keyword">import</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>runner<span class="token punctuation">.</span>RunWith<span class="token punctuation">;</span>  
  
<span class="token annotation punctuation">@RunWith</span><span class="token punctuation">(</span>JUnitPlatform<span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">)</span>  
<span class="token annotation punctuation">@SelectPackages</span><span class="token punctuation">(</span><span class="token string">"com.libqa.junit.tagging"</span><span class="token punctuation">)</span>  
<span class="token annotation punctuation">@IncludeTags</span><span class="token punctuation">(</span><span class="token string">"production"</span><span class="token punctuation">)</span>  
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">IncludeTagTest</span> <span class="token punctuation">{</span>  
    <span class="token annotation punctuation">@Test</span>  
    <span class="token keyword">void</span> <span class="token function">includeProductionTest</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">" 프로젝션 코드가 호출되어야 함"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
    <span class="token punctuation">}</span>  
<span class="token punctuation">}</span>
</code></pre>
<p>TagTests 클래스의 <code>Development and Production Test !</code> 만 호출되는 것을 확인할 수 있다.</p>
<blockquote>
<p>물론 IncludeTags(“development”) 로 할 경우 development 태그가 적용된 두개의 메소드 모두 호출되는     것을 확인할 수 있으며 <strong><code>@ExcludeTags("production")</code></strong> 혹은 <strong><code>@IncludeTags({"production","development"})</code></strong> 와 같은 형태로도 사용할 수 있다.</p>
</blockquote>
<h3 id="assertions">Assertions</h3>
<p>JUnit5 의 단정문  (assertions) 은 테스트 케이스의 실제 출력 값을 예상 출력값으로 비교하여 유효성을 확인하는 정적 클래스이다.</p>
<blockquote>
<p>관련 API는 <a href="https://junit.org/junit5/docs/5.0.1/api/org/junit/jupiter/api/Assertions.html">https://junit.org/junit5/docs/5.0.1/api/org/junit/jupiter/api/Assertions.html</a> 를 참고한다.</p>
</blockquote>
<p><code>assertEquals</code> , <code>assertNotEquals</code>, <code>assertArrayEquals</code>, <code>assertTrue</code>, <code>assertFalse</code> 등의 구문을 통해 호출된 결과값과 기대값을 비교하는데 사용한다.</p>
<h4 id="assertequals">assertEquals()</h4>
<p>기대값과 실제값이 같은지를 비교하는 Assertions.asserEquals() 구문은 아래와 같이 쓰인다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertEquals</span><span class="token punctuation">(</span><span class="token keyword">int</span> expected<span class="token punctuation">,</span> <span class="token keyword">int</span> actual<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertEquals</span><span class="token punctuation">(</span><span class="token keyword">int</span> expected<span class="token punctuation">,</span> <span class="token keyword">int</span> actual<span class="token punctuation">,</span> String message<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertEquals</span><span class="token punctuation">(</span><span class="token keyword">int</span> expected<span class="token punctuation">,</span> <span class="token keyword">int</span> actual<span class="token punctuation">,</span> Supplier<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> messageSupplier<span class="token punctuation">)</span>
</code></pre>
<p>간단한 계산 어플리케이션을 작성해보며 assertEquals를 사용해보자.</p>
<p>com.libqa.junit.assertion 패키지에 CalculatorTest 를 작성한다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">package</span> com<span class="token punctuation">.</span>libqa<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>assertion<span class="token punctuation">;</span>  
<span class="token keyword">import</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Test<span class="token punctuation">;</span>  
<span class="token keyword">import</span> <span class="token keyword">static</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Assertions<span class="token punctuation">.</span>assertEquals<span class="token punctuation">;</span>  
  
<span class="token keyword">class</span> <span class="token class-name">CalculatorTest</span> <span class="token punctuation">{</span>  
  
    <span class="token annotation punctuation">@Test</span>  
    <span class="token keyword">void</span> <span class="token function">addTest</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        <span class="token keyword">long</span> addResult <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Calculator</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
        <span class="token comment">//Test will pass  </span>
        <span class="token function">assertEquals</span><span class="token punctuation">(</span>4L<span class="token punctuation">,</span> addResult<span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span>  
<span class="token punctuation">}</span>
</code></pre>
<p>최초 실행시  Calculator 클래스에 add 메소드가 존재하지 않기 때문에 에러가 발생할 것이다.<br>
add 메소드를 작성한다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">package</span> com<span class="token punctuation">.</span>libqa<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>assertion<span class="token punctuation">;</span>  
  
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">Calculator</span> <span class="token punctuation">{</span>  
  
    <span class="token keyword">public</span> <span class="token keyword">long</span> <span class="token function">add</span><span class="token punctuation">(</span><span class="token keyword">long</span> first<span class="token punctuation">,</span> <span class="token keyword">long</span> second<span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        <span class="token keyword">return</span> first <span class="token operator">+</span> second<span class="token punctuation">;</span>  
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<p>넘어온 파라미터를 더하여 리턴하는 간단한 메소드로, assertEquals를 통해 타입이나 리턴값을 검증할 수 있다.<br>
다시 테스트케이스를 실행하면 정상적으로 녹색 라인이 출력되는 것을 확인 할 수 있다.</p>
<p>이제 결과값이 다른 실패 케이스를 작성해보자. 이는, 다른 형태의 메소드 시그니처를 테스트 해보기 위해서 인데, 위의 Assertions.asserEquals() 구문 유형중 두번째와 세번째의 경우를 테스트 해보기 위함이다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">package</span> com<span class="token punctuation">.</span>libqa<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>assertion<span class="token punctuation">;</span>  
  
<span class="token keyword">import</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Test<span class="token punctuation">;</span>  
<span class="token keyword">import</span> java<span class="token punctuation">.</span>util<span class="token punctuation">.</span>function<span class="token punctuation">.</span>Supplier<span class="token punctuation">;</span>  
<span class="token keyword">import</span> <span class="token keyword">static</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Assertions<span class="token punctuation">.</span>assertEquals<span class="token punctuation">;</span>  
  
<span class="token keyword">class</span> <span class="token class-name">CalculatorTest</span> <span class="token punctuation">{</span>  
  
    <span class="token annotation punctuation">@Test</span>  
    <span class="token keyword">void</span> <span class="token function">addTest</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        <span class="token keyword">long</span> addResult <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Calculator</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
        <span class="token comment">//Test will pass  </span>
        <span class="token function">assertEquals</span><span class="token punctuation">(</span>4L<span class="token punctuation">,</span> addResult<span class="token punctuation">)</span><span class="token punctuation">;</span>  
    <span class="token punctuation">}</span>    
  
    <span class="token annotation punctuation">@Test</span>  
    <span class="token keyword">void</span> <span class="token function">addFailValueTest</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        <span class="token keyword">long</span> addResult <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Calculator</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
        <span class="token comment">//Test will fail  </span>
        <span class="token function">assertEquals</span><span class="token punctuation">(</span>5L<span class="token punctuation">,</span> addResult<span class="token punctuation">,</span> <span class="token string">"Calculator.add(2, 2) == 5 Is False!!!"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
    <span class="token punctuation">}</span>  
  
    <span class="token annotation punctuation">@Test</span>  
    <span class="token keyword">void</span> <span class="token function">addFailSupplierTest</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        <span class="token keyword">long</span> addResult <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Calculator</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
        <span class="token comment">//Test will fail  </span>
        Supplier<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> messageSupplier  <span class="token operator">=</span> <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token string">"Calculator.add(2, 2) == 3 test failed"</span><span class="token punctuation">;</span>  
        <span class="token function">assertEquals</span><span class="token punctuation">(</span>3L<span class="token punctuation">,</span> addResult <span class="token punctuation">,</span> messageSupplier<span class="token punctuation">)</span><span class="token punctuation">;</span>  
    <span class="token punctuation">}</span>  
<span class="token punctuation">}</span>
</code></pre>
<p>두번째 메소드인 addFailValueTest 의 경우 assertEquals 를 통해 검증에 실패할 경우 3번째 인자값인 message 가 출력된다.<br>
세번째의 경우도 마찬가지인데, 매개 변수가 있는 좀 더 다양한 방식의 오류 메시지를 작성할 때 쓰인다.</p>
<h4 id="assertnotequals">assertNotEquals()</h4>
<p>마찬가지로 Assertions.assertNotEquals() 의 경우 예상값과 실제값이 동일하지 않다고 단정할 경우 사용된다.</p>
<p>구문은 아래와 같다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertNotEquals</span><span class="token punctuation">(</span>Object expected<span class="token punctuation">,</span> Object actual<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertNotEquals</span><span class="token punctuation">(</span>Object expected<span class="token punctuation">,</span> Object actual<span class="token punctuation">,</span> String message<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertNotEquals</span><span class="token punctuation">(</span>Object expected<span class="token punctuation">,</span> Object actual<span class="token punctuation">,</span> Supplier<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> messageSupplier<span class="token punctuation">)</span>
</code></pre>
<p>Calculator 클래스에 아래와 같이 코드를 완성한 후 테스트를 진행해보자.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">package</span> com<span class="token punctuation">.</span>libqa<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>assertion<span class="token punctuation">;</span>  
  
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">Calculator</span> <span class="token punctuation">{</span>  
  
    <span class="token keyword">public</span> <span class="token keyword">long</span> <span class="token function">add</span><span class="token punctuation">(</span><span class="token keyword">long</span> first<span class="token punctuation">,</span> <span class="token keyword">long</span> second<span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        <span class="token keyword">return</span> first <span class="token operator">+</span> second<span class="token punctuation">;</span>  
  <span class="token punctuation">}</span>  
  
    <span class="token keyword">public</span> <span class="token keyword">long</span> <span class="token function">subtract</span><span class="token punctuation">(</span><span class="token keyword">long</span> first<span class="token punctuation">,</span> <span class="token keyword">long</span> second<span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        <span class="token keyword">return</span> first <span class="token operator">-</span> second<span class="token punctuation">;</span>  
  <span class="token punctuation">}</span>  
  
    <span class="token keyword">public</span> <span class="token keyword">long</span> <span class="token function">multiply</span><span class="token punctuation">(</span><span class="token keyword">long</span> first<span class="token punctuation">,</span> <span class="token keyword">long</span> second<span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        <span class="token keyword">return</span> first <span class="token operator">*</span> second<span class="token punctuation">;</span>  
  <span class="token punctuation">}</span>  
  
    <span class="token keyword">public</span> <span class="token keyword">long</span> <span class="token function">divide</span><span class="token punctuation">(</span><span class="token keyword">long</span> first<span class="token punctuation">,</span> <span class="token keyword">long</span> second<span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        <span class="token keyword">return</span> first <span class="token operator">/</span> second<span class="token punctuation">;</span>  
  <span class="token punctuation">}</span>  
<span class="token punctuation">}</span>
</code></pre>
<p>add, subtract, multiply 의 테스트 케이스를 작성한다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">package</span> com<span class="token punctuation">.</span>libqa<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>assertion<span class="token punctuation">;</span>  
  
<span class="token keyword">import</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>DisplayName<span class="token punctuation">;</span>  
<span class="token keyword">import</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Test<span class="token punctuation">;</span>  
  
<span class="token keyword">import</span> <span class="token keyword">static</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Assertions<span class="token punctuation">.</span>assertNotEquals<span class="token punctuation">;</span>  
  
<span class="token keyword">class</span> <span class="token class-name">CalculatorNotEqualsTest</span> <span class="token punctuation">{</span>  
  
    <span class="token annotation punctuation">@Test</span>  
    <span class="token keyword">void</span> <span class="token function">addTestNotEqualsGiven3</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        <span class="token comment">//Test will pass  </span>
	    Long addResult <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Calculator</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">add</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
	    <span class="token function">assertNotEquals</span><span class="token punctuation">(</span>3L<span class="token punctuation">,</span> addResult<span class="token punctuation">)</span><span class="token punctuation">;</span>  
    <span class="token punctuation">}</span>  
  
  
    <span class="token annotation punctuation">@Test</span>  
    <span class="token annotation punctuation">@DisplayName</span><span class="token punctuation">(</span><span class="token string">"4가 주어졌을 때 subtract 결과 값이 같지 않은지 검사한다. "</span><span class="token punctuation">)</span>  
    <span class="token keyword">void</span> <span class="token function">addTestNotEqualsSubtractGiven4</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        Long addResult <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Calculator</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">subtract</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
	    <span class="token comment">//Test will fail  </span>
	    <span class="token function">assertNotEquals</span><span class="token punctuation">(</span>0L<span class="token punctuation">,</span> addResult<span class="token punctuation">,</span> <span class="token string">"addTestNotEqualsSubtractGiven4 test failed"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
  <span class="token punctuation">}</span>  
  
    <span class="token annotation punctuation">@Test</span>  
	<span class="token annotation punctuation">@DisplayName</span><span class="token punctuation">(</span><span class="token string">"Supplier multiply gove x * y Fail "</span><span class="token punctuation">)</span>  
    <span class="token keyword">void</span> <span class="token function">addTestNotEqualsSupplierGiven4</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        <span class="token keyword">int</span> x <span class="token operator">=</span> <span class="token number">3</span><span class="token punctuation">;</span>  
		<span class="token keyword">int</span> y <span class="token operator">=</span> <span class="token number">5</span><span class="token punctuation">;</span>  
		Long expected <span class="token operator">=</span> 15L<span class="token punctuation">;</span>  
	    Long addResult <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Calculator</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">multiply</span><span class="token punctuation">(</span>x<span class="token punctuation">,</span> y<span class="token punctuation">)</span><span class="token punctuation">;</span>  
	    <span class="token function">assertNotEquals</span><span class="token punctuation">(</span>expected<span class="token punctuation">,</span> addResult<span class="token punctuation">,</span>  
						  <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> String<span class="token punctuation">.</span><span class="token function">format</span><span class="token punctuation">(</span><span class="token string">"%s * %s != %s"</span><span class="token punctuation">,</span> x<span class="token punctuation">,</span> y<span class="token punctuation">,</span> expected<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
    <span class="token punctuation">}</span>  
<span class="token punctuation">}</span>
</code></pre>
<p><code>addTestNotEqualsGiven3</code> 테스트는 기대값과 같지 않기 때문에 정상적으로 통과 하지만 나머지 두개의 테스트는 기대값과 같기 때문에 assertNotEquals 테스트를 통과 하지 못한다.</p>
<p><code>addTestNotEqualsSubtractGiven4 의 에러 메시지</code><br>
<img src="https://lh3.googleusercontent.com/KTH_WiaRQC2UTLPaRcYszCSykuocLXMq8qYWCne-YBEOQWzOy0v5V4WW1Xs8Dh0B50HyIFetMCrXpA" width="800px"></p>
<p><code>addTestNotEqualsSupplierGiven4 의 에러 메시지</code><br>
<img src="https://lh3.googleusercontent.com/A1LV2K9-G03xeR9rFywhaYsPwlZS07xN9PW9RZcK7zseFInDR3OUR5yc3EqgOk9fECtLFzke0Ak0UQ" width="800px"></p>
<h4 id="assertarrayequals">assertArrayEquals()</h4>
<p>Array 의 경우 assertArrayEquals() 로 실제값의 어레이 값을 단정할 수 있다. 마찬가지로 테스트 통과 실패시 출력할 메시지를 지원한다.<br>
구문은 아래와 같다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertArrayEquals</span><span class="token punctuation">(</span><span class="token keyword">int</span><span class="token punctuation">[</span><span class="token punctuation">]</span> expected<span class="token punctuation">,</span> <span class="token keyword">int</span><span class="token punctuation">[</span><span class="token punctuation">]</span> actual<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertArrayEquals</span><span class="token punctuation">(</span><span class="token keyword">int</span><span class="token punctuation">[</span><span class="token punctuation">]</span> expected<span class="token punctuation">,</span> <span class="token keyword">int</span><span class="token punctuation">[</span><span class="token punctuation">]</span> actual<span class="token punctuation">,</span> String message<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertArrayEquals</span><span class="token punctuation">(</span><span class="token keyword">int</span><span class="token punctuation">[</span><span class="token punctuation">]</span> expected<span class="token punctuation">,</span> <span class="token keyword">int</span><span class="token punctuation">[</span><span class="token punctuation">]</span> actual<span class="token punctuation">,</span> Supplier<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> messageSupplier<span class="token punctuation">)</span>
</code></pre>
<p>예제를 살펴보자.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">package</span> com<span class="token punctuation">.</span>libqa<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>assertion<span class="token punctuation">;</span>  
  
<span class="token keyword">import</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Test<span class="token punctuation">;</span>   
<span class="token keyword">import</span> <span class="token keyword">static</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Assertions<span class="token punctuation">.</span>assertArrayEquals<span class="token punctuation">;</span>  
  
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">AssertArrayEqualsTest</span> <span class="token punctuation">{</span>  
  
    <span class="token annotation punctuation">@Test</span>  
    <span class="token keyword">void</span> <span class="token function">assertArraysTest</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        <span class="token keyword">int</span><span class="token punctuation">[</span><span class="token punctuation">]</span> one <span class="token operator">=</span> <span class="token punctuation">{</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">}</span><span class="token punctuation">;</span>  
        <span class="token keyword">int</span><span class="token punctuation">[</span><span class="token punctuation">]</span> two <span class="token operator">=</span> <span class="token punctuation">{</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">}</span><span class="token punctuation">;</span>  
        <span class="token function">assertArrayEquals</span><span class="token punctuation">(</span>one<span class="token punctuation">,</span> two<span class="token punctuation">,</span> <span class="token string">"ArrayEquals Test"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
    <span class="token punctuation">}</span>  
  
    <span class="token annotation punctuation">@Test</span>  
    <span class="token keyword">void</span> <span class="token function">assertArraysWrongTest</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        <span class="token keyword">int</span><span class="token punctuation">[</span><span class="token punctuation">]</span> one <span class="token operator">=</span> <span class="token punctuation">{</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">}</span><span class="token punctuation">;</span>  
		<span class="token keyword">int</span><span class="token punctuation">[</span><span class="token punctuation">]</span> two <span class="token operator">=</span> <span class="token punctuation">{</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">,</span> <span class="token number">4</span><span class="token punctuation">}</span><span class="token punctuation">;</span>  
	    <span class="token function">assertArrayEquals</span><span class="token punctuation">(</span>one<span class="token punctuation">,</span> two<span class="token punctuation">,</span> <span class="token string">"ArrayEquals assertArraysWrongTest Test"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
    <span class="token punctuation">}</span>  
<span class="token punctuation">}</span>
</code></pre>
<h4 id="assertiterableequals">assertIterableEquals()</h4>
<p>assertIterableEquals() 는 예상과 실제 iterable 의 요소 수와 순서가 동일함을 테스트 한다.<br>
구문은 아래와 같다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertIterableEquals</span><span class="token punctuation">(</span>Iterable<span class="token operator">&lt;</span><span class="token operator">?</span><span class="token operator">&gt;</span> expected<span class="token punctuation">,</span> Iterable<span class="token operator">&gt;</span> actual<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertIterableEquals</span><span class="token punctuation">(</span>Iterable<span class="token operator">&lt;</span><span class="token operator">?</span><span class="token operator">&gt;</span> expected<span class="token punctuation">,</span> Iterable<span class="token operator">&gt;</span> actual<span class="token punctuation">,</span> String message<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertIterableEquals</span><span class="token punctuation">(</span>Iterable<span class="token operator">&lt;</span><span class="token operator">?</span><span class="token operator">&gt;</span> expected<span class="token punctuation">,</span> Iterable<span class="token operator">&gt;</span> actual<span class="token punctuation">,</span> Supplier<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> messageSupplier<span class="token punctuation">)</span>
</code></pre>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">package</span> com<span class="token punctuation">.</span>libqa<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>assertion<span class="token punctuation">;</span>  
  
<span class="token keyword">import</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Test<span class="token punctuation">;</span>  
<span class="token keyword">import</span> java<span class="token punctuation">.</span>util<span class="token punctuation">.</span>ArrayList<span class="token punctuation">;</span>  
<span class="token keyword">import</span> java<span class="token punctuation">.</span>util<span class="token punctuation">.</span>Arrays<span class="token punctuation">;</span>   
<span class="token keyword">import</span> <span class="token keyword">static</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Assertions<span class="token punctuation">.</span>assertIterableEquals<span class="token punctuation">;</span>  
  
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">AssertIterableEquals</span> <span class="token punctuation">{</span>  
  
    <span class="token annotation punctuation">@Test</span>  
    <span class="token keyword">void</span> <span class="token function">assertIterableEqualsTest</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        Iterable<span class="token operator">&lt;</span>Integer<span class="token operator">&gt;</span> listOne <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">ArrayList</span><span class="token operator">&lt;</span><span class="token operator">&gt;</span><span class="token punctuation">(</span>Arrays<span class="token punctuation">.</span><span class="token function">asList</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">,</span><span class="token number">2</span><span class="token punctuation">,</span><span class="token number">3</span><span class="token punctuation">,</span><span class="token number">4</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
	    Iterable<span class="token operator">&lt;</span>Integer<span class="token operator">&gt;</span> listTwo <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">ArrayList</span><span class="token operator">&lt;</span><span class="token operator">&gt;</span><span class="token punctuation">(</span>Arrays<span class="token punctuation">.</span><span class="token function">asList</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">,</span><span class="token number">2</span><span class="token punctuation">,</span><span class="token number">3</span><span class="token punctuation">,</span><span class="token number">4</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
	    Iterable<span class="token operator">&lt;</span>Integer<span class="token operator">&gt;</span> listThree <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">ArrayList</span><span class="token operator">&lt;</span><span class="token operator">&gt;</span><span class="token punctuation">(</span>Arrays<span class="token punctuation">.</span><span class="token function">asList</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">,</span><span class="token number">2</span><span class="token punctuation">,</span><span class="token number">3</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
  
	    <span class="token function">assertIterableEquals</span><span class="token punctuation">(</span>listOne<span class="token punctuation">,</span> listTwo<span class="token punctuation">)</span><span class="token punctuation">;</span>  
	    <span class="token comment">//assertIterableEquals(listOne, listThree, "Iterable List not matched");  </span>
    <span class="token punctuation">}</span> 
<span class="token punctuation">}</span>
</code></pre>
<h4 id="assertnotnull--assertnull">assertNotNull &amp; assertNull</h4>
<p>assertNotNull()은 actual가 null이 아니라고 단정한다.<br>
마찬가지로 assertNull() 메소드는 actual가 null이라는 것을 나타낸다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertNotNull</span><span class="token punctuation">(</span>Object actual<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertNotNull</span><span class="token punctuation">(</span>Object actual<span class="token punctuation">,</span> String message<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertNotNull</span><span class="token punctuation">(</span>Object actual<span class="token punctuation">,</span> Supplier<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> messageSupplier<span class="token punctuation">)</span>

<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertNull</span><span class="token punctuation">(</span>Object actual<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertNull</span><span class="token punctuation">(</span>Object actual<span class="token punctuation">,</span> String message<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertNull</span><span class="token punctuation">(</span>Object actual<span class="token punctuation">,</span> Supplier<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> messageSupplier<span class="token punctuation">)</span>
</code></pre>
<h4 id="assertnotsame--assertsane">assertNotSame &amp;&amp; assertSane</h4>
<p>assertNotSame()은 예상과 실제가 동일한 객체를 참조하지 않는다고 단정한다.<br>
마찬가지로 assertSame() 메소드는 예상과 실제가 동일한 객체를 참조한다고 단정한다. 구문은 아래와 같다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertNotSame</span><span class="token punctuation">(</span>Object actual<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertNotSame</span><span class="token punctuation">(</span>Object actual<span class="token punctuation">,</span> String message<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertNotSame</span><span class="token punctuation">(</span>Object actual<span class="token punctuation">,</span> Supplier<span class="token operator">&lt;</span><span class="token operator">&gt;</span> messageSupplier<span class="token punctuation">)</span>

<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertSame</span><span class="token punctuation">(</span>Object actual<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertSame</span><span class="token punctuation">(</span>Object actual<span class="token punctuation">,</span> String message<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertSame</span><span class="token punctuation">(</span>Object actual<span class="token punctuation">,</span> Supplier<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> messageSupplier<span class="token punctuation">)</span>
</code></pre>
<h4 id="asserttrue--assertfalse">assertTrue &amp; assertFalse</h4>
<p>assertTrue() 는 제공된 조건이 true이거나 BooleanSupplier가 제공하는 조건이 true임을 단정한다.<br>
마찬가지로 assertFalse() 는 제공된 조건이 거짓임을 나타낸다.  구문은 아래와 같다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertTrue</span><span class="token punctuation">(</span><span class="token keyword">boolean</span> condition<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertTrue</span><span class="token punctuation">(</span><span class="token keyword">boolean</span> condition<span class="token punctuation">,</span> String message<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertTrue</span><span class="token punctuation">(</span><span class="token keyword">boolean</span> condition<span class="token punctuation">,</span> Supplier<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> messageSupplier<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertTrue</span><span class="token punctuation">(</span>BooleanSupplier booleanSupplier<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertTrue</span><span class="token punctuation">(</span>BooleanSupplier booleanSupplier<span class="token punctuation">,</span> String message<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertTrue</span><span class="token punctuation">(</span>BooleanSupplier booleanSupplier<span class="token punctuation">,</span> Supplier<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> messageSupplier<span class="token punctuation">)</span>

<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertFalse</span><span class="token punctuation">(</span><span class="token keyword">boolean</span> condition<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertFalse</span><span class="token punctuation">(</span><span class="token keyword">boolean</span> condition<span class="token punctuation">,</span> String message<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertFalse</span><span class="token punctuation">(</span><span class="token keyword">boolean</span> condition<span class="token punctuation">,</span> Supplier<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> messageSupplier<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertFalse</span><span class="token punctuation">(</span>BooleanSupplier booleanSupplier<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertFalse</span><span class="token punctuation">(</span>BooleanSupplier booleanSupplier<span class="token punctuation">,</span> String message<span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assertFalse</span><span class="token punctuation">(</span>BooleanSupplier booleanSupplier<span class="token punctuation">,</span> Supplier<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> messageSupplier<span class="token punctuation">)</span>
</code></pre>
<p>예제 코드는 아래와 같다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">package</span> com<span class="token punctuation">.</span>libqa<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>assertion<span class="token punctuation">;</span>  
  
<span class="token keyword">import</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Test<span class="token punctuation">;</span>  
<span class="token keyword">import</span> <span class="token keyword">static</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Assertions<span class="token punctuation">.</span>assertFalse<span class="token punctuation">;</span>  
<span class="token keyword">import</span> <span class="token keyword">static</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Assertions<span class="token punctuation">.</span>assertTrue<span class="token punctuation">;</span>  
  
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">AssertTrueTest</span> <span class="token punctuation">{</span>  
  
    <span class="token keyword">private</span> <span class="token keyword">static</span> String <span class="token function">getMessage</span> <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        <span class="token keyword">return</span> <span class="token string">"Test result is False"</span><span class="token punctuation">;</span>  
    <span class="token punctuation">}</span>  
  
    <span class="token keyword">private</span> <span class="token keyword">static</span> <span class="token keyword">boolean</span> <span class="token function">getResult</span> <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        <span class="token keyword">return</span> <span class="token boolean">true</span><span class="token punctuation">;</span>  
    <span class="token punctuation">}</span>   
  
    <span class="token annotation punctuation">@Test</span>  
    <span class="token keyword">void</span> <span class="token function">assertTrueTest</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        <span class="token function">assertTrue</span><span class="token punctuation">(</span>AssertTrueTest<span class="token operator">:</span><span class="token operator">:</span>getResult<span class="token punctuation">,</span> AssertTrueTest<span class="token operator">:</span><span class="token operator">:</span>getMessage<span class="token punctuation">)</span><span class="token punctuation">;</span>  
    <span class="token punctuation">}</span>  
  
    <span class="token annotation punctuation">@Test</span>  
    <span class="token keyword">void</span> <span class="token function">assertFalseTest</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        <span class="token function">assertFalse</span><span class="token punctuation">(</span>AssertTrueTest<span class="token operator">:</span><span class="token operator">:</span>getResult<span class="token punctuation">,</span> AssertTrueTest<span class="token operator">:</span><span class="token operator">:</span>getMessage<span class="token punctuation">)</span><span class="token punctuation">;</span>  
    <span class="token punctuation">}</span>  
<span class="token punctuation">}</span>
</code></pre>
<h4 id="assertthrows">assertThrows</h4>
<p>테스트중인 어플리케이션에서 던져진 예외에 대한 단정은 assertThrows() 메소드를 통해 확인이 가능하다.<br>
assertThrows() 메소드는 다음의 매개변수들을 사용한다.</p>
<ul>
<li>예상되는 예외의 형태를 지정하는 클래스 객체</li>
<li>테스트중인 어플리케이션을 호출하는 Executable 객체</li>
<li>선택적 오류 메시지</li>
</ul>
<p>기본적인 구문은 아래와 같다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token function">assertThrows</span><span class="token punctuation">(</span>Class<span class="token operator">&lt;</span>T<span class="token operator">&gt;</span> expectedType<span class="token punctuation">,</span> Executable executable<span class="token punctuation">)</span>
<span class="token function">assertThrows</span><span class="token punctuation">(</span>Class<span class="token operator">&lt;</span>T<span class="token operator">&gt;</span> expectedType<span class="token punctuation">,</span> Executable executable<span class="token punctuation">,</span> String message<span class="token punctuation">)</span>
<span class="token function">assertThrows</span><span class="token punctuation">(</span>Class<span class="token operator">&lt;</span>T<span class="token operator">&gt;</span> expectedType<span class="token punctuation">,</span> Executable executable<span class="token punctuation">,</span> Supplier<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> messageSupplier<span class="token punctuation">)</span>	
</code></pre>
<p>NullPointer Exception을 던지는 테스트 케이스를 가졍하고 assertThrows를 사용항면 아래와 같다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">package</span> com<span class="token punctuation">.</span>libqa<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>assertion<span class="token punctuation">;</span>  
  
<span class="token keyword">import</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>DisplayName<span class="token punctuation">;</span>  
<span class="token keyword">import</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Test<span class="token punctuation">;</span>  
<span class="token keyword">import</span> <span class="token keyword">static</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Assertions<span class="token punctuation">.</span>assertThrows<span class="token punctuation">;</span>  
<span class="token keyword">import</span> <span class="token keyword">static</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Assertions<span class="token punctuation">.</span>assertEquals<span class="token punctuation">;</span>

<span class="token annotation punctuation">@DisplayName</span><span class="token punctuation">(</span><span class="token string">"Writing assertions for exceptions"</span><span class="token punctuation">)</span>  
<span class="token keyword">class</span> <span class="token class-name">ExceptionAssertionTest</span> <span class="token punctuation">{</span>  
   
    <span class="token annotation punctuation">@Test</span>  
	<span class="token annotation punctuation">@DisplayName</span><span class="token punctuation">(</span><span class="token string">"Should throw the NullPointerException"</span><span class="token punctuation">)</span>  
    <span class="token keyword">void</span> <span class="token function">shouldThrowCorrectException</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        <span class="token function">assertThrows</span><span class="token punctuation">(</span>  
                NullPointerException<span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">,</span>  
			    <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token punctuation">{</span> <span class="token keyword">throw</span> <span class="token keyword">new</span> <span class="token class-name">NullPointerException</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token punctuation">}</span>  
        <span class="token punctuation">)</span><span class="token punctuation">;</span>  
    <span class="token punctuation">}</span>  
    
    <span class="token annotation punctuation">@Test</span>  
	<span class="token annotation punctuation">@DisplayName</span><span class="token punctuation">(</span><span class="token string">"Should throw an exception that has the correct message"</span><span class="token punctuation">)</span>  
	<span class="token keyword">void</span> <span class="token function">shouldThrowAnExceptionWithCorrectMessage</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
	    <span class="token keyword">final</span> NullPointerException thrown <span class="token operator">=</span> <span class="token function">assertThrows</span><span class="token punctuation">(</span>  
	            NullPointerException<span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">,</span>  
			    <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token punctuation">{</span> <span class="token keyword">throw</span> <span class="token keyword">new</span> <span class="token class-name">NullPointerException</span><span class="token punctuation">(</span><span class="token string">"Hello World!"</span><span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token punctuation">}</span>  
	    <span class="token punctuation">)</span><span class="token punctuation">;</span>  
	    <span class="token function">assertEquals</span><span class="token punctuation">(</span><span class="token string">"Hello World!"</span><span class="token punctuation">,</span> thrown<span class="token punctuation">.</span><span class="token function">getMessage</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<p>발생 된 예외에 올바른 메시지가 있는지 확인하려면 shouldThrowAnExceptionWithCorrectMessage() 과 같이 작성할 수 있다.</p>
<h3 id="assumptions">Assumptions</h3>
<p>Assumptions 클래스는 가정을 기반으로 조건부 테스트 실행을 지원하는 정적 메서드를 제공한다. 실패할 경우 테스트가 중단된다.</p>
<blockquote>
<p>관련 API는 <a href="https://junit.org/junit5/docs/current/api/org/junit/jupiter/api/Assumptions.html">https://junit.org/junit5/docs/current/api/org/junit/jupiter/api/Assumptions.html</a> 를 참고한다.</p>
</blockquote>
<h4 id="assumtrue">assumTrue</h4>
<p>assumTrue() 는 주어진 가정을 true로 가정하고 가정이 true이면 테스트가 진행되고, 그렇지 않으면 테스트 실행을 중단한다.</p>
<p>기본적인 구문은 아래와 같다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assumeTrue</span><span class="token punctuation">(</span><span class="token keyword">boolean</span> assumption<span class="token punctuation">)</span> <span class="token keyword">throws</span> TestAbortedException
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assumeTrue</span><span class="token punctuation">(</span><span class="token keyword">boolean</span> assumption<span class="token punctuation">,</span> Supplier<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> messageSupplier<span class="token punctuation">)</span> <span class="token keyword">throws</span> TestAbortedException
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assumeTrue</span><span class="token punctuation">(</span><span class="token keyword">boolean</span> assumption<span class="token punctuation">,</span> String message<span class="token punctuation">)</span> <span class="token keyword">throws</span> TestAbortedException

<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assumeTrue</span><span class="token punctuation">(</span>BooleanSupplier assumptionSupplier<span class="token punctuation">)</span> <span class="token keyword">throws</span> TestAbortedException
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assumeTrue</span><span class="token punctuation">(</span>BooleanSupplier assumptionSupplier<span class="token punctuation">,</span> String message<span class="token punctuation">)</span> <span class="token keyword">throws</span> TestAbortedException
<span class="token keyword">public</span> <span class="token keyword">static</span> <span class="token keyword">void</span> <span class="token function">assumeTrue</span><span class="token punctuation">(</span>BooleanSupplier assumptionSupplier<span class="token punctuation">,</span> Supplier<span class="token operator">&lt;</span>String<span class="token operator">&gt;</span> messageSupplier<span class="token punctuation">)</span> <span class="token keyword">throws</span> TestAbortedException
</code></pre>
<p>예제를 살펴보자.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">package</span> com<span class="token punctuation">.</span>libqa<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>assumption<span class="token punctuation">;</span>  
  
<span class="token keyword">import</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Test<span class="token punctuation">;</span>  
<span class="token keyword">import</span> <span class="token keyword">static</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Assertions<span class="token punctuation">.</span>assertEquals<span class="token punctuation">;</span>  
<span class="token keyword">import</span> <span class="token keyword">static</span> org<span class="token punctuation">.</span>junit<span class="token punctuation">.</span>jupiter<span class="token punctuation">.</span>api<span class="token punctuation">.</span>Assumptions<span class="token punctuation">.</span>assumeTrue<span class="token punctuation">;</span>  
  
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">AssumeTrue</span> <span class="token punctuation">{</span>  
  
    <span class="token keyword">private</span> <span class="token keyword">static</span> String <span class="token function">message</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        <span class="token keyword">return</span> <span class="token string">"TEST Execution Failed  "</span><span class="token punctuation">;</span>  
    <span class="token punctuation">}</span>  
  
  
    <span class="token annotation punctuation">@Test</span>  
    <span class="token keyword">void</span> <span class="token function">systemIsDevelopTest</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        System<span class="token punctuation">.</span><span class="token function">setProperty</span><span class="token punctuation">(</span><span class="token string">"ENV"</span><span class="token punctuation">,</span> <span class="token string">"DEV"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
	    <span class="token function">assumeTrue</span><span class="token punctuation">(</span><span class="token string">"DEV"</span><span class="token punctuation">.</span><span class="token function">equals</span><span class="token punctuation">(</span>System<span class="token punctuation">.</span><span class="token function">getProperty</span><span class="token punctuation">(</span><span class="token string">"ENV"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
  
	    <span class="token comment">//remainder of test will proceed  </span>
	    <span class="token function">assertEquals</span><span class="token punctuation">(</span>System<span class="token punctuation">.</span><span class="token function">getProperty</span><span class="token punctuation">(</span><span class="token string">"ENV"</span><span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token string">"PROD"</span><span class="token punctuation">,</span> <span class="token string">"프로덕션 환경이 아닙니다."</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
    <span class="token punctuation">}</span>  
  
    <span class="token annotation punctuation">@Test</span>  
    <span class="token keyword">void</span> <span class="token function">systemIsProductionTest</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>  
        System<span class="token punctuation">.</span><span class="token function">setProperty</span><span class="token punctuation">(</span><span class="token string">"ENV"</span><span class="token punctuation">,</span> <span class="token string">"PROD"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
	    <span class="token function">assumeTrue</span><span class="token punctuation">(</span><span class="token string">"DEV"</span><span class="token punctuation">.</span><span class="token function">equals</span><span class="token punctuation">(</span>System<span class="token punctuation">.</span><span class="token function">getProperty</span><span class="token punctuation">(</span><span class="token string">"ENV"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">,</span> AssumeTrue<span class="token operator">:</span><span class="token operator">:</span>message<span class="token punctuation">)</span><span class="token punctuation">;</span>  
  
	    <span class="token comment">//remainder of test will be aborted  </span>
	    <span class="token function">assertEquals</span><span class="token punctuation">(</span>System<span class="token punctuation">.</span><span class="token function">getProperty</span><span class="token punctuation">(</span><span class="token string">"ENV"</span><span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token string">"DEV"</span><span class="token punctuation">,</span> <span class="token string">"개발 환경이 아닙니다."</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
  <span class="token punctuation">}</span>  
<span class="token punctuation">}</span>
</code></pre>
<p>systemIsDevelopTest() 메소드의 경우 assumTrue 에 의해 결과가 true가 되고 다음 테스트 구문이 실행이 되는 것을 확인 할 수 있으나 systemIsProductionTest() 의 경우 assumTrue 이후 결과가 false 임에 따라 다음 테스트 구문은 실행이 되지 않는것을 확인할 수 있다.</p>
<h3 id="selectclasses에-의한-test-suite-만들기">SelectClasses에 의한 Test Suite 만들기</h3>
<p>Single class일 경우 아래와 같이 @SelectClasses 어노테이션에 하나의 클래스를 파라미터로 전달함으로써 테스트 할 수 있다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token annotation punctuation">@RunWith</span><span class="token punctuation">(</span>JUnitPlatform<span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">)</span>
<span class="token annotation punctuation">@SelectClasses</span><span class="token punctuation">(</span> ClassATest<span class="token punctuation">.</span><span class="token keyword">class</span> <span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">JUnit5TestSuiteExample</span> <span class="token punctuation">{</span>
	<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span> 
<span class="token punctuation">}</span>
</code></pre>
<p>여러 클래스를 지정해야 할 경우 Array 형태의  <code>{ a.class , b.class, ...}</code> 를  @SelectClasses 어노테이션에 전달함으로써 테스트를 할 수 있다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token annotation punctuation">@RunWith</span><span class="token punctuation">(</span>JUnitPlatform<span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">)</span>
<span class="token annotation punctuation">@SelectClasses</span><span class="token punctuation">(</span> <span class="token punctuation">{</span> ClassATest<span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">,</span> ClassBTest<span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">,</span> ClassCTest<span class="token punctuation">.</span><span class="token keyword">class</span> <span class="token punctuation">}</span> <span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">JUnit5TestSuiteExample</span> <span class="token punctuation">{</span>
	<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token punctuation">}</span>
</code></pre>
<p>특정 하위 패키지를 제외하거나 패키지를 포함 시키려면 @IncludePackages 및 @ExcludePackages Annotation을 활용하여 @SelectPackages 하위에 추가하거나 제외할 수 있다. (@IncludeTags 와 @ExcludeTags 도 사용 가능함)</p>
<p>이와 같이 다양한 형태의 Test Suite 를 작성할 수 있으며 필터링을 통해 복합적인 테스트가 가능해졌다.</p>


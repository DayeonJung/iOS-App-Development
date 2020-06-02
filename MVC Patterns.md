---


---

<h1 id="mvc-patterns">MVC Patterns</h1>
<p><strong>M</strong>odel - 알고리즘, 데이터, 데이터베이스, 실행하게 될 함수들<br>
<strong>V</strong>iew - controller의 미니언<br>
<strong>C</strong>ontroller - Model과 View의 매개체. 사용자의 입력을 받는 곳</p>
<h2 id="controller---model">Controller -&gt; Model</h2>
<p>항상 가능. 사용자에게 모델에 있는 것을 표현. 사용자로부터 정보를 받아 모델에 업데이트</p>
<h2 id="controller---view">Controller -&gt; View</h2>
<p>항상 가능. Outlet으로 연결.</p>
<h2 id="model---view">Model -&gt; View</h2>
<p>절대 소통 불가능. 모든 소통은 Controller를 통해 이루어짐.</p>
<h2 id="view---controller">View -&gt; Controller</h2>
<p>제한적으로 가능. 눈에 보이지 않고 구조화되어 있어야 함.</p>
<p>구조화?</p>
<ol>
<li>Target action</li>
<li>Delegate(View 내의 property) - 예를 들어 ScrollView 가 zoom in/out, scroll 과 같은 액션을 할 때 컨트롤러에게 물어봐야 함</li>
</ol>
<p>View는 자신이 보여주고 있는 데이터를 소유할 수 없다!</p>
<p>그렇다면 어떻게 표시? Controller에게 물어본다. Data source 라는 property를 이용해서 controller에게 위임하여 원하는 정보를 얻을 수 있다.</p>
<h2 id="model---controller">Model -&gt; Controller</h2>
<p>불가능. UI와 모델은 관련이 없다.<br>
모델이 값이 바뀌는 데이터를 가지고 있다면 controller에게 어떻게 소통? -&gt; <strong>Notification</strong></p>


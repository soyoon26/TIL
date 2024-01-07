리액트는 속성을 PROP이라고 부름 !
props 예시

```
function Header(props){
	return <header>
    	<h1>{props.title}</h1>
    </header>
}

function App(){
	return (
       <div>
          <Header title = "Hi"></Header>
       </div>
    );
}
```

---

```
functino Nav(props){
	const lis = [
      ]
      for(let i=0; i<props.topics.length; i++){
        let t = props.topics[i];
        lis.push(<li key={t.id}><a href={'/read'+t.id}>{t.title}</a></li>)
    }
	return <nav>
   	  <ol>
        {lis}
      </ol>
   </nav>
}

function App(){
  const topics = [
    {id:1, title: 'hi', body:'hi is haha'}
    {id:2, title: 'hello', body:'hello is hi'}
    {id:3, title: 'nice to meet you', body:'nice is'}
  ]
  return (
  	<div>
      <Nav topics={topics}></Nav>
    </div>
  )
}

export default App()
```

""으로 전달하면 문자열로 전달되기 때문에 {}인 중괄호로 전달해야 함 !
for에는 key값 넣어주기

컴포넌트는 어떤 값을 주냐에 따라 다른게 작동하게 된다

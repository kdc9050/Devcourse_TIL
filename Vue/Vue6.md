## vue 컴포넌트 데이터 전달

- props를 객체형태로 전달받는게 좋음
- 단순하게 배열로 받는법, 객체로 여러 데이터 추가해서 받는법

1. 부모컴포넌트에서 props 전달하는 방법
   1.1 props를 사용하는 방법 (부모-> 자식)
2. 자식컴포넌트에서 props 받는 방법
   2.1 props 속성으로 배열로 지정하는 방법
   2.2 props 속성으로 객체로 지정하는 방법

```
props:{
  title:String,
  likes:Number,
}
```

- 타입은 옵션 방법
- type은 기초 타입 값
- validator는 함수로 값이 유효한지 확인하는 함수
- required는 필수값 여부
- default는 기본값
- 함수도 넘길 수 있음=> props의 값을 넘길때 - 기호써서 함수로 넘김 =>print-Hello

### 함수를 전달하는 또 다른 방법

- 함수 전달할 때 :handle-event="함수명" 이게 첫번째 방법이고 이건 그냥 props로 전달하는 방법
- 두번째는 @handle-event="함수명" 이렇게 이벤트로 전달하는 방법
  - 이건 받을때 emits으로 받아야함 => $emit('handle-event')
  - `<SecondChild :name="name" :print-hello="printHello" @greet="$emit('greet')" />` => 이렇게 받아야함
- emit은 이벤트를 발생시키는 함수
- 컴포넌트 하나 이동이면 @greet="$emit('greet')" 이렇게 하는 게 좋음
- 컴포넌트 두개 이상이면 props로 전달하는게 좋음

### 공통 props (provide, inject)

- provide는 부모에서 자식으로 데이터를 전달할 때 사용
- inject는 자식에서 부모로 데이터를 전달할 때 사용
- provide는 객체로 전달하고 inject는 배열로 전달

```js
provide:{
  name:'Kim',
  age:20,
},
inject:['name','age'],
```

```js
provide: function(){
  return{
    name:'Kim',
    age:20,
  }
}
```

- 객체상태의 provide는 고정된 데이터 공급할 때
- 함수형태의 provide는 다른 옵션 api 데이터, 메서드 공급할때
- provide로 공급하는 데이터는 반응성을 가지지 않는다 => 데이터가 변경되어도 반응하지 않음
  - count: computed(() => this.count) 이렇게 computed로 사용해야함
  - computed 함수로 사용하면 반응성을 가짐
- inject를 다른 이름으로 지정해서 사용할 수 있음
  - 원래는 `inject:['count']` 이렇게 사용하는데
  - `inject:{ secondCount:{ from:'count2', default:0 } }` 이렇게 사용할 수 있음
- symbol을 사용해서 데이터를 전달할 수 있음
  - const count = Symbol('count');
  - provide(){
    return{
    [count]: 0,
    }
    }
  - inject:{ count: { from: count, default:0 } }

## ref 함수

- 부모컴포넌트가 자식컴포넌트를 참조하는 것
- ref는 자식컴포넌트의 인스턴스를 참조하는 것
- `this.$refs.참조이름` 이렇게 사용
- `this.$parent.$refs.참조이름` 이렇게 부모컴포넌트에서도 참조할 수 있음

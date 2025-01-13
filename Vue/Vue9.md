## vue pinia persist

- https://github.com/prazdevs/pinia-plugin-persistedstate
- npm i pinia-plugin-persistedstate

```
//main.js
import { createPinia } from 'pinia'
import piniaPluginPersistedstate from 'pinia-plugin-persistedstate'

const pinia = createPinia()
pinia.use(piniaPluginPersistedstate)
```

```
//store.js
export const useStore = defineStore('store', () => {
  const someState = ref('hello pinia')
  return { someState }
}, {
  persist: {
    storage: sessionStorage,
    pick: ['someState'],
  },
})
```

## vue 데이터 통신

- npm install json-server@0.17.0
- package.json => "db": "json-server --watch src/db.json";
  - "db:delay" : "json-server --watch src/db.json --delay 2000"

### vue fetch

- Get 요청

```
//Get
onBeforeMount(async () => {
  const response = await fetch("http://localhost:3000/posts");
  const data = await response.json();
  posts.value = data;
});
```

- Post 요청

```
//Post
const handlePost = async () => {
  const response = await fetch("http://localhost:3000/posts", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify({
      title: "New Post2",
      author: "Vue Fetch",
    }),
  });

  if (response.ok) {
    const data = await response.json();
    posts.value.push(data);

    console.log(data);
  }
};
```

- Put 요청

```
const handlePut = async () => {
  const response = await fetch("http://localhost:3000/posts/3", {
    method: "PUT",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify({
      title: "Updated Post",
      author: "Vue Fetch",
    }),
  });
  if (response.ok) {
    const data = await response.json();
    posts.value = posts.value.map((post) =>
      post.id === data.id ? { ...data } : post
    );
    console.log(data);
  }
};
```

- Patch 요청

```
const handlePatch = async () => {
  const response = await fetch("http://localhost:3000/posts/3", {
    method: "PATCH",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify({
      title: "Patched Post",
    }),
  });
  if (response.ok) {
    const data = await response.json();
    posts.value = posts.value.map((post) =>
      post.id === data.id ? { ...data } : post
    );
    console.log(data);
  }
};
```

- Delete 요청

```
const handleDelete = async (id) => {
  const response = await fetch(`http://localhost:3000/posts/${id}`, {
    method: "DELETE",
  });
  if (response.ok) {
    posts.value = posts.value.filter((post) => post.id !== id);
  }
};
```

### vue axios

- npm install axios

```
//Get
onBeforeMount(async () => {
  try {
    const { data, status } = await axios.get("http://localhost:3000/posts");
    if (status === 200) posts.value = data;
  } catch (error) {
    console.error(error);
  }
});
//Post
const handlePost = async () => {
  try {
    const { data, status } = await axios.post("http://localhost:3000/posts", {
      title: "New Post2",
      author: "Vue Axios",
    });
    if (status === 201) posts.value.push(data);
  } catch (error) {
    console.error(error);
  }
};

//Put - 리소스 전체를 업데이트
const handlePut = async () => {
  try {
    const { data, status } = await axios.put("http://localhost:3000/posts/3", {
      title: "Updated Post",
      author: "Vue Axios",
    });
    if (!status === 200) throw new Error("오류");
    posts.value = posts.value.map((post) =>
      post.id === data.id ? { ...data } : post
    );
  } catch (error) {
    console.error(error);
  }
};

//Patch - 리소스 일부분만 업데이트
const handlePatch = async () => {
  try {
    const { data, status } = await axios.patch(
      "http://localhost:3000/posts/2",
      {
        title: "Patched Post",
        author: "Vue Axios",
      }
    );
    if (!status === 200) throw new Error("오류");
    posts.value = posts.value.map((post) =>
      post.id === data.id ? { ...data } : post
    );
  } catch (error) {
    console.error(error);
  }
};

//Delete
const handleDelete = async (id) => {
  try {
    const { status } = await axios.delete(`http://localhost:3000/posts/${id}`);
    if (!status === 200) throw new Error("오류");
    posts.value = posts.value.filter((post) => post.id !== id);
  } catch (error) {
    console.error(error);
  }
};
```

- env 파일 설정

```
VUE_APP_API_URL=http://localhost:3000
```

```
/Get
await axios.get(`${import.meta.env.VITE_API_URL}/posts`);
```

### Suspense

- Suspense는 비동기 컴포넌트를 렌더링하는 동안 로딩 상태를 처리하는 컴포넌트
- Suspense 컴포넌트는 비동기 컴포넌트를 렌더링하는 중에 fallback 속성에 정의된 컴포넌트를 렌더링

---
title: About Data Store
category: Architecture
tags: frontend architecture
toc: true
toc_label: "Contents"
---

# Data Store

이 글은 MobX 의 공식 문서를 참고, 정리한 것입니다.
거의 모든 내용이 동일하고, 컨텐츠에 대한 모든 권리는 MobX에 있습니다.

# Store

스토어는 플럭스 아키텍처의 공통된 개념입니다.
이는 고전적인 `MVC 패턴`의 컨트롤러와는 약간 다릅니다.

스토어의 주요한 책임은, 

- **컴포넌트의 로직과 상태를 프론트엔드 및 백엔드에서 사용할 수 있고,**
- **독립적으로 테스트할 수 있는 단위로 만드는 것**

입니다.

대부분의 애플리케이션에서는 적어도 2개의 저장소

- **도메인 state 저장소**
- **UI state 저장소**

를 권장합니다.

이렇게 둘을 분리함으로써, 도메인 state를 전체적으로 **재사용하고, 테스트**할 수 있는 장점이 있고,

다른 애플리케이션에서 재사용할 수 있습니다.

## Domain Store

하나의 애플리케이션에는 아마도 **`도메인 스토어`**가 하나이상은 있습니다.
이 스토어데는 애플리케이션의 모든 데이터(Todo items, users, books, movies 등의 `도메인 객체`)가 저장됩니다.
하나의 도메인 스토어는 애플리케이션에서 ***하나의 개념*** 만을 책임집니다. 하나의 도메인 스토어는 종종 여러가지 도메인 객체가 내부에 있는 트리 구조(**컴포지트 패턴**)으로 구성됩니다. 

예를 들어, **상품에 관한 도메인 스토어** 하나와, **주문 및 주문 정보에 관한 스토어**가 있다고 가정합시다.
일반적으로 두 항목이 포함 관계인 경우, 동일한 저장소에 있어야합니다.
즉, 스토어는 *도메인 객체* 를 관리하게 됩니다.

스토어가 가지는 책임은 다음과 같습니다.

- **도메인 객체를 인스턴스화 합니다.(도메인 객체가 자신이 속한 저장소를 알고 있는지 확인합니다.)**
- **각 도메인 객체의 인스턴스가 하나만 있는지 확인합니다. 동일한 도메인 객체가 2개 이상 메모리에 있어서는 안됩니다. 이렇게 하면, 참조가 안전해지며, 참조를 확인할 필요없이 최신의 인스턴스만 참조하게 됩니다. 이러한 방식은 디버깅할 때 빠르고, 편리합니다.**
- **백엔드 통합을 제공합니다. 필요할 때 데이터를 저장합니다.**
- **백엔드에서 업데이트 내용을 받은 경우, 기존의 인스턴스를 업데이트합니다.**
- **독립적이고, 일반적이고, 테스트할 수 있는 애플리케이션 컴포넌트를 제공합니다.**
- **스토어를 테스트할 수 있고, 서버 측에서 실행할 수 있는지 확인하기 위해, 실제 웹 소켓, 혹은 http 요청을 별도의 객체로 이동하여, 통신 계층을 추상화할 수 있습니다.**
- **스토어 인스턴스는 하나만 있어야합니다.**

## 도메인 객체

각 `도메인 객체`는 자체 클래스(혹은 생성자 함수)를 사용하여 표현해야합니다. 클라이언트 애플리케이션 state를 일종의 데이터베이스로 취급할 필요가 없습니다.

실제 참조, 순환 데이터 구조 및 인스턴스 메소드는 `JS`의 강력한 개념입니다. 도메인 객체는 다른 스토어의 도메인 객체를 직접 참조할 수 있습니다.

우리의 `action`과 `view`는 최대한 단순해야 합니다.

MobX의 패턴을 사용하면, **업무 규칙, 액션과 사용자 인터페이스**를 훨씬 간단하게 구축할 수 있습니다.

도메인 객체는 경우에 따라 자신의 모든 로직을 자신이 속한 스토어에 위임할 수 있습니다.
도메인 객체는 plain 객체가 될 수 있지만, 클래스로 표현될 때 강점이 있습니다.

- **멤버 함수를 가집니다. 멤버 함수를 통해 도메인 개념을 독립 실행형으로 더 쉽게 사용하고, 애플리케이션에 필요한 컨텍스트의 인식의 양을 줄일 수 있습니다. 그냥 객체를 전달해 주기만 하면 됩니다. 인스턴스 메소드만을 사용하는 경우, 스토어를 전달하거나, 객체에 적용할 수 있는 액션을 파악할 필요가 없습니다. 이는 대규모 애플리케이션에서 중요합니다.**
- **속성 및 메소드의 가시성을 세밀하게 제어할 수 있습니다.**
- **생성자 함수를 사용하여 생성된 객체는 observable 속성 및 메소드와 non-observable 속성 및 메소드를 자유롭게 섞어 쓸 수 있습니다.**
- **가독성이 좋고 강한 타입핑이 가능합니다.**

## 도메인 스토어의 예시

```jsx
import { makeAutoObservable, autorun, runInAction } from "mobx"
import uuid from "node-uuid"

export class TodoStore {
    authorStore
    transportLayer
    todos = []
    isLoading = true

    constructor(transportLayer, authorStore) {
        makeAutoObservable(this)
        this.authorStore = authorStore // 작성자를 확인할 수 있는 스토어
        this.transportLayer = transportLayer // 서버 요청을 할 수 있는 것
        this.transportLayer.onReceiveTodoUpdate(updatedTodo =>
            this.updateTodoFromServer(updatedTodo)
        )
        this.loadTodos()
    }

    // 서버에서 모든 todo를 가져옵니다.
    loadTodos() {
        this.isLoading = true
        this.transportLayer.fetchTodos().then(fetchedTodos => {
            runInAction(() => {
                fetchedTodos.forEach(json => this.updateTodoFromServer(json))
                this.isLoading = false
            })
        })
    }

    // 서버의 정보로 Todo를 업데이트합니다. Todo가 한 번만 존재함을 보장합니다.
    // 새로운 Todo를 생성하거나 기존 Todo를 업데이트하거나 
    // 서버에서 삭제된 Todo를 제거할 수 있습니다.
    updateTodoFromServer(json) {
        let todo = this.todos.find(todo => todo.id === json.id)
        if (!todo) {
            todo = new Todo(this, json.id)
            this.todos.push(todo)
        }
        if (json.isDeleted) {
            this.removeTodo(todo)
        } else {
            todo.updateFromJson(json)
        }
    }

    // 클라이언트와 서버에 새로운 Todo를 생성합니다.
    createTodo() {
        const todo = new Todo(this)
        this.todos.push(todo)
        return todo
    }

    // Todo가 어떻게든 삭제되었을 때 클라이언트 메모리에서 삭제합니다.
    removeTodo(todo) {
        this.todos.splice(this.todos.indexOf(todo), 1)
        todo.dispose()
    }
}

// 도메인 객체 Todo.
export class Todo {
    id = null // Todo의 고유 id, 변경할 수 없습니다.
    completed = false
    task = ""
    author = null // authorStore에서 가져온 Author 객체에 대한 참조
    store = null
    autoSave = true // Todo의 변경사항을 서버에 제출하기 위한 표시
    saveHandler = null // todo를 자동저장하는 부수효과의 Disposer(dispose).

    constructor(store, id = uuid.v4()) {
        makeAutoObservable(this, {
            id: false,
            store: false,
            autoSave: false,
            saveHandler: false,
            dispose: false
        })
        this.store = store
        this.id = id

        this.saveHandler = reaction(
            () => this.asJson, // JSON에서 사용되는 모든 것을 관찰합니다.
            json => {
                // autoSave가 true이면 JSON을 서버로 보냅니다.
                if (this.autoSave) {
                    this.store.transportLayer.saveTodo(json)
                }
            }
        )
    }

    // 클라이언트와 서버에서 해당 Todo를 제거합니다.
    delete() {
        this.store.transportLayer.deleteTodo(this.id)
        this.store.removeTodo(this)
    }

    get asJson() {
        return {
            id: this.id,
            completed: this.completed,
            task: this.task,
            authorId: this.author ? this.author.id : null
        }
    }

    // 서버의 정보로 Todo를 업데이트합니다.
    updateFromJson(json) {
        this.autoSave = false // 변경 사항을 서버로 다시 보내는 것을 방지합니다.
        this.completed = json.completed
        this.task = json.task
        this.author = this.store.authorStore.resolveAuthor(json.authorId)
        this.autoSave = true
    }

    // observer를 청소합니다.
    dispose() {
        this.saveHandler()
    }
}
```

## UI Store

**ui-state-store**에는 애플리케이션에 대해 매우 구체적이지만, 간단합니다.
**ui-state-store**에는 로직이 많지는 않지만, 느슨하게 결합한 UI에 대해 많은 정보를 저장합니다. 
이는 대부분의 애플리케이션이 개발 프로세스 중에 UI state을 자주 변경하므로 이상적입니다.

UI Store는 주로 다음과 같은 정보가 저장됩니다.

- **세션 정보**
- **애플리케이션이 로드된 정도에 대한 정보**
- **백엔드에 저장되지 않을 정보**
- **UI에 전체적으로 영향을 미치는 정보**
    - **Window dimensions**
    - **Accessibilithy Information**
    - **Current Language**
    - **Currently active theme**
- **관련없는 여러가지 컴포넌트에 영향을 미치는 유저 인터페이스 state**
    - **현재 선택 항목**
    - **툴바 가시성**
    - **위저드 state**
    - **전역 overlay state**

이러한 정보들은 특정 컴포넌트의 `내부 state`(예, 모달의 visibility)로 시작되지만, 이후 애플리케이션의 다른 위치에도 이 정보가 필요하다는 것을 알게됩니다. 일반적인 React 앱에서와 같이, 컴포넌트 트리에서 위쪽으로 state를 푸시하는 대신, state를 ui-state-store로 이동시키면 됩니다.

동형 애플리케이션의 경우, 모든 컴포넌트가 예상대로 렌더링 되도록 기본값으로 저장소의 스텁(stub) 구현을 제공할 수도 있습니다. 애플리케이션에 Context API를 이용하여 ui-state-store를 배포할 수 있습니다.

### UI State 예시

```jsx
import { makeAutoObservable, observable, computed, asStructure } from "mobx"

export class UiState {
    language = "en_US"
    pendingRequestCount = 0

    // .struct는 dimension 객체가 deepEqual 방식으로 
    // 변경되지 않는 한 observer가 신호를 받지 않도록 합니다.
    
    windowDimensions = {
        width: window.innerWidth,
        height: window.innerHeight
    }

    constructor() {
        makeAutoObservable(this, { windowDimensions: observable.struct })
        window.onresize = () => {
            this.windowDimensions = getWindowDimensions()
        }
    }

    get appIsInSync() {
        return this.pendingRequestCount === 0
    }
}
```

## 스토어 결합하기

싱글톤을 사용하지 않고 여러 스토어를 결합하는 방법에 대해 이야기해봅시다.

효과적인 패턴은 모든 저장소를 인스턴스화하고, 참조를 공유하는 `RootStore`를 만드는 것입니다. 이러한 패턴은 다음과 같은 장점이 있습니다.

1. 설정이 간단합니다.
2. 강력한 타이핑을 지원합니다.
3. 루트 저장소를 인스턴스화 하기만 하면, 복잡한 유닛 테스트를 쉽게 할 수 있습니다.

```jsx
class RootStore {
    constructor() {
        this.userStore = new UserStore(this)
        this.todoStore = new TodoStore(this)
    }
}

class UserStore {
    constructor(rootStore) {
        this.rootStore = rootStore
    }

    getTodos(user) {
        // root 저장소를 통해 todoStore에 접근합니다.
        return this.rootStore.todoStore.todos.filter(todo => todo.author === user)
    }
}

class TodoStore {
    todos = []
    rootStore

    constructor(rootStore) {
        makeAutoObservable(this, { rootStore: false })
        this.rootStore = rootStore
    }
}
```

# 마치며

데이터 스토어에 대한 내용을 학습하며, 애플리케이션의 클린 아키텍처를 다시한번 생각하게 되었습니다.
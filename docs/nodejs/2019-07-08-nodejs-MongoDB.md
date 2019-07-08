# MongoDB

---

- MongoDB 는 document 또는 NoSQL 데이터베이스 이다.

    - 단순히 `json 객체`를 저장한다.

    - 데이터를 `querying` 할 때 MongoDB로부터 `json 객체`를 가져와서 클라이언트에게 전달한다.

- 따라서 관계형 데이터베이스와는 달리 테이블, 스키마, 뷰, 레코드 같은 게 없다.

- MongoDB의 `collection`은 관계형 데이터베이스의 `table`과 비슷하다.

- MongoDB의 `document`는 관계형 데이터베이스의 `row`와 비슷하다.

## Mongoose

> Mongoose gives us a simple api to work with a MongoDB

- Mongoose는 MongoDB ODM(Object Document Mapping)이다.

    - 문서를 DB에서 조회할 때 `json 객체`로 바꿔주는 역할을 한다.

#### Mongoose의 장점

- 강제 스키마(`schema`)의 부활

- `populate`

- `프로미스`와 `콜백` 사용 가능

- 편리한 `쿼리 빌더` 등


### schema

- Mongoose에는 `schema`라는 개념이 있다. MongoDB에는 없는 `schema`를 Mongoose를 이용하면 사용할 수 있다.

- `schema`는 `collection`안에 있는 `documents`의 구조를 정의할 때 사용된다.

![](https://user-images.githubusercontent.com/34808501/60753298-1641b480-a00b-11e9-9e4e-d2dd4fd24063.png)

- 예를 들어, 온라인 강의 데이터를 관리하는 MongoDB가 있다고 할 때 강의 스키마(`schema for course`)를 다음과 같이 만들 수 있다.

```js
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost/playground')
    .then(() => console.log('Connected to MongoDB'))
    .catch(err => console.error('Could not connect to MongoDB...', err))

const courseSchema = new mongoose.Schema({
    name: String,
    author: String,
    tags: [ String],
    date: { type: Date, default: Date.now},
    isPublished: Boolean
})
```

- 스키마(`schema`)를 만들었으면 `model`에 컴파일(`compile`)시켜야한다.

### What is model?

- 모델(`model`)이란 무엇일까?

- 예를 들어, 강의 스키마(`courseSchema`)에서 `nodeCourse`를 만들었다고 가정해보자.

- 이 둘의 관계는 클래스(`class`)와 인스턴스(`instance`)의 관계와 비슷하다.

    - 인스턴스를 만들기 위해서는 클래스가 필요한 것처럼

    - 어떤 강의 인스턴스(`nodeCourse`)를 만들기 위해서는 강의 클래스가 필요하다
    - 이 때, 강의 클래스를 만들기 위해서는 스키마(`schema`)를 `model`에 컴파일(`compile`)해줘야 한다.

### How to complie a schema into a model

- `mongoose`객체의 `model 메서드`를 이용하면 스키마(`schema`)를 `model`에 컴파일 할 수 있다.

- `mongoose`객체의 `model 메서드`는 두 개의 인자를 받는다.

    1. `model`이 사용할 `collection`의 **단일 이름**
    
    2. 해당 `collection`에서 `document` 구조를 정의하는 **스키마**(`schema`)

- `courseSchema`를 `model`에 컴파일하는 방법은 아래와 같다.

- `courseSchema`라는 스키마(`schema`)를 `model`에 컴파일하는 방법은 다음과 같다.

```js
const Course = mongoose.model('Course', courseSchema);
const course = new Course({
    name: 'Node.js Course',
    author: 'Sony',
    tags: ['node', 'backend'],
    isPublished: true
})
```

- `mongoose`객체의 `model 메서드`는 클래스를 리턴한다. 위 예제에서는 리턴 받은 클래스를 `Course`라는 변수에 할당했다.

- `Course` 변수에 담긴 클래스를 이용하여 `course` 객체를 생성 할 수 있다.

#### 정리

- 스키마(`schema`)를 생성한 다음에는 `model`에 컴파일(`compile`)해줘야 한다.

- `model 메서드`로 컴파일 하면 클래스를 리턴한다.

- 해당 클래스를 이용해서 객체를 생성할 수 있으며 이 객체를 통해 document를 MongoDB 안에 매핑(mapping)할 수 있다.

## Saving a Document

- `document`를 MongoDB에 어떻게 저장할까?

- `save 메서드`를 사용한다.

- `save 메서드`는 비동기로 동작하며 `promise`를 리턴한다.

    - DB에 접근해서 파일을 저장하는 과정을 수행하기 위해서는 어느 정도 시간이 소요되기 때문에 비동기로 처리해야한다.

- 따라서 `async await`을 이용해서 비동기 작업이 끝나기를 기다렸다가 완료되면 결과를 받으면 된다.

- 아래 코드와 같이 작성해주면 된다.

```js
const Course = mongoose.model('Course', courseSchema);

async function createCourse(){
    const course = new Course({
        name: 'Node.js Course',
        author: 'Sony',
        tags: ['node', 'backend'],
        isPublished: true
    })
    
    const result = await course.save()
    console.log(result);
}
createCourse();
```

```bash
{ tags: [ 'node', 'backend' ],
  date: 2019-07-06T08:01:54.830Z,
  _id: 5d205572a2c42b8c9fc77e74,
  name: 'Node.js Course',
  author: 'Sony',
  isPublished: true,
  __v: 0 }
```

- DB에 저장된 결과값을 확인해보면 `_id: 5d205572a2c42b8c9fc77e74`가 추가된 것을 볼 수 있다.

- MongoDB는 `course 객체`를 저장할 때 객체 식별을 위해 `id`를 할당한다.

## Querying Document

- MongoDB 데이터베이스에서 `documents`를 검색하기 위해서는 `find` 메서드를 사용하면 된다.

- `find()`: **filter** documents

```js
async function getCourses(){
    const courses = await Course
        .find({author: 'Sony', isPublished: true})
        .limit(10)
        .sort({name: 1})
        .select({name: 1, tags: 1})
    console.log(courses);
}

getCourses();
```

- `sort()`: `1`: 오름차순(`ascending order`), `-1`: 내림차순(` descending order`)

```bash
[ { tags: [ 'node', 'backend' ],
    _id: 5d205572a2c42b8c9fc77e74,
    name: 'Node.js Course' },
  { tags: [ 'react', 'frontend' ],
    _id: 5d2057ec06be2e8cf631c896,
    name: 'React Course' } ]
```

### comparison query operator

> 비교 연산자

- `eq` : equal
- `ne` : not equal
- `gt` : grater than
- `gte` : grater than or equal to
- `lt` : less than
- `lte` : less than or equal to
- `in`
- `nin` : not in

```js
async function getCourses(){
    const courses = await Course
        .find({ price: { $gte: 10 $lte: 20} }) // price between 10~20
        .find({ price: { $in: [10, 15, 20]} }) // price at 10 or 15 or 20
}

getCourses();
```

### logical query operator

> 논리 연산자

- `or`
- `and`

```js
async function getCourses(){
    const courses = await Course
        .find()
        .or([ { author: 'Sony}, { isPublished: true} ])
        .limit(10)
        .sort({name: 1})
        .select({name: 1, tags: 1})
    console.log(courses);
}

getCourses();
```

### regular expression

```js
async function getCourses(){
    const courses = await Course
        
        //Starts with Sony
        .find({ author: /^Sony/})

        // Ends with Sony
        .find({ author: /Sony$/})
        
        // Contains Sony
        .find({ author: /.*Sony.*/})

        .limit(10)
        .sort({name: 1})
        .select({name: 1, tags: 1})
    console.log(courses);
}

getCourses();
```

### count

- `documents`의 갯수를 알고 싶을 때는 `count` 메서드를 사용한다.

```js
async function getCourses(){
    const courses = await Course
        .find({author: 'Sony', isPublished: true})
        .limit(10)
        .sort({name: 1})
        .count(); // return documents that match our filter
    console.log(courses);
}

getCourses();
```

### pagination

> 페이징

```js
async function getCourses(){
    const pageNumber = 2; // get a page number from users
    const pageSize = 10;

    const courses = await Course
        .find({author: 'Sony', isPublished: true})
        .skip((pageNumber-1) * pageSize)
        .limit(pageSize)
        .sort({name: 1})
        .select({name: 1, tags: 1})
    console.log(courses);
}

getCourses();
```

## Updating documents

- MongoDB의 `documents`를 수정하는 방법은 크게 두 가지가 있다.

> `1. Query First`
>
> `2. Update First`

### 1. Query First

1. `findById()` : `id`로 `document`를 가져온다.

2. `Modify its properties` : 해당 `document`의 속성을 수정한다.

3. `save` : 수정 사항을 저장한다.

```js
const Courses = mongoose.model('Course', courseSchema);

async function updateCourse(id) {
    // findById()
    const course = await Courses.findById(id);
    if(!course) return;
    
    // Modify its properties
    course.isPubliched =true;
    course.name = 'Another Author';

    // save
    return await course.save();
}


async function run(){
    const result = await updateCourse('5d2094879aeabbd60d3530fa')
    console.log(result)
}
run()
```

### 2. Update First

> document를 가져올 필요 없이 바로 값을 수정해야 할 때 쓰인다. 
>
> ex) 좋아요 수 업데이트

1. Update directly : `id`로 `document`에 접근해 바로 수정한다.

2. Optionally : get the updated documnet

```js
const Courses = mongoose.model('Course', courseSchema);

async function updateCourse(id) {
     return await Courses.update({_id: id}, {
        $set: {
            author: 'Sony',
            isPubliched: false
        }
    });
}


async function run(){
    const result = await updateCourse('5d2094879aeabbd60d3530fa')
    console.log(result)
}
run()
```

```bash
{ n: 1, nModified: 1, ok: 1 }
```

- 수정 할 `document`를 리턴하고 싶으면 `findByIdAndUpdate` 메서드를 사용한다.

```js
const Courses = mongoose.model('Course', courseSchema);

async function updateCourse(id) {
     return await Courses.findByIdAndUpdate(id, {
        $set: {
            author: 'Park',
            isPubliched: true
        }
    });
}


async function run(){
    const result = await updateCourse('5d2094879aeabbd60d3530fa')
    console.log(result)
}
run()
```

```bash
{ tags: [ 'node', 'backend' ],
  _id: 5d2094879aeabbd60d3530fa,
  date: 2018-01-24T21:44:01.075Z,
  name: 'Another Author',
  author: 'Sony',
  isPublished: true,
  price: 12,
  __v: 0,
  isPubliched: false }
```

- it returns the original document.

- `findByIdAndUpdate` 메서드는 디폴트로 `수정 되기 전의 document`를 리턴한다.

- `수정 사항이 반영된 document`를 리턴하고 싶으면  `{new: true}` option을 추가해준다.


```js
const Courses = mongoose.model('Course', courseSchema);

async function updateCourse(id) {
     return await Courses.findByIdAndUpdate(id, {
        $set: {
            author: 'Sony Park',
            isPubliched: false
        }
    }, {new: true}); // set the new property to true
}


async function run(){
    const result = await updateCourse('5d2094879aeabbd60d3530fa')
    console.log(result)
}
run()
```


```bash
{ tags: [ 'node', 'backend' ],
  _id: 5d2094879aeabbd60d3530fa,
  date: 2018-01-24T21:44:01.075Z,
  name: 'Another Author',
  author: 'Sony Park',
  isPublished: true,
  price: 12,
  __v: 0,
  isPubliched: false }
```

## Removing document

- `deleteOne` : `document` 하나를 삭제한다.

- `deleteMany` : 여러 개의 `document`를 삭제한다.

- `findByIdAndRemove` : `document`를 삭제하고 삭제된 `document`를 리턴한다.

```js
async function removeCourse(id) {
    return await Courses.deleteOne(id); 
}
```

```js
async function removeCourse(id) {
    return await Courses.findByIdAndRemove(id); 
}
```

### Reference

- [Udemy: Mosh nodejs-master-class](https://www.udemy.com/nodejs-master-class)
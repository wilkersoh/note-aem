- [Frontend](#frontend)
  * [data-sly-list](#data-sly-list)
- [Backend](#backend)


# Frontend

## data-sly-list

他可以return

1. `array` 
2. `list` 
    - String/Int/etc

    ```html
    <!-- sly-use.anyNameYouWant 這個就像 import 這個 class 進來 -->
    <div data-sly-use.itemBooks="pathToTheClass"></div>

    <!-- itemBooks.books, books 是在backend的class getBooks 到frontend就是 books -->
    <div data-sly-list.bookName="${itemBooks.books @ begin = 0, end = 3}">
    	<p>Book name: ${bookName}</p>
    	這裡只會顯示4個 bookName[0] 到 3；
    	
    	<p>#${bookNameList.count}: + List.count 就可以拿到這個bookName是在那個list裡的第幾個了,不過它的 從0 它會從1, 用 .index 就是0 </p>
    </div>

    <!-- 分割線 -->
    <!-- 用 step， 每次loop 就 + 2 -->
    <div data-sly-use.itemBooks="pathToTheClass"></div>

    <div data-sly-list.bookName="${itemBooks.books @ begin = 0, step = 2, end = 7}">
     這裡會 print出 第一個， 第3個， 第5個，第7個
    </div>

    <!-- 分割線 -->
    <!-- 可以做一點判斷 return true or false 和 拿它的index-->
    <div data-sly-list.bookNames="${itemBooks.books}">
    	<p>Index: ${bookNamesList.index}</p>
    	<p>isFirst: ${bookNamesList.first}</p>
    	<p>isMiddle: ${bookNamesList.middle}</p>
    	<p>isLast: ${bookNamesList.last}</p>
    	<p>isOdd: ${bookNamesList.odd}</p>
    	<p>isEven: ${bookNamesList.even}</p>
    </div>

    <!-- 分割線 -->
    <!-- 
    	data-sly-repeat 這個是 整個 repeat的 element都 一起loop 
    	就像 vue的 <div v-for=""></div> 一模一樣
     -->
    <div class="repeat" data-sly-repeat.bookNames="${itemBooks.books}">
    	
    </div>
    ```

    - Map
    - POJO / BEAN
3. `Map`

    ```html
    <!-- sly-use.anyNameYouWant 這個就像 import 這個 class 進來 -->
    <div data-sly-use.htl="pathToTheClass"></div>

    <div data-sly-list.anyName="${htl.booksMap}">
    	<!-- 
    		map的 data type差不多是長這樣, 它會有 key和value
    		{
    			key1: value1,
    			key2: value2,
    		};
    		
    		anyName print出來 會是 key1先
    	-->
    	<p>key: ${ anyName }</p>

    	<!--
    		How to print value?
    	-->
    	<p>${htl.booksMap[anyName]}</p>
    </div>
    ```

# Backend

```java
// core\src\main\java\com\taylorsuniversity\models\HeaderComponentModel.java

public final class HeaderComponentModel {
	public List<Page> getNavigationSectionModelBean() {
/**
這個 getNavigationSectionModelBean的意思 是 pass去frontend的東西
在frontend要拿到是從header.navigationSectionModelBean
*/
	}
}
```

Frontend

```html
<!-- 需要表明 use.valueStoreObjName="pathToTheClass" --> 
<div data-sly-use.header="com.taylorsunviversity.models.HeaderComponentModel">
	<div data-sly-list.item="${header.navigationSectionModelBean}">

	</div>
</div>
```

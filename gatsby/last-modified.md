# Published 와 Last Updated 여러 접근법

##  1.MDX의 frontmatter 필드추가하기 





블로그의 포스트 같은 경우는 누군가의 피드백도 받는 경우도 있고, 수정해야 할 일들이 꽤나 생긴다. 포스트를 변경할 때마다 마지막 변경 시점을 graphql에서 아마 사용할 수 있지 않을까 했는데 역시나 쿼리를 실행할 수 있는 필드가 있었다.

```graphql
query MyQuery {
 
  allFile {
    nodes {
      birthTime
      mtime
      modifiedTime
    }
  }
}

```

 mtime 또는 modifiedTime 필드가 마지막으로 수정한 날의 정보를 알려준다. 

 하지만 이 modifiedTime은 gatsby빌드시에도 적용이 되어 모든 파일이 같은 날짜\(빌드한 날짜\) 를 가지게 된다. 

{% embed url="https://joshuatz.com/posts/2019/gatsby-better-last-updated-or-modified-dates-for-posts/" %}



`lastModified` 와 pushlished 날짜를 구분하기 위해서  frontmatter에 date필드대신 사용자 정의로 published와 lastModified 필드를 대체하였다. 

이런 내 접근이 올바르지 않다는것을 gatsby에서 알려주었다.  

![](../.gitbook/assets/screen-shot-2021-10-03-at-11.06.54-am.png)

공식문서에서  참고하자면 

> This will confuse Gatsby’s type inference since the `joinedAt` field will now have both Date and String values.

 해결은 명시적으로 type definitions를 지정하여  [`createTypes`](https://www.gatsbyjs.com/docs/reference/config-files/actions/#createTypes) action 과 함께 사용하라고 하라고 한다. 



 


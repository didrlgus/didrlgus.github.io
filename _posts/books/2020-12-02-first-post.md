---
layout: single
classes: wide

title: "첫번째 포스트"
excerpt: "발췌부분 설정하면 이 글이 들어가고, 설정하지 않는다면 글의 첫 문단이 들어가게됨"

date: 2020-04-09 16:50:00 +0900
lastmod: 2020-04-09 16:50:00 +0900 # sitemap.xml에서 사용됨

author_profile: false # 왼쪽부분 프로필을 띄울건지

header:
  overlay_image: https://images.unsplash.com/photo-1501785888041-af3ef285b470?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1350&q=80
  overlay_filter: 0.5 # 투명도
  teaser: https://images.unsplash.com/photo-1501785888041-af3ef285b470?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1350&q=80

sidebar:
  nav: "docs"
  
categories: 
  - test post

tags: 
  - test
  - theme

# table of contents
toc: true # 오른쪽 부분에 목차를 자동 생성해준다.
toc_label: "Index" # toc 이름 설정
toc_icon: "cog" # 아이콘 설정
toc_sticky: true # 마우스 스크롤과 함께 내려갈 것인지 설정
---

### 목적
You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

### 환경
To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

### 내용
Jekyll also offers powerful support for code snippets:

### 코드
 ```java
package com.shoppingmall;

import com.shoppingmall.publisher.MessagePublisher;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.boot.builder.SpringApplicationBuilder;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.FilterType;

@ComponentScan(excludeFilters  = {@ComponentScan.Filter(
        type = FilterType.ASSIGNABLE_TYPE, classes = {MessagePublisher.class})})
@SpringBootApplication
public class OrderApplication {
    private static final String APPLICATION_LOCATIONS = "spring.config.location="
            + "classpath:application.yml,"
            //+ "/home/ec2-user/app/config/springboot-webservice/real-order-application.yml";
            + "C:\\config\\real-order-application.yml";

    public static void main(String[] args) {
        new SpringApplicationBuilder(OrderApplication.class)
                .properties(APPLICATION_LOCATIONS)
                .run(args);
    }
}
```

### 결과
Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
---
layout: post
title: "Composite - 그릇과 내용물을 동일시하기"
date: 2019-12-15 11:35:12 +0900
categories: pattern
published: false
---

자바(Java)에서는 `List`를 엘리먼트 추가와 동시에 생성하는 방법이 다양하게 제공되고 있다. jdk 8 이하 버전에서 지원되는 방법 중 몇 가지는 다음과 같다.

{% highlight java %}
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.Stream;

public class Main {

    public static void main(String[] args) {
        List<String> myFamily = new ArrayList<String>(){
            {
                add("Tommy");
                add("Jerry");
                add("Jolly");
            }
        };
        System.out.println(myFamily);

        List<String> whoIsJolly = Arrays.asList("Who", "is", "Jolly");
        System.out.println(whoIsJolly);

        List<String> myDaughter = Stream.of("She", "is", "my", "daughter").collect(Collectors.toList());
        System.out.println(myDaughter);

        List<String> imSoHappyForHer = Collections.singletonList("I'm so happy.");
        System.out.println(imSoHappyForHer);
    }

}
{% endhighlight %}

결과
{% highlight java %}
#=> [Tommy, Jerry, Jolly]
#=> [Who, is, Jolly]
#=> [She, is, my, daughter]
#=> [I'm so happy.]
{% endhighlight %}

소스코드는 Github Repository [initialize-list-with-elements]에 공유되어 있다.

[initialize-list-with-elements]: https://github.com/crzhacko/initialize-list-with-element
[//]: # "Java - 엘리먼트 추가와 함께 List를 생성하기"
[//]: # "Java - 엘리먼트 추가와 함께 ArrayList를 생성하기"
[//]: # "Java - List 한 줄로 생성"
[//]: # "Java - ArrayList 한 줄로 생성"

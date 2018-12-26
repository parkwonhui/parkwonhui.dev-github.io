---
layout: post
title: java null object pattern
categories: [java]
tags: [basic,java,pattern]
comments: true
---
- User.java

~~~
public abstract class User {
       protected String name;
       public abstract boolean isNull();
       public abstract String getName();
}
~~~

- Player.java

~~~
public class Player extends User{
       public Player() {}
       public Player(String _name) {
              name = _name;
       }
       @Override
       public boolean isNull() {
              return false;
       }
       @Override
       public String getName() {
              return name;
       }
}
~~~

- NullPlayer.java

~~~
public class NullPlayer extends User{
       public NullPlayer() {}
       public NullPlayer(String _name) {
              name = _name;
       }
       @Override
       public boolean isNull() {
              return true;
       }
       @Override
       public String getName() {
              return "Null Player";
       }
}
~~~
- PlayerFactory

~~~
public class PlayerFactory {
       public PlayerFactory(){}
       public User create(String name) {
              if(name.equals("PlayerName"))
                     return new Player(name);
              
              return new NullPlayer(name);
       }
}
~~~
- Main.java

~~~
public class Main {
       public static void main(String[] args) {
              PlayerFactory playerFactory = new PlayerFactory();
              User user1 = playerFactory.create("PlayerName");
              User user2 = playerFactory.create("Unkown");
              
              System.out.println("user1:"+user1.getName());
              System.out.println("user2:"+user2.getName());                 
       }
}
~~~




<div id="disqus_thread"></div>
<script>

/**
*  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
*  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables*/
/*
var disqus_config = function () {
this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
*/
(function() { // DON'T EDIT BELOW THIS LINE
var d = document, s = d.createElement('script');
s.src = 'https://parkwonhui.disqus.com/embed.js';
s.setAttribute('data-timestamp', +new Date());
(d.head || d.body).appendChild(s);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
                            
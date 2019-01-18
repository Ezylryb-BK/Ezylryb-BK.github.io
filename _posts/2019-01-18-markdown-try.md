---
layout: post
title: Try Markdown
subtitle: A test on the syntax here
gh-repo: daattali/beautiful-jekyll
gh-badge: [star,folk,follow]
tags: [test,try]
comments: true
---

# heading

**bold text**

table:
|name|id|class|
|:---|:---|:---|
|A|01|03|
|B|02|03|

picture:
![saber](../img/saber.comlex.jpg)

code chunk:

~~~
    #include<bits/stdc++.h>
    int main(){
        return 0;
    }
~~~

another code chunk:

```javascript
var name=Array();
name[0]=Ezylryb;
```

code with line numbers
{% highlight javascript linenos %}
var name=Array();
name[1]=Saber;
{% endhighlight %}

## boxes

### notification

{: notification .box-note}

### warning

{: warning .box-warning}

### error

{: error .box-error}

***
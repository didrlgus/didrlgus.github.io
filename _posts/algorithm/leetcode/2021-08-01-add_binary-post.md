---
layout: single
classes: wide

title: "[leetcode] add binary"
excerpt: "[leetcode] add binary 풀이입니다."

date: 2021-08-01 09:00:00 +0900
lastmod: 2021-08-01 09:00:00 +0900

author_profile: false

sidebar:
nav: "docs"

categories:
- algorithm

tags:
- algorithm
- leetcode

# table of contents
toc: true # 오른쪽 부분에 목차를 자동 생성해준다.
toc_label: "Index" # toc 이름 설정
toc_icon: "cog" # 아이콘 설정
toc_sticky: true # 마우스 스크롤과 함께 내려갈 것인지 설정
---


# 문제

* [https://leetcode.com/problems/add-binary/](https://leetcode.com/problems/add-binary/)

<br><br>

# 문제해결 과정

* 이진수 두개를 덧셈하는 문제다.
* 뒷자리부터 덧셈하고, 덧셈하면서 올림수를 잘 생각하면 어렵지 않게 해결할 수 있는 문제이다.

<br><br>

# 코드

```c++
class Solution {
public:
    string addBinary(string a, string b) {
        
        int a_size=a.size(),b_size=b.size();
        
        if (a_size>b_size) {
            int diff=a_size-b_size;
            while(diff--) b='0'+b;
        } else {
            int diff=b_size-a_size;
            while(diff--) a='0'+a;
        }
        string ret="";
        int t_size=a.size();
        int carry=0;
        for (int i=t_size-1;i>=0;i--) {
            int a_val=a[i]-'0',b_val=b[i]-'0';
            int val=a_val+b_val+carry;
            if (val>=2) carry=1;
            else carry=0;
            string str_val=to_string(val%2);
            ret=str_val+ret;
        }
        if (carry>=1) ret=to_string(carry)+ret;
        return ret;
    }
};
```

<br><br>

# 결과

* [https://leetcode.com/problems/add-binary/submissions/](https://leetcode.com/problems/add-binary/submissions/)
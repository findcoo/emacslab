
# Table of Contents

1.  [Emacs tutorial](#orgd9c0aea)
    1.  [Graphviz](#org91bab44)
        1.  [dot 문법](#org0ee7f81)
        2.  [예제 받아 출력](#orgde300a8)


<a id="orgd9c0aea"></a>

# Emacs tutorial


<a id="org91bab44"></a>

## Graphviz


<a id="org0ee7f81"></a>

### dot 문법

기본적으로 json형식 같이 key value 형식과 유사하며 키에 분포적인 정의가 가미된 형태다.
[]안의 요소는 선택적인 옵션을 ()안의 요소는 필요로 되는 요소들의 묶음. | 는 대체할 수 있는 요소를 표현.

1.  Simple Diagraph
    
        /* 
        graph: (graph | diagraph) [ID] 그래프의 형식을 선언하며 ID를 정의할 수 있다.
        {}: 그래프를 구성하는 요소들을 정의하는 부분 
        */
          graph { 
            a -- b;
          }
    
    ![img](images/example1.svg)


<a id="orgde300a8"></a>

### 예제 받아 출력

<table id="org026be02" border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<tbody>
<tr>
<td class="org-left">a</td>
<td class="org-left">Hello</td>
</tr>


<tr>
<td class="org-left">b</td>
<td class="org-left">World</td>
</tr>
</tbody>
</table>

위의 테이블을 다이어그램으로 변환한다.

    (mapcar `(lambda (x)
              (princ (format "%s [label =\"%s\", shape = \"box\"\];\n" 
                            (first x) (second x)))) table)
              (princ (format "%s -- %s;\n" 
                            (first (first table)) (first (second table))))

테이블을 graphviz 형식으로 변경하는 코드

    a [label ="Hello", shape = "box"];
    b [label ="World", shape = "box"];
    a -- b

변형의 결과값

    graph {
      $input
    }

입력 받은 형식을 통해 다이어그램 이미지를 생성한다.

![img](images/test-dot.png)

다이어그램 변환 결과

1.  dot 구문을 이용한 출력
    
        digraph G {
          my_start -> one_branch;
          my_start -> another_branch;
        }
    
    ![img](images/test-dot2.png)


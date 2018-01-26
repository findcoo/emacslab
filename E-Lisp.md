
# Table of Contents

1.  [E-Lisp](#org9fd0847)
    1.  [Text Editing](#org26a69bb)
        1.  [커서의 위치](#org4e74fbd)
        2.  [커서 이동 및 검색](#orgc5db74e)
        3.  [문자 삭제/삽입/변환](#org4cbdb2a)
        4.  [문자열](#orgc3aa55a)
        5.  [파일](#org3eb1dac)
        6.  [버퍼](#orge5bbc2c)
    2.  [좀 더 익혀야할 것들](#orgc30c6e3)
        1.  [Preserve Cursor Position](#org5b550b5)
        2.  [Grab Text from Buffer to String](#orgecbe236)
        3.  [Strings](#orgd4234fd)


<a id="org9fd0847"></a>

# E-Lisp

common lisp은 일반적인 프로그래밍 언어를 목표로 하기 때문에 elisp과는 상이한 점이 많다.
앞서 수의 체계에서도 알 수 있듯이 목표로하는 이점이 다르기 때문이다. 이제 부터는 elisp을 이용한 텍스트 편집에 중점을 두려한다.


<a id="org26a69bb"></a>

## Text Editing


<a id="org4e74fbd"></a>

### 커서의 위치


<a id="orgc5db74e"></a>

### 커서 이동 및 검색


<a id="org4cbdb2a"></a>

### 문자 삭제/삽입/변환


<a id="orgc3aa55a"></a>

### 문자열

    (length "abc")
    
    ;; a 이후 부터 e까지의 문자열 값
    (substring "abdefg" 1 4 )
    
    ;; 십진수 수들을 X로 변환한다.
    (replace-regexp-in-string "[0-9]" "X" "abc123")


<a id="org3eb1dac"></a>

### 파일


<a id="orge5bbc2c"></a>

### 버퍼


<a id="orgc30c6e3"></a>

## 좀 더 익혀야할 것들


<a id="org5b550b5"></a>

### Preserve Cursor Position

텍스트 편집에 있어 명령어 간에 커서 간섭으로 인해 커서가 예상하지 못한 곳으로 이동하는 것을 방지하기 위해
커서의 위치를 보존하는 함수를 사용한다.


<a id="orgecbe236"></a>

### Grab Text from Buffer to String

    ;; 이맥스 텍스트들은 특정 프로퍼티를 내포하고 있어서 문자를 추출할 때 프로퍼티를 제거하는 작업이 필요하다.
    (buffer-substring-no-properties 99 200)
    
    ;; 현재 커서의 단어를 반환
    (thing-at-point `word)
    
    ;; hyphen(-)과 underscore(_)를 포함하는 단어를 반환한다.
    (thing-at-point `symbol)
    
    ;; 현재 커서의 라인을 문자열로 반환
    (thing-at-point `line)
    
    ;; 단어의 시작과 끝의 위치값을 반환 
    (bounds-of-thing-at-point `word)


<a id="orgd4234fd"></a>

### Strings


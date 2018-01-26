
# Table of Contents

1.  [E-Lisp](#orgf39dd18)
    1.  [Text Editing](#orgc9fbb96)
        1.  [커서의 위치](#orge141a5f)
        2.  [커서 이동 및 검색](#org88ce7b9)
        3.  [문자 삭제/삽입/변환](#org7a918f7)
        4.  [문자열](#orgc4b0cc3)
        5.  [파일](#orgd8ddaad)
        6.  [버퍼](#org6c744da)
    2.  [좀 더 익혀야할 것들](#org8a51b6c)
        1.  [Preserve Cursor Position](#orga1e4cda)
        2.  [Grab Text from Buffer to String](#org473c005)
        3.  [Strings](#orgd47cd9d)


<a id="orgf39dd18"></a>

# E-Lisp

common lisp은 일반적인 프로그래밍 언어를 목표로 하기 때문에 elisp과는 상이한 점이 많다.
앞서 수의 체계에서도 알 수 있듯이 목표로하는 이점이 다르기 때문이다. 이제 부터는 elisp을 이용한 텍스트 편집에 중점을 두려한다.


<a id="orgc9fbb96"></a>

## Text Editing


<a id="orge141a5f"></a>

### 커서의 위치

    ;; 현재 커서의 위치값 왼쪽부터 시작된다.
    (point)
    
    ;; 선택된 영역의 커서 위치값
    (region-beginning)
    (region-end)
    
    ;; 현재 줄의 커서 위치값 
    (line-beginning-position)
    (line-end-position)
    
    ;; 현재 버퍼의 최소/최대 위치값
    (point-max)
    (point-min)


<a id="org88ce7b9"></a>

### 커서 이동 및 검색

    (goto-char 39)
    
    (forward-char 4)
    (backward-char 4)
    
    (search-forward "some")
    (search-forward "some")
    
    ;; 정규표현식을 이용한 검색
    (re-search-forward "[0-9]")
    (re-search-backward "[0-9")
    
    (skip-chars-forward "a-z")
    (skip-chars-backward "a-z")


<a id="org7a918f7"></a>

### 문자 삭제/삽입/변환

    (delete-char 9)
    (delete-region 3 10)
    
    (insert "hello")
    
    (setq x (buffer-substring 71 300))
    
    (capitalize-region 71 300)


<a id="orgc4b0cc3"></a>

### 문자열

    (length "abc")
    
    ;; a 이후 부터 e까지의 문자열 값
    (substring "abdefg" 1 4 )
    
    ;; 십진수 수들을 X로 변환한다.
    (replace-regexp-in-string "[0-9]" "X" "abc123")


<a id="orgd8ddaad"></a>

### 파일

    ;; 현재 버퍼에 해당 파일을 연다.
    (find-file "~/.spacemacs")
    
    ;; 현재 파일을 저장한다.
    (write-file path)
    
    ;; 현재 위치에 해당 파일의 내용을 입력한다. 
    ;; spacemacs 에서는 insert-file
    (insert-file-contents path)
    
    ;; 현재 버퍼에 내용을 해당 파일에 추가한다.
    (append-to-file start-pos end-pos path)
    
    (rename-file file-name new-name)
    (copy-file old-name new-name)
    (delete-file file-name)
    
    (file-name-directory full-path)
    (file-name-nondirectory full-path)
    (file-name-extenstion file-name)
    (file-name-sans-extension file-name)


<a id="org6c744da"></a>

### 버퍼

    (buffer-name)
    (buffer-file-name)
    
    ;; xyz 버퍼로 현재 버퍼를 변경한다.
    (set-buffer "xyz")
    
    (save-buffer)
    (kill-buffer "xyz")
    (with-current-buffer "xyz"
    ;; 해당 버퍼를 현재 작업 버퍼로 설정한다. 아래 부분에서 버퍼 편집에 관련된 작업들을 삽입한다.
    )


<a id="org8a51b6c"></a>

## 좀 더 익혀야할 것들


<a id="orga1e4cda"></a>

### Preserve Cursor Position

텍스트 편집에 있어 명령어 간에 커서 간섭으로 인해 커서가 예상하지 못한 곳으로 이동하는 것을 방지하기 위해
커서의 위치를 보존하는 함수를 사용한다.


<a id="org473c005"></a>

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


<a id="orgd47cd9d"></a>

### Strings


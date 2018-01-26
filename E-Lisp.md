
# Table of Contents

1.  [E-Lisp](#org9fa466e)
    1.  [Text Editing](#org00a3ea8)
        1.  [커서의 위치](#org499ebed)
        2.  [커서 이동 및 검색](#org905c06f)
        3.  [문자 삭제/삽입/변환](#org366a44e)
        4.  [문자열](#org92fe1f9)
        5.  [파일](#org5048822)
        6.  [버퍼](#orgfe87335)
    2.  [좀 더 익혀야할 것들](#org779a417)
        1.  [Preserve Cursor Position](#orga2cac90)
        2.  [Grab Text from Buffer to String](#org69b21df)
        3.  [Strings](#orgf15641b)


<a id="org9fa466e"></a>

# E-Lisp

common lisp은 일반적인 프로그래밍 언어를 목표로 하기 때문에 elisp과는 상이한 점이 많다.
앞서 수의 체계에서도 알 수 있듯이 목표로하는 이점이 다르기 때문이다. 이제 부터는 elisp을 이용한 텍스트 편집에 중점을 두려한다.


<a id="org00a3ea8"></a>

## Text Editing


<a id="org499ebed"></a>

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


<a id="org905c06f"></a>

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


<a id="org366a44e"></a>

### 문자 삭제/삽입/변환

    (delete-char 9)
    (delete-region 3 10)
    
    (insert "hello")
    
    (setq x (buffer-substring 71 300))
    
    (capitalize-region 71 300)


<a id="org92fe1f9"></a>

### 문자열

    (length "abc")
    
    ;; a 이후 부터 e까지의 문자열 값
    (substring "abdefg" 1 4 )
    
    ;; 십진수 수들을 X로 변환한다.
    (replace-regexp-in-string "[0-9]" "X" "abc123")


<a id="org5048822"></a>

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


<a id="orgfe87335"></a>

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


<a id="org779a417"></a>

## 좀 더 익혀야할 것들


<a id="orga2cac90"></a>

### Preserve Cursor Position

텍스트 편집에 있어 명령어 간에 커서 간섭으로 인해 커서가 예상하지 못한 곳으로 이동하는 것을 방지하기 위해
커서의 위치를 보존하는 함수를 사용한다.

    ;; point, mark, buffer을 고정한다.
    (save-excursion
    ;; 커서의 고정후 행위를 지정하는 영역.
    )
    
    ;; 사용자가 지정한 narrow 영역을 보존한다. narrow란 너무 긴 문서에서 특정 영역만을 선택하고 다른 영역을 제외함을 뜻한다.
    (save-restriction
      (narrow-to-region pos1 pos2)
      ;; 행위 영역
    )


<a id="org69b21df"></a>

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


<a id="orgf15641b"></a>

### Strings

    ;; 부분 문자열 추출
    (substring "abc" 1 2)
    
    ;; 문자열 합치기
    (concat "some" "thing")
    
    ;; 패턴 검증, 일치하는 문자의 갯수를 반환한다.
    (setq x "abc123")
    (string-match "\\(1\\)\\(2\\)" x)
    
    ;; 정규식 패턴에 일치한 문자를 반환한다. 첫번째 매개변수는 패턴의 인덱스다
    ;; 아래 예제에서 2는 (2) 정규식 패턴에 일치한 문자를 캡쳐하게된다.
    (match-string 2 x)
    
    ;; 정규식에 일치한 문자를 다른 문자로 변환한다.
    (replace-regexp-in-string "1" "2" x)
    
    ;; 문자열을 delimiter를 통해 분리하고 리스트로 반환한다.
    (listp (split-string "xy_007_cat" "_"))
    
    (string-to-number "3")
    (number-to-string 3)
    
    (setq testBuffer (buffer-string))
    (with-temp-buffer
      (insert testBuffer)
      (goto-char (point-min))
      ;; 작업 시작점
    
      ;; 임시 버퍼에 모든 문자열을 반환시킨다.
      (buffer-string)
    )


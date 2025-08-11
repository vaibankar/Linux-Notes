# Editors are used to create new files, and edit or modify the content inside it. Simply editors are used to read and write data in existing or newly created file. Editors can be classified on the basis of interfaces that they use, i.e. Graphical Editors and Command Line Editors.

# Graphical editor:
- Graphical editor uses graphical user interface. It is easy to use but consumes more memory than command line editors. In Linux, following are some well-known graphical editors.

1. gedit: - It is same as that of notepad in windows. You can open gedit graphically in application menu and also using command as $gedit.
2. kedit: - It is similar to gedit but contain some advance features. Generally, we have to install kedit separately to use it.
3. Open office: - Open Office is same as that of MS Office. This Open Office is specially developed for Linux based operating systems.

# Command line editor:
- Command line editor uses command line interface. These editors are much master and consumes less memory than any graphical editors. Following are some well-known command line editors.

1. nano: - nano editor is easy to use since it provides simple features to edit data from files.
      ```
      nano <filename>.<extension>
      ```
2. vi and vim: - vi (virtual interface) and vim (virtual interface modified) are most commonly used editors. vi and vim both editors are same where as vim is the                    advance version of vi editor. Thus, it contains some additional features. These editors works in four different modes.
   - Insert mode
   - Ex-mode
   - Command mode
   - Visual mode

     <img width="871" height="290" alt="image" src="https://github.com/user-attachments/assets/47d801ca-04ab-455b-a2e0-ecabd6c4837f" />
---
## Command Mode:- This is default mode. Press esc to exit from any mode and enter into command mode.
1. Delete current line = dd
2. Delete n no. of lines from current line = <n>dd
3. Delete current word = dw
4. Delete n no. of words from current word = <n>dw
5. Copy current line = yy
6. Copy n no. of lines from current line = <n>yy
7. Copy current word = yw
8. Copy n no. of words from current word = <n>yw
9. Cut current line and enter in insert mode = cc
10. Cut n no. of lines and enter in insert mode = <n>cc
11. Cut current word and enter in insert mode = cw
12. Cut n no. of words from current word and enter in insert mode = <n>cw
13. Paste = p
14. Remove current character and enter in insert mode = s
15. Remove current line and enter in insert mode = S
16. Undo = u
17. Redo = Ctrl+r
18. Move cursor to the top of screen = H
19. Move cursor to the middle of screen = M
20. Move cursor to the bottom of screen = L
21. Move cursor at the end of file = G
22. Move cursor at the beginning = gg
23. Move cursor at nth line = <n>gg
24. Search particular word/string/character = /<word>
25. Show next search result = n
26. Show previous search result = N
---
## Insert Mode:- Following are commands to enter in insert mode
1. insert text at current cursor position = i
2. insert text at start of the current line = I
3. insert text just right of the current character = a
4. insert text at end of the current line = A
5. insert new line below the current line = o
6. insert new line above the current line = O
7. it replaces single character = r
8. replace multiple characters = R
---
## Ex-mode:- special executing mode
1. quit without saving = :q
2. quit without saving forcefully = :q!
3. save and stay in file = :w
4. save and quit = :wq or :x
5. save and quit forcefully = :wq!
6. set line numbers = :set nu
7. Jump to nth line = :<n>
8. remove line numbers = :set nonu
9. Highlight word/string/character = :/<word>
10. Remove highlight = :nohl
11. Find and replace old word with new word = :%s/<old>/<new>/g
12. Execute any command on terminal without leaving editor = :!<command>
---
## Visual Mode:- this mode is used for selection.
1. Select character by character = v
2. Select line by line = V
3. Select block = ctrl+v
4. For copy, delete, and cut selected area = y,d,c





































Minibufexplorer with path patch
================================

.vimrc data for correct working
-------------------------
```
"Highlights
highlight link MBENormal Normal

"minibufexplorer options
map <Leader>b :MiniBufExplorer<cr>

"               To enable the optional mapping of Control + Vim Direction Keys
"               [hjkl] to window movement commands, you can put the following into
"               your .vimrc:
let g:miniBufExplMapWindowNavVim = 1
"
"               To enable the optional mapping of Control + Arrow Keys to window
"               movement commands, you can put the following into your .vimrc:
"
let g:miniBufExplMapWindowNavArrows = 1
"
"               To enable the optional mapping of <C-TAB> and <C-S-TAB> to a
"               function that will bring up the next or previous buffer in the
"               current window, you can put the following into your .vimrc:
"
let g:miniBufExplMapCTabSwitchBufs = 1
"
"               To enable the optional mapping of <C-TAB> and <C-S-TAB> to mappings
"               that will move to the next and previous (respectively) window, you
"               can put the following into your .vimrc:
"
let g:miniBufExplMapCTabSwitchWindows = 1

"
"delete the buffer; keep windows
"
function Kwbd(kwbdStage)
    if(a:kwbdStage == 1)
        let g:kwbdBufNum = bufnr("%")
        let g:kwbdWinNum = winnr()
        windo call Kwbd(2)
        execute "bd! " . g:kwbdBufNum
        execute "normal " . g:kwbdWinNum . ""
    else
        if(bufnr("%") == g:kwbdBufNum)
            let prevbufvar = bufnr("#")
            if(prevbufvar > 0 && buflisted(prevbufvar) && prevbufvar != g:kwbdBufNum)
                b #
            else
                bn
            endif
        endif
    endif
endfunction

" close buffer
imap <S-F4> <Esc>:call Kwbd(1)<CR>
nmap <S-F4> :call Kwbd(1)<CR>
```

# Belajar Vim 

## Daftar Isi
<!-- vim-markdown-toc GFM -->

  * [Instalasi](#instalasi)
  * [Berkas Konfigurasi](#berkas-konfigurasi)
    * [Vim](#vim)
    * [Neovim](#neovim)
  * [Manajemen Plugin](#manajemen-plugin)
    * [vim-plug](#vim-plug)
      * [Manual](#manual)
      * [Otomatis](#otomatis)
* [Navigasi (WIP)](#navigasi-wip)
* [Mapping (WIP)](#mapping-wip)
* [Kontribusi](#kontribusi)

<!-- vim-markdown-toc -->

## Instalasi

Umumnya `vim` sudah dibundle dengan sistem operasi yang distribusi beberbasi _Linux_ (_Archlinux,Ubuntu_) atau _Darwin_(_OSX_). Namun jika tidak tersedia, silahkan lakukan pemasangan dengan menggunakan _package manager_ yang kamu senangi.

## Berkas Konfigurasi

### Vim 
> terletak pada `~/.vimrc`
### Neovim
> terletak pada `~/.config/nvim/init.vim`

## Manajemen Plugin
### vim-plug
Untuk `vim-plug`, kamu hanya perlu mengambil berkas dari [Repository: junegunn/vim-plug](https://github.com/junegunn/vim-plug/blob/master/plug.vim?raw=true), lalu menyimpan berkas tersebut kedalam direktori `autoload`.
   
> Catatan: _autoload_ antara `Vim` dan `neovim` itu berbeda.
   
* `Vim`: ~/.vim/autoload
* `neovim`: ~/.local/share/nvim/site/autoload (:echo stdpath('data') . '/site/autoload')
   
#### Manual
1. Unduh dan simpan ke `autoload` direktori 
```shell
// pilih salah satu path dibawah ini 
// 1. neovim
> VIM_PLUG_FILE="~/.local/share/site/autoload/plug.vim"
// 2. Vim
> VIM_PLUG_FILE="~/.vim/autoload/plug.vim"
> curl -fLo $PLUG_FILE --create-dirs \
  https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```
2. Tambahkan fungsi dari `vim-plug` yang berguna untuk menulis daftar `plugin` yang kita gunakan pada berkas konfigurasi [vim](#vim) atau [neovim](#neovim) 
```viml
call plug#begin('~/.vim/plugged')
" kamu menulis setiap plugin yang kamu gunakan
" antara baris plug#begin dan plug#end
" formatnya Plug '<user|organization_name>/<plugin_name>'
" contoh (hapus doublequote atau kutip 2 pada baris dibawah ini)
" Plug 'sheerun/vim-polyglot' 
" setelah menuliskan nama plugin yang kamu gunakan 
" kamu perlu memuat ulang konfigurasi vim kamu dengan menjalankan 
" perintah berikut pada `vim` atau neovim
" :source $MYVIMRC
" lalu menjalankan 
" :PlugInstall
" silahkan baca didokumentasi vim-plug untuk lebih lengkap mengenai command-nya
call plug#end()
3. Selesai
```

#### Otomatis
1. Tambahkan [fungsi berikut](https://github.com/ri7nz/.dotifiles/commit/cdc6b84c376722ce88a3c96342e56d737e4e2ee2#diff-7b703895bd6083d95820fd09acf991e47e2a9dc7822d0dbfdb54d7f4486eb1afR5-R29) pada berkas konfigurasi [vim](#vim) atau [neovim](#neovim) 
```viml
"""
" @usage
" call s:InitPluginManager()
" @return {string} plugged path
"
" autoload vim-plug 
"""
func! s:InitPluginManager()
  if has('nvim')
    let l:vim_plug_file = stdpath('data') . '/site/autoload/plug.vim'
  else
    let l:vim_plug_file = '~/.vim/autoload/plug.vim'
  endif
  " when vim-plug aka {plug.vim} NOT exist in autoload path
  " download file from {https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim}
  if empty(glob(vim_plug_file))
      echo "installing vim-plug..."
      let l:vim_plug_raw = 'https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
      silent! execute "!curl -fLo " .vim_plug_file. " --create-dirs " . vim_plug_raw
      autocmd VimEnter * PlugInstall --sync | source $MYVIMRC
      echo "vim-plug installed!"
  endif
endfunc
" call InitPluginManager only for this file
call s:InitPluginManager()
call plug#begin('~/.vim/plugged')
" tambahkan plugin kamu disini
" formatnya Plug '<user|organization_name>/<plugin_name>'
call plug#end()
```
2. muat ulang konfigurasi vim atau neovim kamu `:source $MYVIMRC`
3. tunggu sampai selesai dan selesai
 
# Navigasi (WIP)
# Mapping (WIP)
# Kontribusi

Kamu bebas memberikan apapun, kritik, saran, atau meminta sesuatu (semoga bisa dibantu) 


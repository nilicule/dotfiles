#
# ~/.zshrc for Remco Brink <remco@rc6.org>
#
# This is a compilation of a whole bunch of .zshrc
# files out there.
#
# Original version by Jesper Noehr <jesper@noehr.org>
# 
# ChangeLog:
#   20070117 - Cleaned up file a bit
#              Kill now lists all procs in a colourful menu
#              Added bash/restart/profile/reload functions
#   20051101 - Fixed prompt problems and screen responsiveness,
#              fixed title support (remco@rc6.org)
#   20050507 - Added duh
#
# Grab whatever you want -- I couldn't care less.
#

zshrc_load_status () {
   #echo -n "\r.zshrc load: $* ... \e[0K"
}

zshrc_load_status 'startup'

# Prompt ala my famous prompt from tcsh.
if test $SSH_CLIENT; then 
    # PROMPT="[%B%n%b@%B%u%m%b(%BSSH%b): %B%~%b]%(#.#.>) "
    # PROMPT="[%B%n%b@%B%u%m%b(%BSSH%b):%B%~%b]%(#.#.) "
    PROMPT="[%B%n%b@%B%u%m%b:%B%~%b]%(#.#.) "
else 
    # PROMPT="[%B%u%m%b/%B%n%b] %B%~%b %(#.#.>) "
    PROMPT="[%B%u%m%b/%B%n%b]%B%~%b %(#.#.) "
fi

# The prompt used for spelling correction. The sequence `%R' expands to
# the string which presumably needs spelling correction, and `%r' expands
# to the proposed correction. All other prompt escapes are also allowed.
SPROMPT=$'%BError!%b Correct %{\e[31m%}%R%{ \e[0m%}to%{ \e[36m%}%r%{ \e[0m%}? [No/Yes/Abort/Edit]: '

# ZFTP is an ftp client built right in to zsh. *Very* neat.
  if [[ $ZSH_VERSION > '4.2' ]]; then
  autoload  zfinit ; zfinit
  # Emailaddress for anonymous-session
  (( ${+EMAIL_ADDR} )) || export EMAIL_ADDR="anonftp@strcat.de"
  # A `G' for a get operation and a `P' for a put operation.
  ZFTP_TRANSFER=yes
  # Default is a reverse progressbar but its very ugly *narf*
  # Valid options are ``none'', ``bar'' and ``percent''.
  zstyle ':zftp:*' progress percent 
  # Specifies the minimum time interval between updates of the
  # progress meters in seconds
  zstyle ':zftp:*' update true
  # If set to ``1'', ``yes'' or ``true'', filename generation
  # (globbing) is performed on the remote maschine instead of
  # zsh itself. Hell no!!!11!
  zstyle ':zftp:*' remote-glob false
  fi

zshrc_load_status 'normal stuff'

# Nano, of course.
EDITOR="nano"
export EDITOR

# Start emacs in console-mode.
#alias emacs="emacs -nw"

## Someone once accused zsh of not being as complete as Emacs, because it
## lacks Tetris and an adventure game.
autoload -U tetris
zle -N tetris
bindkey "^Xt" tetris ## C-x-t to play

## watch for my friends
## An array (colon-separated list) of login/logout events to report.
## If it contains the single word `all', then all login/logout events
## are reported.  If it contains the single word `notme', then all
## events are reported as with `all' except $USERNAME.
## An entry in this list may consist of a username,
## an `@' followed by a remote hostname,
## and a `%' followed by a line (tty).
#watch=( $(<~/.friends) )  ## watch for people in $HOME/.friends file
watch=(notme)  ## watch for everybody but me
LOGCHECK=60  ## check every ... seconds for login/logout activity

## The format of login/logout reports if the watch parameter is set.
## Default is `%n has %a %l from %m'.
## Recognizes the following escape sequences:
## %n = name of the user that logged in/out.
## %a = observed action, i.e. "logged on" or "logged off".
## %l = line (tty) the user is logged in on.
## %M = full hostname of the remote host.
## %m = hostname up to the first `.'.
## %t or %@ = time, in 12-hour, am/pm format.
## %w = date in `day-dd' format.
## %W = date in `mm/dd/yy' format.
## %D = date in `yy-mm-dd' format.
# WATCHFMT='%n %a %l from %m at %t.'
WATCHFMT="%n from %M has %a tty%l at %T %W"

if (( EUID == 0 )); then
    umask 022
fi

# Historyfile.
HISTSIZE=200
SAVEHIST=200
HISTFILE=~/.zsh_history

# Use less for pager.
PAGER=less

zshrc_load_status 'options'

# Some options
setopt correct
# Who would've thought this would break almost every friggin loadable module?
#setopt cshjunkiequotes
setopt interactivecomments
setopt noclobber
setopt sunkeyboardhack
setopt extendedglob
setopt nobeep # beeping is annoying.
setopt nohup  # don't kill background-jobs upon logout
setopt listpacked
setopt nolisttypes
setopt completeinword
unsetopt promptcr # Fixes problems in screen

zshrc_load_status 'limits'

# Limits.
unlimit
limit stack 8192
limit core 0 # No coredumps.
limit -s

zshrc_load_status 'aliases'

# colors for ls, etc.
#eval `dircolors -b /etc/DIR_COLORS`

# Shell functions.
#setenv() { typeset -x "${1}${1:+=}${(@)argv[2,$#]}" }

# Add some folders to our function path
fpath=(~/.zsh $fpath)

# Search path for cd.
#cdpath=(.. ~)

manpath=($X11HOME/man /usr/man /usr/lang/man /usr/local/man /usr/share/man)
export MANPATH

PATH=$PATH:/home/flow/bin:/usr/local/bin
export PATH

export LESS=-cx3M

#
# Completion tweaking
#

zshrc_load_status 'zstyles'

# Match uppercase from lowercase
    zstyle ':completion:*' matcher-list 'm:{a-z}={A-Z}'

# Pretty menu!
    zstyle ':completion:*' menu select=1
    #zstyle ':completion:*:scp:*' menu yes select

# Process completion
    #zstyle ':completion:*:*:kill:*' menu yes select
    #zstyle ':completion:*:kill:*' force-list always
    zstyle ':completion:*:processes' command 'ps -au$USER'
    zstyle ':completion:*:*:*:*:processes' menu yes select
    zstyle ':completion:*:*:*:*:processes' force-list always
    zstyle ':completion:*:*:kill:*:processes' list-colors '=(#b) #([0-9]#)*=0=01;31'

# User completion
    zstyle ':completion:*' users $users

# Some patterns to ignore
    zstyle ':completion:*:functions' ignored-patterns '_*'
    zstyle ':completion:*:(all-|)files' ignored-patterns '(|*/)CVS'
    zstyle ':completion:*:cd:*' ignored-patterns '(*/)#CVS'
    zstyle ':completion:*:*:(^rm):*:*files' ignored-patterns '*?.o' '*?.c~' '?*.old'

# Host completion (code by bkhl)
    if [[ -f ~/.ssh/known_hosts ]]; then
        _etchosts=(${(s: :)${(ps:\t:)${${(f)"$(</etc/hosts)"}%%\#*}##[:blank:]#[^[:blank:]]#}})
        _sshhosts=(${${${${(f)"$(<~/.ssh/known_hosts)"}:#[0-9]*}%%\ *}%%,*})
        _myhosts=($_etchosts $_sshhosts)
        zstyle ':completion:*' hosts $_myhosts
    fi

# Ignore line with rm
    zstyle ':completion:*:rm:*' ignore-line yes

# Add colors to completions
    zstyle ':completion:*' list-colors ${(s.:.)LS_COLORS}

# Enable caching
    zstyle ':completion::complete:*' use-cache 1
    zstyle ':completion::complete:*' cache-path ~/.zsh/cache/$HOST

# To force zsh to realize new commands
    #zstyle ':completion:*' completer _oldlist _expand _force_rehash _complete

zshrc_load_status 'modules'

zmodload zsh/complist
autoload zcalc

# Note: cshjunkiequotes totally f*cked this up. Do *not* use 'em!
autoload -U colors
autoload -U compinit promptinit
autoload -U zmv
compinit -C
#promptinit; prompt gentoo
colors

# Sweet trick from zshwiki.org :-)
cd () {
  if (( $# != 1 )); then
    builtin cd "$@"
    return
  fi

  if [[ -f "$1" ]]; then
    builtin cd "$1:h"
  else
    builtin cd "$1"
  fi
}

if [[ $TERM == tgtelnet ]]; then
    echo
else
    echo -n "\r"
fi

zshrc_load_status 'title status'

##
# Functions
##

# Restarting zsh or bash; reloading .zshrc or functions
TRAPUSR2() {
  [ -f ~/.sh-sourceall ] && . ~/.sh-sourceall
}

_force_rehash() {
  (( CURRENT == 1 )) && rehash
  return 1	# Because we didn't really complete anything
}

bash () {
  NO_ZSH="yes" command bash "$@"
}

restart () {
  exec $SHELL "$@"
}

profile () {
  ZSH_PROFILE_RC=1 $SHELL "$@"
}

reload () {
  if [[ "$#*" -eq 0 ]]; then
    . ~/.zshrc
  else
    local fn
    for fn in "$@"; do
      unfunction $fn
      autoload -U $fn
    done
  fi
}
compdef _functions reload

### zurl()        create small urls via tinyurl.com {{{
###   needs wget, grep and sed. yes, it's a hack ;)
function zurl() {
  [[ -z ${1} ]] && print "please give an url to shrink." && return 1
  local url=${1}
  local tiny="http://tinyurl.com/create.php?url="
  #print "${tiny}${url}" ; return
  wget  -O-             \
        -o/dev/null     \
        "${tiny}${url}" \
    | grep -Eio 'value="(http://tinyurl.com/.*)"' \
    | sed 's/value=//;s/"//g'
}

## Bzip2 all files and directories given on the command line.
pack(){
  if [[ $# -le 0 ]]; then
    echo "Usage: $0 <files or directories>";
    return 1;
  fi

  integer i;
  for ((i=1; i <= $#; i++)); do
    # Be extra paranoid and remove all slashes.  Since we can run 'rm -rf' from
    # this function, make us cd to the directory and execute it there.
    local entry=${argv[i]//\//};

    # If it is already compressed, don't bother recompressing.
    # This means match any of the extensions at the end of the name.
    # Make sure it is a file or directory and not a symlink.
    if [ -h "${entry}" ]; then
      echo "Skipping \"${entry}\" because it is a symlink."
    else
      if [ -f "${entry}" ]; then
        # Convert it to lower case, and then check the entry extension.
        if [ -z ${${(L)entry}//%*.(gz|bz2|zip|tgz|tbz)/} ]; then
          echo "Skipping \"${entry}\" because it is already compressed"
        else
          bzip2 -9 -v "${entry}"
        fi
      elif [ -d "${entry}" ]; then
        if [ -f "${entry}.tar.bz2" ]; then
          echo "Error: File \"${entry}.tar.bz2\" already exists!"
        else
          echo "Compressing directory ${entry}"
          # rm with ./ to make sure we aren't accidentally doing /.
          # rm with -- to avoid problems with 'rm *' where there is a file
          # named -r.
          tar -cvpf "${entry}.tar" "${entry}/" && bzip2 -9 -v "${entry}.tar" \
              && rm -rf -- ./"${entry}"
        fi 
      else
        echo "Skipping \"${entry}\" because it is not a file or directory."
      fi
    fi
  done
}

# generate thumbnails ;)
function genthumbs ()
{
    rm -rf thumb-* index.html
    echo "
<html>
  <head>
    <title>Images</title>
  </head>
  <body>" > index.html
    for f in *.(gif|jpeg|jpg|png)
    do
        convert -size 100x200 "$f" -resize 100x200 thumb-"$f"
        echo "    <a href=\"$f\"><img src=\"thumb-$f\"></a>" >> index.html
    done
    echo "
  </body>
</html>" >> index.html
}

# display some informations
function status()
{
  local system="$(cat /etc/[A-Za-z]*[_-][rv]e[lr]*)"
  print ""
  print "Date..: "$(date "+%Y-%m-%d %H:%M:%S")""
  print "Shell.: Zsh $ZSH_VERSION (PID = $$, $SHLVL nests)"
  print "Term..: $TTY ($TERM), $BAUD bauds, $COLUMNS x $LINES cars"
  print "Login.: $LOGNAME (UID = $EUID) on $HOST"
  print "System: $system"
  print "Uptime:$(uptime)"
  print ""
}

# Usage: simple-extract <file>
# Description: extracts archived files (maybe)
simple-extract () 
{
        if [[ -f "$1" ]]
        then
                case "$1" in
                        *.tar.bz2)  bzip2 -v -d "$1" ;;
                        *.tar.gz)   tar -xvzf "$1"   ;;
                        *.ace)      unace e "$1"     ;;
                        *.rar)      unrar x "$1"     ;;
                        *.deb)      ar -x "$1"       ;;
                        *.bz2)      bzip2 -d "$1"    ;;
                        *.lzh)      lha x "$1"       ;;
                        *.gz)       gunzip -d "$1"   ;;
                        *.tar)      tar -xvf "$1"    ;;
                        *.tgz)      gunzip -d "$1"   ;;
                        *.tbz2)     tar -jxvf "$1"   ;;
                        *.zip)      unzip "$1"       ;;
                        *.Z)        uncompress "$1"  ;;
                        *.shar)     sh "$1"          ;;
                        *)          echo "'"$1"' Error. Please go away" ;;
                esac
        else
                echo "'"$1"' is not a valid file"
        fi
}

# Usage: smartcompress <file> (<type>)
# Description: compresses files or a directory.  Defaults to tar.gz
smartcompress()
{
if [ '$2' ]; then
case '$2' in
tgz | tar.gz)   tar -zcvf$1.$2 '$1' ;;
tbz2 | tar.bz2) tar -jcvf$1.$2 '$1' ;;
                        tar.Z)          tar -Zcvf$1.$2 '$1' ;;
                        tar)            tar -cvf$1.$2  '$1' ;;
                        gz | gzip)      gzip           '$1' ;;
                        bz2 | bzip2)    bzip2          '$1' ;;
*)
echo "Error: $2 is not a valid compression type"
                        ;;
esac
else
smartcompress '$1' tar.gz
fi
}

# Usage: show-archive <archive>
# Description: view archive without unpack
show-archive()
{
        if [[ -f $1 ]]
        then
                case $1 in
                        *.tar.gz)      gunzip -c $1 | tar -tf - -- ;;
                        *.tar)         tar -tf $1 ;;
                        *.tgz)         tar -ztf $1 ;;
                        *.zip)         unzip -l $1 ;;
                        *.bz2)         bzless $1 ;;
                        *)             echo "'$1' Error. Please go away" ;;
                esac
        else
                echo "'$1' is not a valid archive"
        fi
}

# Shows latest kernel versions
function kernel()
{
printf 'GET /kdist/finger_banner HTTP1.0\n\n' | nc www.kernel.org 80 | grep latest
}

function http_header()
{
       # This is zsh but still no gnu echoism ;P
       if [[ $2 != "" ]] { port=$2 } else { port=80 }
       if [[ $3 != "" ]] { vhost="$3" } else { vhost=$1 }
 
       printf "HEAD /$4 HTTP/1.1\\nHost: $vhost\nConnection: close\n\n" \
        | nc $1 $port
}

lsperm () {
  echo $1 | perl -e 'chomp($s=<>);$p=(stat($s))[2] & 07777;printf "$s -> %04o\n",$p'
}

# du with depth 1
duh () {
    du "$@" | egrep -v '/.*/'
}
## Invoke this every time when u change .zshrc to
## recompile it.
src ()
{
    autoload -U zrecompile
    [ -f ~/.zshrc ] && zrecompile -p ~/.zshrc
    [ -f ~/.zcompdump ] && zrecompile -p ~/.zcompdump
    [ -f ~/.zshrc.zwc.old ] && rm -f ~/.zshrc.zwc.old
    [ -f ~/.zcompdump.zwc.old ] && rm -f ~/.zcompdump.zwc.old
    source ~/.zshrc
}

## find process to kill and kill it.
pskill ()
{ 
	local pid
	pid=$(ps -ax | grep $1 | grep -v grep | awk '{ print $1 }')
	echo -n "killing $1 (process $pid)..."
	kill -9 $=pid
	echo "slaughtered."
}

function title {
    if [[ $TERM == "screen" ]]; then
      # Use these two for GNU Screen:
      print -nR $'\033k'$1$'\033'\\\

      print -nR $'\033]0;'$2$'\a'
    elif [[ $TERM == "xterm" || $TERM == "rxvt" ]]; then
      # Use this one instead for XTerms:
      print -nR $'\033]0;'$*$'\a'
    fi
}

function precmd {
    title zsh "$PWD"

}

function dirsize()
{
	if [ -z $1 ]; then
		dir="."
	else
		dir=$1
	fi
	find $dir -type d -maxdepth 1 -mindepth 1 -exec du -sh '{}' \; 2>/dev/null \
	| perl -pe "s/\t.*\/(.*)$/\t$(echo '\033[01;32m')\1$(echo '\033[0m')/gi" 
	echo
	echo "Total: " $(du -sh $dir 2>/dev/null | awk '{print $1}')
}

# find process and kill it
morons() { reply=(`ps ax | grep -v COMMAND |perl -nle '@a=split(" ",$_,9);$_=$a[4];s/[()]//g;s/.*\///g;print'`) }
compctl -K morons pskill pkill
pskill()
{
        local signal="HUP"
        if [[ $1 == "" || $3 != "" ]]; then
                print "Usage: $0 processname [signal]" && return 1
        fi
        [[ $2 != "" ]] && signal=$2
        set -A pids $(command ps wwaux | grep $1 | grep -v "grep $1" | awk '{ print $2 }')
        if [[ ${#pids} -lt 1 ]]; then
                print "No matching processes for »$1«" && return 1
        fi
        if [[ ${#pids} -gt 1 ]]; then
                print "${#pids} processes matched: $pids"
                read -q "?Kill all? [y/n] " || return 0
        fi
        if kill -$signal $pids; then
                echo "Killed $1 pid $pids with SIG$signal"
        fi
}

# Show days since given birthday
function days () 
{
	if [ "$*" = "" ]; then
		echo "Use $0 day month year"
		echo "Example: $0 "12 aug 1999""
	else
		BIRTHDAY="$*"
		print $(( (`date +%s -d ${2:="now"}` - `date +%s -d ${1:=$BIRTHDAY}` )/60/60/24 ))
	fi
}

# Exchange ' ' for '_' in filenames.
unspaceit()
{
        for _spaced in "${@:+"$@"}"; do
                if [ ! -f "${_spaced}" ]; then
                        continue;
                fi
                _underscored=$(echo ${_spaced} | tr ' ' '_');
                if [ "${_underscored}" != "${_spaced}" ]; then
                        mv "${_spaced}" "${_underscored}";
                fi
        done
}

function preexec {
    emulate -L zsh
    local -a cmd; cmd=(${(z)1})
    title $cmd[1]:t "$cmd[2,-1]"
}

## make screenshot of current desktop (use import from ImageMagic)
sshot ()
{ sleep 5; import -window root `date "+%d-%m-%Y--%H:%M:%S"`.jpg }

## display processes tree in less
pst ()
{ pstree -p $* | less -S }

function svnu {
exec svn update "$@" 2>&1 \
| awk '/^C | conflicts /                  { print "\033[1;31m" $0"\033[0m"; next }
/svn update/                       { print "\033[0;32m" $0"\033[0m"; next }
/^\? /                             { print "\033[0;33m" $0"\033[0m"; next }
/^A /                              { print "\033[1;33m" $0"\033[0m"; next }
/^N /                              { print "\033[1;33m" $0"\033[0m"; next } # import
/^R /                              { print "\033[0;35m" $0"\033[0m"; next }
/^P /                              { print "\033[0;36m" $0"\033[0m"; next }
/^Merging differences /            { print "\033[0;36m" $0"\033[0m"; next }
/already contains the differences/ { print "\033[0;36m" $0"\033[0m"; next }
/^U /                              { print "\033[1;32m" $0"\033[0m"; next }
/^M /                              { print "\033[0;34m" $0"\033[0m"; next }
/^(RCS file: |retrieving |done$)/  { print "\033[1;32m" $0"\033[0m"; next }
/not .* pertinent/                 { print "\033[0;1m"  $0"\033[0m"; next }

# Nothing should reach here
{ print "\033[1;35m" $0 }

END { printf "\033[0m" }'
}

function svna {
exec svn add "$@" 2>&1 \
| awk '/^C | conflicts /                  { print "\033[1;31m" $0"\033[0m"; next }
/svn update/                       { print "\033[0;32m" $0"\033[0m"; next }
/^\? /                             { print "\033[0;33m" $0"\033[0m"; next }
/^A /                              { print "\033[1;33m" $0"\033[0m"; next }
/^N /                              { print "\033[1;33m" $0"\033[0m"; next } # import
/^R /                              { print "\033[0;35m" $0"\033[0m"; next }
/^P /                              { print "\033[0;36m" $0"\033[0m"; next }
/^Merging differences /            { print "\033[0;36m" $0"\033[0m"; next }
/already contains the differences/ { print "\033[0;36m" $0"\033[0m"; next }
/^U /                              { print "\033[1;32m" $0"\033[0m"; next }
/^M /                              { print "\033[0;34m" $0"\033[0m"; next }
/^(RCS file: |retrieving |done$)/  { print "\033[1;32m" $0"\033[0m"; next }
/not .* pertinent/                 { print "\033[0;1m"  $0"\033[0m"; next }

# Nothing should reach here
{ print "\033[1;35m" $0 }

END { printf "\033[0m" }'
}

function svnl {
    svn log $*
}

# Give us a root shell, or run the command with sudo.
# Expands command aliases first (cool!)
smart_sudo () {
    if [[ -n $1 ]]; then
        #test if the first parameter is a alias
        if [[ -n $aliases[$1] ]]; then
            #if so, substitute the real command
            sudo ${=aliases[$1]} $argv[2,-1]
        else
            #else just run sudo as is
            sudo $argv
        fi
    else
        #if no parameters were given, then assume we want a root shell
        sudo -s
    fi
}
alias s=smart_sudo
compdef _sudo smart_sudo

##
# Included files
##

# Key bindings
source ~/.zshrc-bindings

# Make sure we start some programs
source ~/.zshrc-startup

# Load our aliases
source ~/.zshrc-aliases

# If available, load host specific stuff
if [ -f ~/.zshrc.`hostname` ]; then
    source ~/.zshrc.`hostname`
fi

return 0

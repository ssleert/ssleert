<div align="center">

### *`sfome`*
#### *zstd compressed mind*
  
Hello there and I haven't decided what I am yet. <br>
But I'm good at writing scripts, cli utilities and infrastructure tools, <br> 
as well as setting up work and dev environments. Also interested in learning useless stuff <br> 
like `nim`, `zig` and `bash`. <br>
<br>
You can also check some of my repositories and you probably won't find anything useful. <br>
I write mostly in `Go` and `sh` at the moment. <br>

<br>
</div>

<details>
<summary align="center">some of my code examples</summary>

### `GetChar()` from sterm
```go
// simple func to get char from terminal
// similar to getchar() in C
func GetChar() (rune, error) {
	s, err := term.MakeRaw(0)
	defer term.Restore(0, s)
	if err != nil {
		return 0, err
	}

	in := bufio.NewReader(os.Stdin)

	rn, _, err := in.ReadRune()
	if err != nil {
		return 0, err
	}

	return rn, nil
}
```

<br>
  
### `2arr()` from pblib
#### splits string to characters with '\n' delimiter
```bash
function pblib::str::2arr() {
  local -r string="$1"
  shift $#

  if [[ -z $string ]]; then
    return 1
  else
    local -a array
    local char
    for (( i = 0; i < ${#string}; ++i )); do
      char="${string:${i}:1}"
      if [[ -z $char ]]; then
        array+=(' ')
      else
        array+=("${char}")
      fi
    done
    unset char
    readonly array
    printf '%s\n' "${array[@]}"
    return 0
  fi
}
```

<br>

### `lines_while()` from pblib
#### count lines in file with while cycle
```bash
function pblib::fs::lines_while() {
  local -r file="$1"
  shift $#

  if [[ ! -f $file ]]; then
    return 1
  else
    local -i lines_count=0
    while IFS='' read -r _; do
      ((++lines_count))
    done < "${file}"
    readonly lines_count
    printf '%u\n' "${lines_count}"
    return 0
  fi
}
```

<br>

### `ReadLines()` from sfolib
### read N lines from file
```go
// read N lines from file
func ReadLines(s string, n int) ([]string, error) {
	f, err := os.Open(s)
	if err != nil {
		return nil, err
	}
	defer f.Close()

	lines := make([]string, 0, n)
	sc := bufio.NewScanner(f)
	for i := 0; i < n && sc.Scan(); i++ {
		lines = append(lines, sc.Text())
	}

	return lines, nil
}
```

</details>

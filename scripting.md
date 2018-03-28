# Scripting

## helpful log function with date/time
```
log() {
  # parameter $@ is every parameter passed in
  dt=$(date +"%Y-%m-$d:%H%M%S")
  echo -e "$dt: $@
}
```

## run script in loop
```
while true; do <command> ; done
```

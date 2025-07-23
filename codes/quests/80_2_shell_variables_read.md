# 인자와 read를 함께 사용하여 변수 조합 출력

### ~$ 80_2_shell_variables_read.sh agument_first
### read input : read_first
### 
### input values : agument_first read_first



```shell
# 셸 스크립트

#!/bin/bash

V_FIRST_INPUT="$1"

read -p "input: " V_READ_INPUT

echo "$V_FIRST_INPUT, $V_READ_INPUT"
```

```shell
# 실행
[skp@localhost ~/quests]$ ./80_2_shell_variables_read.sh aaa
input: bbb
aaa, bbb
```
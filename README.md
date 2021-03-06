# Mazefuck

Mazefuck은 Brainfuck과 Befunge에서 영감을 받은 언어로 Brainfuck의 커맨드가 총 8개인 점에서 이진수 세 자리로 표현 가능하다는 점과 Befunge처럼 미로와 같은 형태에서 명령을 전달할 수 있다는 점에 착안했다.

Mazefuck은 Brainfuck과 같이 `0`으로 초기화된 30000바이트의 배열과 배열의 첫 바이트를 가리키는 포인터를 사용한다. 또한 미로의 최단 탈출 경로를 커맨드로 사용하며 좌회전을 `0`, 우회전을 `1`로 치환해 명령을 조합한다. 만약 최단 탈출 경로가 여러개라면 (오른쪽, 왼쪽, 아래, 위) 를 우선순위로 내림차순 정렬했을 때 가장 먼저오는 경로를 최단 경로로 생각한다. 예를 들어 경로가 (오른쪽, 아래, 아래 왼쪽) 인 경우와 (왼쪽, 아래, 아래, 오른쪽) 인 경우가 있을 때 오른쪽이 왼쪽보다 우선순위가 높으므로 (오른쪽, 아래, 아래, 왼쪽)을 최단 경로로 계산한다. 미로의 가장자리는 통과할 수 없다.

| BrainFuck | MazeFuck | 의미                                                         |
| --------- | -------- | ------------------------------------------------------------ |
| `>`       | `000`    | 포인터를 오른쪽으로 움직인다                                 |
| `<`       | `001`    | 포인터를 왼쪽으로 움직인다                                   |
| `+`       | `010`    | 포인터가 가리키는 바이트의 값을 증가시킨다                   |
| `-`       | `011`    | 포인터가 가리키는 바이트의 값을 감소시킨다                   |
| `.`       | `100`    | 포인터가 가리키는 바이트의 값을 ASCII 문자로 출력한다        |
| `,`       | `101`    | Input a character and store it in  the cell at the pointer   |
| `[`       | `110`    | 포인터가 가리키는 바이트의 값이 `0`이면 뒤쪽의 `]` 또는 `111`로 이동한다 |
| `]`       | `111`    | 포인터가 가리키는 바이트의 값이 `0`이 아니면 앞쪽의 `[` 또는 `110`으로 이동한다 |

미로는 총 4개의 문자로 구성되며 직사각형 모형이어야 한다. 또한 첫 번째 줄에 시작점을 나타내는 문자, 끝점을 나타내는 문자, 빈칸을 나타내는 문자를 하나씩 순서대로 입력해야 한다.

## Usage

* `Mazefuck` 은 Mazefuck 파일을 바로 실행시킬 때 사용한다.
  * `./Mazefuck file_name`
    * `./Mazefuck 42.bf`
* `Brainfuck_To_Mazefuck` 은 Brainfuck 파일을 Mazefuck 파일로 바꿔준다.
  * `./Brainfuck_To_Mazefuck character_set file_name`
    * `character_set`은 Mazefuck에서 사용할 시작 지점 문자, 종료 지점 문자, 벽 문자, 빈 공간 문자가 공백 없이 이어진 문장이다.
    * `./Brainfuck_To_Mazefuck "^$+ " 42.bf`

## Examples

* 다음은 숫자 42를 출력하는 Mazefuck 코드이다.

  ```mf
  ^$ 
  +++++++++++++++++++++++++++++++++++++++++
  ++++                                  +++
  ++++ ++++++++++++++++++++++++++++++++ +++
  ++++ +                              + +++
  ++++ + ++++++++++++++++++++++++++++ + +++
  ++++ + ++                        ++ + +++
  ++++ + ++ ++++++++++++++++++++++ ++ + +++
  ++++ + +  ++                  ++  + + +++
  ++++ + + +   ++++++++++++++++   + + + +++
  ++++ + + + ++++++++++++++++++++ + + + +++
  ++++ + + + ++                 + + + + +++
  ++++ + + + ++ +++++++++++++++ + + + + +++
  ++++ + + + ++ +             + + + + + +++
  ++++ + + + ++ + +++++++++++ + + + + + +++
  ++++ + + + ++ + ++++    +++ + + + + + +++
  ++++ + + + ++ + ++++ ++ +++ + + + + + +++
  ++++ + + + ++ + ++++  +  ++ + + + + + +++
  ++++ + + + ++ + +$ ++ ++ ++ + + + + + +++
  ++++ + + + ++ + ++ ++ ++ ++ + + + + + +++
  ++++ + + + ++ + +  +  ++  + + + + + + +++
  ++++ + + + ++ + + ++ ++++ + + + + + + +++
  ++++ + + + ++ + +    ++++ + + + + + + +++
  ++++ + + + ++ + +++++++++ + + + + + + +++
  ++++ + + + ++ +      +++  + + + + + + +++
  ++++ + + + ++ ++++++     ++ + + + + + +++
  ++++ + + + ++ +++++++++++++ + + + + + +++
  ++++ + + + ++ +             + + + + + +++
  ++++ + + + ++ + +++++++++++++ + + + + +++
  ++++ + + + +  +               + + + + +++
  ++++ + + +   ++++++++++++++++++ + + + +++
  ++++ + +  +++++++++++++++++++   + + + +++
  ++++ + ++                     ++  + + +++
  ++++ + +++++++++++++++++++++++++ ++ + +++
  ++++ +                           ++ + +++
  ++++ ++++++++++++++++++++++++++++++ + +++
  +^+  +                              +   +
  + + ++ ++++++++++++++++++++++++++++++++ +
  + + ++                              +++ +
  + + +++++++++++++++++++++++++++++++   + +
  + + +++++++++++++++++++++++++++++++++ + +
  + +  ++++++++++++++++++++++++++++++   + +
  + ++                                +++ +
  +   +++++++++++++++++++++++++++++++++   +
  +++                                   +++
  +++++++++++++++++++++++++++++++++++++++++
  ```

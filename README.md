<p align="center">
  <img src="https://i.ibb.co/41pL50L/Group-1.png" width="400" alt="logo">
</p>
<p align="center">
  <img src="https://img.shields.io/badge/version-1.0.0-b.svg" alt="version">
</p>

### About
Cross-platform flexible library for your CLI applications.

### Features
- Cross-platform: macOS, Linux, Windows.
- Writing your own autocomplete rules.
- Setting your own highlight colors.
- Required C++17.

### Config Example
1. After `git` may follow: `config`, `init`, `clone`.
2. After `config` may follow: `--global`, `user.name`, `user.email`.
3. After `--global` may follow: `user.name`, `user.email`.
4. After `user.name` may follow optional value: `"[name]"`.
5. ...
```
git
    config
        --global
            user.name
                "[name]"
            user.email
                "[email]"
        user.name
            "[name]"
        user.email
            "[email]"
    init
        [repository name]
    clone
        [url]
```

### Simple Example
> More complex example with: `color settings`, `handling optional values` and `line title configuration` [you will find here.](example/main.cpp)
```cpp
#include <iostream>
#include <string>

#include "../include/autocomplete.h"

int main() {
    std::string config_file_path = "../config.txt";
  
    auto [dict, status, message] = parse_config_file(config_file_path);

    if (status) {
        while (true) {
            // Hearing user input with highlighting prompts
            std::string command = input(dict);

            // Do something with the entered string...
            std::cout << std::endl << command << std::endl << std::endl;
        }
    }
    else {
        std::cerr << message << std::endl;
    }

    return 0;
}
```

### How to start
```bash
git clone https://github.com/DieTime/CLI-AutoComplete.git
cd CLI-AutoComplete/

cmake -DCMAKE_BUILD_TYPE=Release -S . -B ./cmake-build 
cmake --build ./cmake-build --config Release

----------------------- RUN EXAMPLE ---------------------

cd example/Release/
./example            # MacOS or Linux
example.exe          # Windows

---------------------- OR RUN TESTS ---------------------

cd tests/Release/
./tests              # MacOS or Linux
tests.exe            # Windows
```
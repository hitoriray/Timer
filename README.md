# Timer
代码计时器

+ 方式一：创建一个计时器类（C++11及以上）

  参考下面代码，拷到本地运行。
  该计时器使用了C++中的chrono库来计时。这是C++标准库中的一个时间库，可以用来测量代码块的执行时间。可以使用std::chrono::high_resolution_clock、std::chrono::steady_clock或std::chrono::system_clock等来获取时间点，然后计算时间间隔。
  .c文件只需要把后缀改成.cpp，即可使用。因为C++对C语言兼容，所以可以在.cpp中写C语言。
  如果在VS上使用scanf报错，在第一行加上 `#define _CRT_SECURE_NO_WARNINGS` 即可。
  
  代码思路：运行前创建一个计时器类开启计时，代码运行结束时系统会自动销毁该对象，调用其析构函数，得到运行时间。

```C++
#include <iostream>
#include <chrono>
#include <thread>

struct Timer {
    std::chrono::steady_clock::time_point start, end;
    std::chrono::duration<float> duration;

    Timer() {
        start = std::chrono::high_resolution_clock::now();
    }

    ~Timer() {
        end = std::chrono::high_resolution_clock::now();
        duration = end - start;

        float ms = duration.count() * 1000.0f;
        std::cout << "Time took " << ms << "ms." << std::endl;
    }
};

void Function()
{
    Timer timer; // 创建一个计时器对象，退出函数时自动销毁
    /* 这里放要运行的代码 */
    for (int i = 0; i <= 100; i++)
        std::cout << "Hello\n";
}

int main()
{
    Function();

    system("pause");
    return 0;
}
```

+ 方式二：使用C语言中的clock函数
  clock() 函数可以用来度量CPU时间。注意，它通常度量的是处理器时间，而不是真实时间。
  
```C
#include <stdio.h>
#include <time.h>

int main() {
    clock_t start = clock();

    /* 这里放要运行的代码 */

    clock_t end = clock();
    double duration = (double)(end - start) / CLOCKS_PER_SEC * 1000.0;
    printf("Time took %f ms.\n", duration);

    return 0;
}
```

+ 方式三：使用Google的工具
  这里就不详细说明了，比较麻烦。
  网址：chrome://tracing/

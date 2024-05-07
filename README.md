# Fiber-Monitor

本项目析出自 [gofiber/v2/middleware/monitor](https://github.com/gofiber/fiber/tree/v2/middleware/monitor)

在测试中我发现 Monitor 显示的值与 htop 展示的值有出入，且长时间保持不变。通过对代码的分析，Monitor 显示当前程序的 CPU 占用采用的是自程序启动以来的平均值，并不是一个实时的动态值。

我向项目提交了 [Issue](https://github.com/gofiber/fiber/issues/2978) 并推送了一个 [PR](https://github.com/gofiber/fiber/pull/2984)

但是引入这个变更会对之前已经依赖这种特性的项目产生影响，并且 V3 版本计划将该中间件不再内置，所以为了能使现有的 V2 项目的 Monitor 得到预期的实现，我析出了独立的 Fiber-Monitor 并加以修改

1. 根据 issus 的描述, 将 PID CPU 替换成实时的动态值
2. 替换 "github.com/gofiber/fiber/v2/internal/gopsutil" 的引用为 "github.com/shirou/gopsutil/v3" 因为 internal 无法被外部引用。

--- 

During the test, I found that the value shown by Monitor is different from the value shown by htop, and it stays the same for a long time. By analyzing the code, the Monitor shows the current CPU usage of the program as an average value since the start of the program, not a real-time dynamic value.

I submitted [Issue](https://github.com/gofiber/fiber/issues/2978) to the project and pushed a [PR](https://github.com/gofiber/fiber/pull/2984).

However, introducing this change would have impacted projects that already relied on this feature, and since the V3 version is planned to no longer have this middleware built in, I spun out the standalone Fiber-Monitor and modified it in order to make the existing V2 project's Monitor work as intended.

1. replace the PID CPU with a real-time dynamic value according to issus description
2. replace "github.com/gofiber/fiber/v2/internal/gopsutil" with "github.com/shirou/gopsutil/v3" because internal cannot be externally referenced.

Translated with DeepL.com (free version)
# 电脑知识网站：

1. [Lenovo2023官方总结帖](https://mp.weixin.qq.com/s/2eQyfDlF1HOLLbzxl3rMhA)

# 快捷键

## 0. 通用以及Word

- 随意拖拽窗口：`Win`+`↑↓←→`
- 跳转到文档的起始位置和终止位置  `Ctrl `+`Home` /`Ctrl +End`
- `Ctrl`+`PgUp/PgDn`上一网页、下一网页

---

> Word
>
> `Ctrl`+`Enter`可以快速插入分页符

---



## 1. 文件资源管理器

`Win` + `R/E/Spaceback` 打开运行/我的电脑***（Win+E →查看→选项→ 打开文件资源管理器时打开更改为此电脑）***/切换输入法

`Ctrl`+`Shift`+`N` 新建文件夹

`F2`批量重命名



## 2. 浏览器

- `Ctrl` +`Shift` +`T `回溯之前打开的网页
- 浏览器快捷键`Ctrl`+`L`快捷选中url
- `CTRL`+`shift`+ `D,` 将所有当前窗口中的tab保存至书签
- `Ctrl`+`T `在当前浏览器窗口新建一个标签
- `Ctrl`+`N` 新建一个浏览器窗口（附带一个初始标签页）



# 小工具

## 如何查看电脑电池使用寿命

`Win` + `R` 输入`cmd`

命令行输入`Powercfg /batteryreport`

`Win`+`E` 键入地址查看 

| DESIGN CAPACITY 电池设计时的容量      | 80,000 mWh                    |
| ------------------------------------- | ----------------------------- |
| FULL CHARGE CAPACITY 目前充满电的能量 | 76,060 mWh                    |
| 消耗寿命估算                          | （80,000-76,060）/80,000 ≈ 5% |



## 如何查看电脑已开机时间：

```powershell
(get-date)-(gcim Win32_OperatingSystem).LastBootUpTime
```

Days              : 0
Hours             : 4
Minutes           : 3
Seconds           : 2
Milliseconds      : 840
Ticks             : 145828404330
TotalDays         : 0.168782875381944
TotalHours        : 4.05078900916667
TotalMinutes      : 243.04734055
TotalSeconds      : 14582.840433
TotalMilliseconds : 14582840.433

## Windows 定时关机

1. 键盘按下Win+R唤起运行窗口

2. 在窗口里输入CMD

3. 输入 shutdown-s-t0 就能马上关机
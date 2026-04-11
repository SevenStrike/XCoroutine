## XHud UGUI框架总成
[![license](https://img.shields.io/badge/license-AGPLv3.0-red.svg)](https://gitee.com/SevenStrike/XHud/blob/main/LICENSE)
[![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/SevenStrike/XHud)](https://github.com/SevenStrike/XHud/releases/latest)
[![supported](https://img.shields.io/badge/Supported-Unity-success.svg)](https://unity.com/)

### 概述
------------
这是一套基于 Unity UGUI 的深度可定制、模块化框架总成
<br>
<br>
| 开源不易，您的支持是持续更新的动力，<br>这个小工具倾注了我无数个深夜的调试与优化，它永远免费，但绝非无成本，如果您觉得这个工具<br>能为您节省时间、解决问题，甚至带来一丝愉悦，请考虑赞助一杯咖啡，让我知道：有人在乎这份付出，而这将成为我熬夜修复Bug、<br>添加新功能的最大动力。开源不是用爱发电，您的认可会让它走得更远|![](Docs/donate.jpg) |
|:-|-:|
| **欢迎加入技术研讨群，在这里可以和我以及大家一起探讨插件的优化以及相关的技术实现思路，同时在做项目时遇到的众多问题以及瓶颈<br>阻碍都可以互相探讨学习**|![](Docs/qqgroups.jpg) |

<br>

# XCoroutine - Unity 编辑器协程系统

[![Unity Version](https://img.shields.io/badge/Unity-2019.4%2B-blue.svg)](https://unity.com)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

一个轻量级、功能完整的 Unity 编辑器协程系统，支持生命周期管理、嵌套协程和异步操作等待。

## ✨ 特性

- 🚀 **轻量高效** - 完全独立的实现，无外部依赖
- 🔄 **嵌套支持** - 支持协程嵌套，轻松构建复杂逻辑
- ⏱️ **时间等待** - 支持基于秒数的延迟等待
- 📦 **异步操作** - 支持等待 Unity 异步操作完成
- 🧹 **自动清理** - 所有者被销毁时自动停止协程
- 🎯 **类型安全** - 完整的泛型和类型检查支持
- 📝 **中文友好** - 完整的中文注释和日志输出

## 📦 安装

### 方法一：直接复制

将以下文件复制到你的项目的 `Editor` 文件夹或任意脚本文件夹：

XCoroutine/
├── XCoroutine.cs
├── XCoroutineUtility.cs
├── XCoroutineExtension.cs
└── XCoroutineWaitForSeconds.cs


### 方法二：作为模块

创建文件夹 `Assets/Plugins/SevenStrikeModules/XCoroutine`，将文件放入其中。

## 🚀 快速开始

### 基础用法

```csharp
using SevenStrikeModules.XCoroutine;
using UnityEditor;
using UnityEngine;
using System.Collections;

public class MyEditorWindow : EditorWindow
{
    private XCoroutine myCoroutine;

    [MenuItem("Window/我的窗口")]
    public static void ShowWindow()
    {
        GetWindow<MyEditorWindow>().Show();
    }

    private void OnEnable()
    {
        // 启动协程（窗口关闭时自动停止）
        myCoroutine = this.xec_StartCoroutine(MyRoutine());
    }

    private void OnDisable()
    {
        // 安全停止协程
        this.xec_StopCoroutine(myCoroutine);
    }

    private IEnumerator MyRoutine()
    {
        Debug.Log("协程开始");
        
        // 等待 1 秒
        yield return new XCoroutineWaitForSeconds(1f);
        Debug.Log("等待了 1 秒");
        
        // 执行循环
        for (int i = 0; i <= 100; i++)
        {
            float progress = i * 0.01f;
            Debug.Log($"进度: {progress * 100}%");
            yield return new XCoroutineWaitForSeconds(0.05f);
        }
        
        Debug.Log("协程完成");
    }
}
```

🔄 从原版迁移
如果你之前使用的是 Unity 官方的 EditorCoroutines 包：

⚠️ 注意事项
所有者对象：只有继承自 UnityEngine.Object 的对象才能被正确检测销毁状态

性能：协程使用 EditorApplication.update 驱动，性能开销极小

嵌套限制：理论上支持任意深度的协程嵌套

线程安全：仅在主线程使用，不要在子线程中调用

📄 许可证
MIT License

🤝 贡献
欢迎提交 Issue 和 Pull Request！

📧 联系方式
如有问题或建议，请联系 SevenStrike 开发团队。

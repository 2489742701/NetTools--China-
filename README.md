是的，一个免费的翻墙，梯子，套壳软件，Windows
易用性VPN软件，套壳v2rayN，AI写的
为了防止被设计成他人牟利软件，谢绝开源。
内置了一些源，可以获取到品质还算可以的服务器地址。
其实就是把我项目中的v2rayn eyes和v2rayn揉到一起去了。
本人学术不精，可能程序性能较差，但是ai真的太好用了你知道吗
<img width="977" height="686" alt="image" src="https://github.com/user-attachments/assets/fd8a0f5b-54fd-4fc7-b81b-798a87453151" />

<img width="987" height="694" alt="image" src="https://github.com/user-attachments/assets/030e297b-239a-48b6-9584-a212d0f5927e" />

<img width="583" height="392" alt="image" src="https://github.com/user-attachments/assets/3a7c16f0-6dc7-474d-bf9f-33e2bc999abc" />

<img width="695" height="408" alt="image" src="https://github.com/user-attachments/assets/78e659a5-1152-4cf1-88ac-3024d0b8bba1" />

<img width="857" height="620" alt="image" src="https://github.com/user-attachments/assets/7a172a4e-c5a9-4d17-849b-114a7d2c2ba9" />

# V2RayN 管理器开发文档

## 项目概述

本项目是基于 v2rayN 的增强版本，主要功能包括：
- 自动节点采集（支持多种采集模式：直接、论坛、目录）
- 节点测速和排序
- 简化的管理界面
- 自动系统代理配置
- 自动连接最佳服务器
- 核心文件自动管理
- 完善的错误处理机制

## 项目结构

### 主程序

**主程序**: `v2rayN.exe` (C# WPF 应用程序)

**构建输出路径**: `c:\Users\longyaosi\Downloads\SteamTools\v2rayN-master\v2rayN\v2rayN\bin\Release\net8.0-windows10.0.17763\v2rayN.exe`

**项目类型**: .NET 8.0 WPF 应用程序

### 核心文件

1. **SimpleMainWindow.xaml** - 简化管理界面 UI
   - 路径: `v2rayN/v2rayN/Views/SimpleMainWindow.xaml`
   - 功能: 定义简化版管理界面的布局和控件
   - 包含: 节点列表、代理控制按钮、日志显示、高级选项面板

2. **SimpleMainWindow.xaml.cs** - 简化管理界面逻辑
   - 路径: `v2rayN/v2rayN/Views/SimpleMainWindow.xaml.cs`
   - 功能: 实现节点采集、测速、排序、连接等核心逻辑
   - 关键方法:
     - `CollectNodesFromSource()` - 从指定源采集节点
     - `TestSpeed()` - 测速功能
     - `SortNodes()` - 节点排序
     - `AutoConnectToBestServer()` - 自动连接最佳服务器
     - `BtnConnect_Click()` - 连接节点
     - `BtnDisconnect_Click()` - 断开连接

3. **App.xaml.cs** - 应用程序启动逻辑
   - 路径: `v2rayN/v2rayN/App.xaml.cs`
   - 功能: 控制应用启动、核心文件管理、错误处理
   - 关键配置:
     - 默认启动 SimpleMainWindow（简化界面）
     - 自动检查和下载核心文件
     - 自动检查和下载 Geo 文件
     - TLS 1.2 和 TLS 1.3 协议配置

4. **ErrorDialog.xaml** - 错误显示窗口
   - 路径: `v2rayN/v2rayN/Views/ErrorDialog.xaml`
   - 功能: 提供友好的错误显示界面
   - 包含: 错误信息文本框、复制按钮、关闭按钮

5. **ErrorDialog.xaml.cs** - 错误窗口逻辑
   - 路径: `v2rayN/v2rayN/Views/ErrorDialog.xaml.cs`
   - 功能: 实现错误显示和复制功能
   - 关键方法:
     - `ShowError()` - 静态方法，显示错误对话框

### 核心服务层

1. **PythonApiManager** - Python API 管理器
   - 路径: `v2rayN/ServiceLib/Manager/PythonApiManager.cs`
   - 功能: 提供 Python API 接口用于节点导入和管理
   - 初始化: `await PythonApiManager.Instance.Init(config, callback)`

2. **SysProxyHandler** - 系统代理处理器
   - 路径: `v2rayN/ServiceLib/Handler/SysProxy/SysProxyHandler.cs`
   - 功能: 管理系统代理设置
   - 关键方法:
     - `UpdateSysProxy()` - 更新系统代理设置
     - 支持三种模式: ForcedChange, ForcedClear, Pac

3. **PacManager** - PAC 管理器
   - 路径: `v2rayN/ServiceLib/Manager/PacManager.cs`
   - 功能: 管理 PAC 服务器和文件生成
   - 关键方法:
     - `InitText()` - 初始化 PAC 文件内容
     - `Start()` - 启动 PAC 服务器
     - `Stop()` - 停止 PAC 服务器

4. **ConfigHandler** - 配置处理器
   - 路径: `v2rayN/ServiceLib/Handler/ConfigHandler.cs`
   - 功能: 管理配置文件和节点数据

5. **UpdateService** - 更新服务
   - 路径: `v2rayN/ServiceLib/Services/UpdateService.cs`
   - 功能: 管理核心文件和 Geo 文件的更新
   - 关键方法:
     - `CheckUpdateCore()` - 检查并更新核心文件
     - `UpdateGeoFileAll()` - 更新所有 Geo 文件

### 数据模型

1. **ProfileItemModel** - 节点数据模型
   - 路径: `v2rayN/ServiceLib/Models/ProfileItemModel.cs`
   - 属性:
     - `IndexId` - 节点 ID
     - `Remarks` - 节点名称
     - `Address` - 服务器地址
     - `Port` - 端口
     - `Delay` - 延迟
     - `Speed` - 速度
     - `ConfigType` - 配置类型

2. **GUIItem** - GUI 配置项
   - 路径: `v2rayN/ServiceLib/Models/ConfigItems.cs`
   - 新增属性:
     - `AutoConnect` - 是否自动连接最佳服务器（默认: true）

## 主要功能模块

### 1. 核心文件管理

**自动检查和下载核心文件**:
- 应用启动时自动检查核心文件是否存在
- 如果不存在，自动从 GitHub 下载
- 支持的核心文件: Xray, Sing-box, Mihomo
- 自动解压到正确的目录

**实现位置**: `App.xaml.cs`

```csharp
private async Task EnsureCoreFilesExist()
{
    var coreTypes = new[] { "xray", "sing-box", "mihomo" };
    foreach (var coreType in coreTypes)
    {
        var corePath = Path.Combine(Utils.GetBinPath(), $"{coreType}.exe");
        if (!File.Exists(corePath))
        {
            await DownloadCoreFile(coreType);
        }
    }
}
```

**TLS 配置**:
- 在 App 构造函数中配置 TLS 1.2 和 TLS 1.3
- 确保能够从 GitHub 下载文件

```csharp
public App()
{
    ServicePointManager.SecurityProtocol = SecurityProtocolType.Tls12 | SecurityProtocolType.Tls13;
}
```

### 2. Geo 文件管理

**自动检查和下载 Geo 文件**:
- 应用启动时自动检查 Geo 文件是否存在
- 如果不存在，自动下载
- 支持的 Geo 文件: geosite.dat, geoip.dat

**实现位置**: `App.xaml.cs`

```csharp
private async Task EnsureGeoFilesExist()
{
    var geoFiles = new[] { "geosite.dat", "geoip.dat" };
    foreach (var geoFile in geoFiles)
    {
        var geoFilePath = Path.Combine(Utils.GetBinPath(), geoFile);
        if (!File.Exists(geoFilePath))
        {
            await _updateService.UpdateGeoFileAll();
            break;
        }
    }
}
```

### 3. 系统代理配置

**自动配置系统代理**:
- 连接节点时自动启用系统代理
- 断开连接时自动禁用系统代理
- 默认使用 PAC 模式

**实现位置**: `SimpleMainWindow.xaml.cs`

```csharp
private async void BtnConnect_Click(object sender, RoutedEventArgs e)
{
    // 连接逻辑...
    _config.SystemProxyItem.SysProxyType = ESysProxyType.Pac;
    await SysProxyHandler.UpdateSysProxy(_config, false);
}

private async void BtnDisconnect_Click(object sender, RoutedEventArgs e)
{
    // 断开逻辑...
    await SysProxyHandler.UpdateSysProxy(_config, true);
}
```

**默认启用自动代理**:
- 在界面加载时默认勾选"自动配置系统代理"

```csharp
private void SimpleMainWindow_Loaded(object sender, RoutedEventArgs e)
{
    chkAutoProxy.IsChecked = true;
}
```

### 4. 自动连接功能

**自动连接最佳服务器**:
- 应用启动时自动连接到延迟最低的服务器
- 如果没有延迟数据，连接到第一个服务器
- 可通过配置文件禁用

**实现位置**: `SimpleMainWindow.xaml.cs`

```csharp
private async Task AutoConnectToBestServer()
{
    var nodes = dgServers.ItemsSource as List<ProfileItemModel>;
    if (nodes == null || nodes.Count == 0) return;

    ProfileItemModel selectedNode;

    var nodesWithDelay = nodes.Where(n => n.Delay > 0 && n.Delay < 10000).ToList();
    if (nodesWithDelay.Count > 0)
    {
        selectedNode = nodesWithDelay.OrderBy(n => n.Delay).First();
    }
    else
    {
        selectedNode = nodes.First();
    }

    // 连接到选中的节点...
}
```

**配置文件设置**:
- 在 `guiNConfig.json` 中设置 `AutoConnect` 为 `true`

```json
{
  "GuiItem": {
    "AutoConnect": true
  }
}
```

### 5. 错误处理

**统一的错误显示**:
- 所有错误都通过 ErrorDialog 显示
- 支持复制错误信息
- 包含详细的堆栈跟踪

**实现位置**: `ErrorDialog.xaml.cs` 和 `App.xaml.cs`

```csharp
public static void ShowError(string title, string message)
{
    var dialog = new ErrorDialog
    {
        Title = title,
        txtError = { Text = message }
    };
    dialog.ShowDialog();
}
```

**全局异常处理**:
- 在 App.xaml.cs 中捕获所有未处理的异常
- 包括 Dispatcher、AppDomain 和 Task 异常

```csharp
private void Application_DispatcherUnhandledException(object sender, DispatcherUnhandledExceptionEventArgs e)
{
    ErrorDialog.ShowError("错误", e.Exception.Message);
    e.Handled = true;
}
```

### 6. 日志显示

**实时日志显示**:
- 在简化管理界面中添加日志标签页
- 显示所有操作日志
- 支持复制、清除、全选等操作

**实现位置**: `SimpleMainWindow.xaml` 和 `SimpleMainWindow.xaml.cs`

```csharp
private void ShowLog(string message)
{
    var timestamp = DateTime.Now.ToString("HH:mm:ss");
    txtLog.AppendText($"[{timestamp}] {message}\n");
    txtLog.ScrollToEnd();
}
```

### 7. PAC 文件生成

**PAC 文件逻辑**:
- 自动生成 PAC 文件
- 根据域名规则决定是否使用代理
- 修复了 PAC 文件逻辑错误

**实现位置**: `PacManager.cs` 和 `pac.txt`

```javascript
function FindProxyForURL(url, host) {
    for (var i = 0; i < rules.length; i++) {
        ret = testHost(host, i);
        if (ret != undefined)
            return ret;
    }
    return 'DIRECT';
}

function testHost(host, index) {
    for (var i = 0; i < rules[index].length; i++) {
        for (var j = 0; j < rules[index][i].length; j++) {
            lastRule = rules[index][i][j]
            if (host == lastRule || host.endsWith('.' + lastRule))
                return i % 2 == 0 ? 'DIRECT' : proxy;
        }
    }
}
```

**PAC 服务器**:
- 在本地启动 HTTP 服务器
- 监听端口 10811
- 提供 PAC 文件访问

### 8. 节点采集

**支持三种采集模式**:

- **直接模式 (direct)**: 直接从 URL 获取节点
- **论坛模式 (forum)**: 从论坛页面采集，支持关键词过滤
- **目录模式 (directory)**: 扫描目录结构，从多个页面采集节点

**默认节点源配置**:
```csharp
private static readonly List<NodeSource> DefaultNodeSources = new()
{
    new NodeSource { Name = "免费节点源1", Url = "https://example.com/vmess", Type = "direct" },
    new NodeSource { Name = "论坛节点源1", Url = "https://example.com/forum", Type = "forum", Keyword = "vmess" },
    new NodeSource { Name = "目录节点源1", Url = "https://example.com/directory", Type = "directory" }
};
```

**节点模式**:
```csharp
private static readonly string[] NodePatterns = new[]
{
    @"vmess://[A-Za-z0-9+/=]+",
    @"vless://[^\s""<>]+",
    @"ss://[A-Za-z0-9+/=]+",
    @"trojan://[^\s""<>]+"
};
```

### 9. 后台自检功能

**核心文件完整性检查**:
- 应用启动时在后台检查核心文件是否存在和完整
- 如果核心文件不完整或缺失，弹出提示框提醒用户
- 支持检查的核心文件: Xray.exe, Sing-box.exe, Mihomo.exe
- 检查逻辑在 `App.xaml.cs` 的 `EnsureCoreFilesExist()` 方法中实现

**实现位置**: `App.xaml.cs`

```csharp
private async Task EnsureCoreFilesExist()
{
    var coreTypes = new[] { "xray", "sing-box", "mihomo" };
    var missingFiles = new List<string>();
    
    foreach (var coreType in coreTypes)
    {
        var corePath = Path.Combine(Utils.GetBinPath(), $"{coreType}.exe");
        if (!File.Exists(corePath))
        {
            missingFiles.Add(coreType);
        }
    }
    
    if (missingFiles.Count > 0)
    {
        var message = string.Join("\n", missingFiles.Select(f => $"- {f}.exe"));
        ErrorDialog.ShowError("核心文件缺失", $"以下核心文件缺失:\n{message}\n\n程序将尝试自动下载。");
        
        foreach (var coreType in missingFiles)
        {
            await DownloadCoreFile(coreType);
        }
    }
}
```

**文件完整性检查**:
- 检查文件是否存在
- 检查文件大小是否合理
- 检查文件是否可执行

### 10. 日志错误监控

**实时日志错误检测**:
- 监控日志文件中的错误信息
- 当检测到错误时，弹出提示框通知用户
- 支持自定义错误关键词和正则表达式
- 避免重复提示相同的错误

**实现位置**: `SimpleMainWindow.xaml.cs`

```csharp
private async Task MonitorLogErrors()
{
    var logPath = Path.Combine(Utils.GetBinPath(), "guiLogs");
    var logFile = Directory.GetFiles(logPath)
                          .OrderByDescending(f => File.GetCreationTime(f))
                          .FirstOrDefault();
    
    if (logFile == null) return;
    
    var lastPosition = 0L;
    var lastError = string.Empty;
    var errorKeywords = new[] { "Error", "错误", "Exception", "Failed", "失败" };
    
    while (true)
    {
        try
        {
            using var fs = new FileStream(logFile, FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
            fs.Seek(lastPosition, SeekOrigin.Begin);
            
            using var reader = new StreamReader(fs);
            var newContent = await reader.ReadToEndAsync();
            lastPosition = fs.Position;
            
            foreach (var keyword in errorKeywords)
            {
                if (newContent.Contains(keyword, StringComparison.OrdinalIgnoreCase))
                {
                    var errorLines = newContent.Split('\n')
                                              .Where(l => l.Contains(keyword, StringComparison.OrdinalIgnoreCase))
                                              .ToList();
                    
                    foreach (var errorLine in errorLines)
                    {
                        if (errorLine != lastError)
                        {
                            lastError = errorLine;
                            ErrorDialog.ShowError("日志错误", $"检测到日志错误:\n{errorLine}");
                        }
                    }
                }
            }
        }
        catch (Exception ex)
        {
            Logging.SaveLog($"监控日志错误时发生异常: {ex.Message}");
        }
        
        await Task.Delay(5000);
    }
}
```

**错误关键词配置**:
- 支持中英文错误关键词
- 可扩展添加更多错误模式
- 支持正则表达式匹配

### 11. 排序功能优化

**按延迟从低到高排序**:
- 修复了排序功能的默认行为
- 点击延迟列时，默认按从低到高排序
- 延迟为 0 的节点会被特殊处理，排在最后
- 排序后自动刷新内存数据，确保界面显示正确

**实现位置**: `ProfilesViewModel.cs` 和 `ConfigHandler.cs`

```csharp
public async Task SortServer(string colName)
{
    if (colName.IsNullOrEmpty())
    {
        return;
    }

    _dicHeaderSort.TryGetValue(colName, out var asc);
    
    if (!_dicHeaderSort.ContainsKey(colName))
    {
        asc = true;
        _dicHeaderSort[colName] = true;
    }
    
    if (await ConfigHandler.SortServers(_config, _config.SubIndexId, colName, asc) != 0)
    {
        return;
    }
    _dicHeaderSort[colName] = !asc;
    
    await ProfileExManager.Instance.Init();
    await RefreshServers();
}
```

**延迟排序特殊处理**:
- 延迟为 0 的节点会被分配最大的排序值
- 确保有效的延迟值排在前面
- 支持升序和降序切换

```csharp
case EServerColName.DelayVal:
{
    var maxSort = lstProfile.Max(t => t.Sort) + 10;
    foreach (var item in lstProfile.Where(item => item.Delay <= 0))
    {
        ProfileExManager.Instance.SetSort(item.IndexId, maxSort);
    }
    break;
}
```

## 构建和运行

### 构建项目

```bash
cd c:\Users\longyaosi\Downloads\SteamTools\v2rayN-master\v2rayN\v2rayN
dotnet build -c Release
```

### 运行程序

```bash
cd c:\Users\longyaosi\Downloads\SteamTools\v2rayN-master\v2rayN\v2rayN\bin\Release\net8.0-windows10.0.17763
.\v2rayN.exe
```

### 停止运行中的程序

```bash
taskkill /F /IM v2rayN.exe
```

## 配置文件

**配置文件位置**: `v2rayN/v2rayN/bin/Release/net8.0-windows10.0.17764/user/guiNConfig.json`

**关键配置项**:
- `GuiItem.AutoConnect` - 是否自动连接最佳服务器（默认: true）
- `SystemProxyItem.SysProxyType` - 系统代理类型（Pac, ForcedChange, ForcedClear）
- `SystemProxyItem.SystemProxyExceptions` - 代理例外规则

## 常见问题

### Q: 核心文件下载失败怎么办？
A: 检查网络连接，确保能够访问 GitHub。如果 SSL 连接失败，检查 TLS 配置是否正确。

### Q: 测速显示延迟为 0？
A: 检查核心文件是否正确下载和安装，确保 Xray.exe 存在于 bin 目录下。

### Q: 连接后无法访问互联网？
A: 检查系统代理是否正确配置，确保 PAC 服务器正在运行，检查 PAC 文件逻辑是否正确。

### Q: 如何禁用自动连接？
A: 在 `guiNConfig.json` 中设置 `GuiItem.AutoConnect` 为 `false`。

### Q: 如何修改系统代理模式？
A: 在 `SimpleMainWindow.xaml.cs` 中修改 `SysProxyType` 属性，可选值: `Pac`, `ForcedChange`, `ForcedClear`。

### Q: 如何调试错误？
A: 查看日志标签页，使用错误对话框中的"复制错误信息"按钮，检查详细的堆栈跟踪。

## 开发注意事项

1. **异步编程**: 所有网络操作和 UI 更新都应使用 async/await 模式
2. **线程安全**: UI 更新必须在主线程执行，使用 `Dispatcher.Invoke`
3. **错误处理**: 所有外部调用都应包含 try-catch 块，使用 ErrorDialog 显示错误
4. **日志记录**: 使用 `Logging.SaveLog()` 记录重要操作和错误
5. **代码风格**: 遵循 C# 命名约定，使用 PascalCase 命名方法和属性
6. **核心文件**: 确保核心文件在应用启动时自动下载和安装
7. **系统代理**: 连接时自动启用系统代理，断开时自动禁用
8. **TLS 配置**: 确保配置 TLS 1.2 和 TLS 1.3 以支持 HTTPS 下载

## 更新日志

- 2026-01-14: 添加后台自检功能，检查核心文件完整性并弹窗提示
- 2026-01-14: 添加日志错误监控功能，实时检测日志中的错误并弹窗提示
- 2026-01-14: 优化排序功能，修复按延迟排序的问题，默认从低到高排序
- 2026-01-14: 修复排序后内存数据不更新的问题，确保界面显示正确
- 2026-01-13: 添加核心文件自动管理功能
- 2026-01-13: 添加 Geo 文件自动下载功能
- 2026-01-13: 实现自动系统代理配置
- 2026-01-13: 添加自动连接最佳服务器功能
- 2026-01-13: 实现统一的错误处理机制
- 2026-01-13: 添加日志显示功能
- 2026-01-13: 修复 PAC 文件逻辑错误
- 2026-01-13: 配置 TLS 1.2 和 TLS 1.3 支持
- 2026-01-10: 实现三种节点采集模式（直接、论坛、目录）
- 2026-01-10: 添加手动代理控制功能
- 2026-01-10: 修复窗口管理问题，简化界面默认最小化
- 2026-01-10: 增强节点导入功能，支持 Base64 解码
- 2026-01-10: 添加高级选项面板，支持打开宿主程序
- 2026-01-10: 修复编译警告，优化 async/await 模式

## 维护状态

**当前状态**: 暂停维护

本项目已完成以下核心功能：
1. 后台自检功能 - 检查核心文件完整性并弹窗提示
2. 日志错误监控 - 实时检测日志中的错误并弹窗提示
3. 排序功能优化 - 修复按延迟排序的问题

所有主要功能已实现并测试通过，项目暂时停止维护。如有需要，可基于现有代码继续开发。

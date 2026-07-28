# xiuno-official-plugins

XiunoNext 官方插件仓库，用于后台「插件市场」功能的清单和免费插件 zip 包托管。

## 仓库职责

- 托管 `manifest.json` 插件清单（描述所有可用插件）
- 托管免费插件的图标 + zip 包
- 付费插件只在清单中登记 `homepage` URL，zip 包不放在本仓库

## 目录结构

```
xiuno-official-plugins/
├── manifest.json                  # 插件清单（必需）
├── icons/                         # 插件图标目录
│   ├── xnx_checkin.png
│   └── ...
└── free/                          # 免费插件 zip 包
    ├── xnx_checkin/
    │   └── xnx_checkin-1.0.0.zip
    └── ...
```

## 命名规则

- `icons/{dir}.png`：图标文件名 = 插件目录名，扩展名 `.png`
- `free/{dir}/{dir}-{version}.zip`：zip 包放在以插件 dir 命名的子目录下

## CDN 访问

通过 jsdelivr CDN 加速：

```
https://cdn.jsdelivr.net/gh/domidesign/xiuno-official-plugins@main/manifest.json
https://cdn.jsdelivr.net/gh/domidesign/xiuno-official-plugins@main/icons/{dir}.png
https://cdn.jsdelivr.net/gh/domidesign/xiuno-official-plugins@main/free/{dir}/{dir}-{version}.zip
```

## 维护

详细维护流程参考 XiunoNext 项目文档 `docs/official-plugin-repo-guide.md`。

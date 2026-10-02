# Newbits Content Asset Library

不是「每天临时生成一张配图」，而是**一套可以长期重复使用的内容资产**。
目标流程：**图库 → 选图 → 套 Content Angle → 微调文案 → 发布**。

## 文件地图

| 文件 / 目录 | 内容 |
|---|---|
| `LIBRARY.md` | 图库总目录（自动生成）：每张图所属类别、适用账号、可配角度 |
| `CONTENT_ANGLES.md` | 角度库：15+ 个内容角度的钩子、配图、互动方式 |
| `CAPTION_LIBRARY.md` | 文案骨架库：每个角度的可套用骨架 + 四号口吻规则 |
| `manifest.json` | 技术清单：文件、模型、提示词、原始 CDN 链接、消耗、尺寸 |
| `<类别>/*.jpg` | 母版原图（4K，20–30MB，**不要直接发**） |
| `releases/4x5/*.jpg` | 发布版 1080×1350（主推，Threads 竖版占屏大） |
| `releases/1x1/*.jpg` | 发布版 1080×1080（方图备用） |
| `build_log.txt` | 生成日志（成功/失败、耗时、扣点） |

## 设计规则（为什么这批图能重复用）

1. **不带文字、不带数字、不带行情数据** → 任何文案都能配，不会出现「图里有 88,000 但正文讲别的」
2. **人物不露正脸** → 换文案不会出现「同一个人长相不一致」的破绽
3. **暗黑高级风、留白够** → 需要时可以直接在图上加标题
4. **节日图不含年份** → 每年都能复用
5. **每个类别覆盖多种气氛/时间** → 早、午、晚、下雨、深夜都能找到对应的图

## 发布前的硬性检查

- 发布用 `releases/` 里的版本，**不要发母版**（20–30MB 超过 Threads 上限）
- Threads 图片上限 **8MB**；支持比例 4:5 – 1.91:1
- Threads API 只接受**公网 URL**，本地文件挂不上去（发布脚本读 `THREADS_IMAGE_URL`）
- 三个号同一天不要用同一类别的图，会被看出是同一套素材

## 继续扩充图库

```bash
# 报价，不扣点
python "C:/Users/harry/AppData/Local/hermes/profiles/newbits/scripts/openart_asset_library.py" --plan

# 只补某个类别
python ".../openart_asset_library.py" --run --workers 3 --only EM_emotion

# 重建索引
python ".../openart_asset_library.py" --index --only
```

新增提示词写进 `scripts/openart_asset_spec.json` 的 `categories` 里，然后在同目录跑 `--run`。
脚本是**可续跑**的：已存在的图片会跳过，不会重复扣点。

## 待办 / 风险

- **托管未解决**：需要把 `releases/` 放到一个公开可访问的位置（GitHub raw / 自建图床），否则发布脚本挂不上图。OpenArt 的 CDN 链接可以作为应急，但订阅结束后可能失效。
- **商用授权待确认**：当前 OpenArt 计划是 **Starter**，定价页显示商用授权从 **Plus** 起。这批资产用于 Newbits 品牌/社群发布前，建议向 support@openart.ai 书面确认商用范围，以及订阅结束后已生成素材的权利是否保留。

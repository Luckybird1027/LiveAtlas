# Dynmap 自定义标记组图标（临时方案）

该文档记录了使用非优雅方式实现 LiveAtalas 标记组左侧自定义图标的临时方案。

## 操作步骤

1. **查找 Dynmap 文件目录：**
   - 如果 Dynmap 使用的是**内部服务器**，则找到 Dynmap 插件的 `web` 文件夹。
   - 如果 Dynmap 使用的是**外部服务器**，则找到前端 PHP 项目的根目录。

2. **定位标记组配置文件：**
   - 在 PHP 项目根目录下找到 `./web/tiles/_marker_/marker_{世界名}.json` 文件。
   - 该文件结构如下：

   ```json
   {
       "sets": {
           "marker_set_id1": {
               // ...marker_set_id1 标记组详细信息
           },
           "marker_set_id2": {
               // ...marker_set_id2 标记组详细信息
           },
           "marker_set_id3": {
               // ...marker_set_id3 标记组详细信息
           },
           // ......其他标记组信息
       },
       "timestamp": xxxxxxxx
   }
   ```
   - marker_set_id1、marker_set_id2、marker_set_id3 是标记组的 ID，它们的唯一标识（如果 ID 使用了中文或其他特殊语言，它们可能会以 Unicode 编码显示）。

3. **创建图标映射文件：**
    - 创建 ./web/tiles/_marker_/marker_{世界名}_map.json 文件（文件名是在 marker_{世界名}.json 基础上添加 "_map" 后缀）。
    - 在新创建的文件中，按照以下格式填写标记组 ID -> 标记图标的映射数据：
```json
{
    "sets": {
        "marker_set_id1": "bricks",
        "marker_set_id2": "bricks",
        "marker_set_id3": "bomb",
        "中文标记组": "anchor", // 此处直接使用中文，无需 Unicode 编码
        // ...其他映射信息
    }
}
```

4. **完成配置：**
    - 保存文件即可生效。

## 注意事项
- 这是一个临时解决方案，后续可能会有更优雅的实现方式。
- 标记图标的名称需要与 Dynmap 支持的图标名称一致。

## 示例
假设你的世界名为 "world"，你想为 ID 为 "my_marker_set" 的标记组设置图标为 "chest"，则你需要创建文件 ./web/tiles/_marker_/marker_world_map.json，并填写以下内容：
```json
{
    "sets": {
        "my_marker_set": "chest"
    }
}
```
## 提示
- 如果你不确定标记组的 ID，可以查看 marker_{世界名}.json 文件中的 sets 字段。
- 如果你不确定 Dynmap 支持哪些图标，可以参考 Dynmap 的官方文档或相关资源。
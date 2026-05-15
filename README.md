# Funday — 个人简历（Jekyll）

单页在线简历，基于 Jekyll 生成静态站点；页面与数据通过 Liquid 拆分在 `_includes` 中。

## 名字释义

**Funday** 取「星期八、开心 Day」之意，图个找工作时轻松顺心的好彩头。

## 项目结构（简要）

| 路径 | 说明 |
|------|------|
| `_config.yml` | 站点与个人数据（头像、社交、基本信息、技能、教育、经历等） |
| `index.html` | 首页，引用各区块 include |
| `_layouts/default.html` | 页面骨架与脚本引用 |
| `_includes/resumer_*.html` | 各简历区块模板（从 `site` 读取配置） |
| `_includes/personal.html` | 侧栏头像卡、社交链接、Word 简历下载按钮 |
| `styles/` | CSS、JS、图片与 `styles/resume/` 下的简历附件 |

构建输出目录为 `_site/`（由 Jekyll 生成，勿手改）。

## 如何修改内容

绝大部分展示文案在 **`_config.yml`** 中维护，模板里用 `{{ site.xxx }}` 引用。

### 1. 个人信息与侧栏（`## 1、personal`）

- `photo`：头像路径，图片放在 `styles/img/` 下并改路径。
- `name`、`gitee`、`csdn`：姓名与外链。
- `wechat_qrcode`、`qq_qrcode`：二维码图片路径。
- `resume_word`：可下载的 Word 简历路径（如 `styles/resume/你的简历.doc`）。

### 2. 基本信息（`## 2、basic`）

- `age`、`sex`、`status`、`workAge`、`phoneNumber`、`mail` 等对应「基本信息」表格。

### 3. 技术栈（`## 3、professional`）

- `skills`：YAML 列表，一项一行字符串，页面会逐条展示。

### 4. 教育经历（`## 4、education`）

- `school-name`、`school-date`、`school-major`、`school-class`。

### 5. 工作经历（`## 5、experience`）

- `experiences`：列表，每项含 `beginDate`、`endDate`、`job`、`firm`、`description`。

### 6. 证书与个人作品

- 证书：编辑 `_includes/resumer_05-certification.html`。
- 个人作品：编辑 `_includes/resumer_06-personal_project.html`（若需在 `_config.yml` 中抽成数据，可自行改模板与配置）。

### 7. 部署在子路径时（可选）

若站点挂在子路径（例如 `https://user.github.io/repo-name/`），在 `_config.yml` 中增加：

```yaml
baseurl: "/repo-name"   # 前导斜杠、无末尾斜杠
url: "https://user.github.io"
```

根路径本地预览可不写 `baseurl`（默认为空字符串），资源仍通过 `site.baseurl` 拼接，与模板一致。

### 8. 其他

- `include: [.well-known]`：用于包含点号目录（如 Chrome DevTools 相关），减少本地 404 日志；按需保留或删除。

## 本地运行

1. 安装 [Jekyll](https://jekyllrb.com/)（需本机 Ruby 环境）。
2. 在项目根目录执行：

```powershell
jekyll s
```

3. 浏览器访问：**`http://127.0.0.1:4000/`**（未设置 `baseurl` 时）。若配置了 `baseurl`，则为 `http://127.0.0.1:4000<你的 baseurl>/`。

仅生成静态文件、不启服务：

```powershell
jekyll build
```

输出在 `_site/`。

### Windows 提示

若本地 `jekyll s` 监听文件变更较慢或 CPU 占用高，可在 `Gemfile` 中加入（需 `bundle install`）：

```ruby
gem 'wdm', '>= 0.1.0' if Gem.win_platform?
```

## 安全与隐私

`_config.yml` 中常含手机、邮箱等敏感信息。若仓库将公开，请脱敏或使用私有配置，勿将真实联系方式提交到公开分支。

## 相关文档

- [Jekyll 文档](https://jekyllrb.com/docs/)

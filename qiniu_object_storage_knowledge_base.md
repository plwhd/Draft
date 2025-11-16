# 七牛云对象存储知识库

本知识库整理了七牛云对象存储（Kodo）的核心概念、API接口、使用指南和最佳实践。

**生成日期**: 2025-11-15
**文档来源**: 七牛开发者中心 (https://developer.qiniu.com/kodo)

---

# 七牛云对象存储 Kodo 知识库

生成时间: 2025-11-15T07:19:32.775Z

---

## 1. 产品概述

七牛云对象存储 Kodo 是七牛云提供的高可靠、强安全、低成本、可扩展的存储服务。您可通过控制台、API、SDK 等方式简单快速地接入七牛存储服务，实现海量数据的存储和管理。

此外，Kodo 的姊妹产品融合 CDN可以对文件下载进行加速，智能多媒体 API更是提供了丰富的基于海量数据深度学习算法的计算机视觉服务，如人脸技术、场景物体识别等。

### 1.1 在线存储和分发

七牛云对象存储提供高可用和高可靠的对象存储服务，您可以放心的将各种内容存储在云端。利用七牛云对象存储的扩展性和按需付费的优势，可以满足您持续快速增长的存储需求。您也可以搭配使用七牛云的对象存储和融合 CDN服务，实现全球覆盖、快速高效的内容分发。

### 1.2 镜像存储

七牛云对象存储支持镜像存储，这是一种快速的数据迁移和加速服务。可以帮助您实现无缝数据迁移，迁移过程中并不影响原有业务系统的访问。镜像存储适用于迁移原有业务系统的已有数据。

### 1.3 备份和归档

七牛云对象存储提供高可用和高可靠的存储解决方案来备份和归档您的关键数据。通过七牛云的身份验证机制可以设置不同的访问权限和级别，保障您数据的访问安全。相比传统自建的备份和归档存储系统，您无需在业务初期采购高昂硬件，无需担心数据增长带来的扩容问题。

### 1.4 富媒体数据处理

针对海量的用户生成内容，七牛云对象存储能够提供跨地域、高并发的内容上传和访问服务。同时结合七牛云提供的数据处理服务，可以在云端实现图片裁剪、格式转化和水印，以及视频转码、切片和拼接等富媒体处理功能，满足移动网络场景下多终端设备的访问需求。

### 1.5 静态资源托管

七牛云对象存储无缝集合各类第三方扩展插件，如 WordPress、Discuz、Emlog 等，并支持一键将各类插件里的静态资源托管到七牛云对象存储。

---

## 2. 基本概念

### 2.1 空间（Bucket）

空间是对象存储中用于存储数据的容器，所有存储在对象存储上的数据都必须隶属于某一个空间。空间名在整个对象存储系统中具有唯一性，且创建后不可修改。

每个空间都有以下属性：
- 存储区域：空间创建时需要指定所属的存储区域，创建后不可修改
- 访问权限：公开空间或私有空间
- 存储类型：标准存储、低频存储、归档存储、深度归档存储等

### 2.2 资源（Object）

资源是对象存储中的基本存储单元，也称为对象或文件。资源由资源内容（Object Content）和资源元信息（Object Metadata）组成。

资源的特点：
- 资源名（Key）：在空间内唯一标识一个资源
- 资源内容：实际存储的数据内容
- 元信息：包括文件大小、MIME类型、自定义元信息等

### 2.3 存储区域（Region）

存储区域是对象存储服务的物理存储位置。七牛云在全球多个地域部署了存储服务，用户可以根据业务需求选择合适的存储区域。

选择存储区域的考虑因素：
- 地理位置：选择离用户最近的区域可以降低访问延迟
- 合规要求：某些行业或地区对数据存储位置有特定要求
- 价格差异：不同区域的存储和流量价格可能有所不同

### 2.4 访问密钥（Access Key）

访问密钥用于验证用户身份和权限，包括：
- AccessKey（AK）：公开的密钥标识
- SecretKey（SK）：私有的密钥，用于签名验证

AccessKey和SecretKey成对出现，用于生成访问凭证（Token）。用户需要妥善保管SecretKey，避免泄露。

---

## 3. 存储区域

存储区域（Region）是七牛云对象存储服务的物理存储位置。七牛云在全球多个地域部署了存储服务，用户可以根据业务需求选择合适的存储区域。

### 3.1 区域信息

七牛云对象存储目前支持以下存储区域：

| 存储区域 | Region ID | 域名 |
|---------|-----------|------|
| 华东-浙江 | z0 | 空间管理：http(s)://uc.qiniuapi.com 源站上传：http(s)://up-z0.qiniup.com源站下载：http(s)://iovip-z0.qiniuio.com 对象管理：http(s)://rs-z0.qiniuapi.com 对象列举：http(s)://rsf-z0.qiniuapi.com  计量查询：http(s)://api.qiniuapi.com |
| 华东-浙江2 | cn-east-2 | 空间管理：http(s)://uc.qiniuapi.com 源站上传：http(s)://up-cn-east-2.qiniup.com源站下载：http(s)://iovip-cn-east-2.qiniuio.com 对象管理：http(s)://rs-cn-east-2.qiniuapi.com 对象列举：http(s)://rsf-cn-east-2.qiniuapi.com计量查询：http(s)://api.qiniuapi.com |
| 华北-河北 | z1 | 空间管理：http(s)://uc.qiniuapi.com源站上传：http(s)://up-z1.qiniup.com 源站下载：http(s)://iovip-z1.qiniuio.com  对象管理：http(s)://rs-z1.qiniuapi.com 对象列举：http(s)://rsf-z1.qiniuapi.com  计量查询：http(s)://api.qiniuapi.com |
| 华南-广东 | z2 | 空间管理：http(s)://uc.qiniuapi.com 源站上传：http(s)://up-z2.qiniup.com源站下载：http(s)://iovip-z2.qiniuio.com 对象管理：http(s)://rs-z2.qiniuapi.com 对象列举：http(s)://rsf-z2.qiniuapi.com计量查询：http(s)://api.qiniuapi.com |
| 西北-陕西1 | cn-northwest-1 | 空间管理：http(s)://uc.qiniuapi.com 源站上传：http(s)://up-cn-northwest-1.qiniup.com源站下载：http(s)://iovip-cn-northwest-1.qiniuio.com 对象管理：http(s)://rs-cn-northwest-1.qiniuapi.com 对象列举：http(s)://rsf-cn-northwest-1.qiniuapi.com计量查询：http(s)://api-cn-northwest-1.qiniuapi.com |
| 北美-洛杉矶 | na0 | 空间管理：http(s)://uc.qiniuapi.com源站上传：http(s)://up-na0.qiniup.com源站下载：http(s)://iovip-na0.qiniuio.com  对象管理：http(s)://rs-na0.qiniuapi.com 对象列举：http(s)://rsf-na0.qiniuapi.com 计量查询：http(s)://api.qiniuapi.com |
| 亚太-新加坡（原东南亚） | as0 | 空间管理：http(s)://uc.qiniuapi.com 源站上传：http(s)://up-as0.qiniup.com源站下载：http(s)://iovip-as0.qiniuio.com 对象管理：http(s)://rs-as0.qiniuapi.com 对象列举：http(s)://rsf-as0.qiniuapi.com计量查询：http(s)://api.qiniuapi.com |
| 亚太-河内 | ap-southeast-2 | 空间管理：http(s)://uc.qiniuapi.com 源站上传：http(s)://up-ap-southeast-2.qiniup.com源站下载：http(s)://iovip-ap-southeast-2.qiniuio.com 对象管理：http(s)://rs-ap-southeast-2.qiniuapi.com 对象列举：http(s)://rsf-ap-southeast-2.qiniuapi.com计量查询：http(s)://api-ap-southeast-2.qiniuapi.com |
| 亚太-胡志明 | ap-southeast-3 | 空间管理：http(s)://uc.qiniuapi.com 源站上传：http(s)://up-ap-southeast-3.qiniup.com源站下载：http(s)://iovip-ap-southeast-3.qiniuio.com 对象管理：http(s)://rs-ap-southeast-3.qiniuapi.com 对象列举：http(s)://rsf-ap-southeast-3.qiniuapi.com计量查询：http(s)://api-ap-southeast-3.qiniuapi.com |

### 3.2 选择存储区域的考虑因素

1. **地理位置**：选择离用户最近的区域可以降低访问延迟，提升用户体验
2. **合规要求**：某些行业或地区对数据存储位置有特定的法律法规要求
3. **价格差异**：不同区域的存储和流量价格可能有所不同
4. **服务可用性**：某些特性可能在特定区域优先上线

### 3.3 注意事项

- 空间创建时需要指定所属的存储区域，创建后不可修改
- 不同区域的数据不能直接互通，需要通过数据迁移实现
- 访问域名需要根据存储区域选择对应的域名

---

## 4. API 概览

七牛云对象存储提供了完整的 RESTful API 接口，用于管理存储空间和对象。API 分为三大类：服务级接口、存储空间接口和对象接口。

### 4.1 API 分类

#### 4.1.1 服务级接口 (Service API)

服务级接口用于管理七牛云对象存储的全局资源和配置：

- **账号管理**：查询账号信息、配额、权限等
- **存储区域查询**：获取可用的存储区域列表
- **全局配置**：设置和查询全局配置参数

#### 4.1.2 存储空间接口 (Bucket API)

存储空间接口用于管理存储空间（Bucket）的生命周期和配置：

- **创建空间**：创建新的存储空间
- **删除空间**：删除已有的存储空间
- **列举空间**：列出账号下的所有存储空间
- **空间配置**：设置和查询空间的访问权限、生命周期规则、跨域配置等
- **域名管理**：绑定和管理自定义域名

#### 4.1.3 对象接口 (Object API)

对象接口用于管理存储空间中的对象（文件）：

- **上传对象**：支持简单上传、分片上传、断点续传等多种上传方式
- **下载对象**：支持简单下载、范围下载、流式下载等
- **删除对象**：删除单个或批量删除多个对象
- **列举对象**：列出空间中的对象列表
- **复制对象**：在同一空间或不同空间之间复制对象
- **移动对象**：移动或重命名对象
- **对象元信息**：查询和修改对象的元数据
- **对象标签**：为对象添加和管理标签

### 4.2 API 调用方式

七牛云对象存储 API 采用 RESTful 风格，支持标准的 HTTP/HTTPS 协议。

#### 4.2.1 请求结构

- **请求方法**：GET, POST, PUT, DELETE 等标准 HTTP 方法
- **请求 URL**：`https://<domain>/<path>?<query>`
- **请求头**：包含认证信息、内容类型等
- **请求体**：根据具体接口要求，可能包含 JSON、表单数据或二进制数据

#### 4.2.2 认证方式

七牛云 API 支持多种认证方式：

1. **管理凭证（Access Token）**：用于管理类操作，基于 AccessKey 和 SecretKey 生成
2. **上传凭证（Upload Token）**：用于上传操作，包含上传策略和签名
3. **下载凭证（Download Token）**：用于私有空间的下载操作

#### 4.2.3 响应格式

- **成功响应**：HTTP 状态码 200，响应体通常为 JSON 格式
- **错误响应**：HTTP 状态码 4xx 或 5xx，响应体包含错误码和错误信息

---

## 5. 上传策略详解

上传策略（Upload Policy）是七牛云对象存储中用于控制上传行为的重要机制。

#### 格式

Code example:
拷贝{    "scope":                          "<Bucket                   string>",    "isPrefixalScope":                <IsPrefixalScope          int>,    "deadline":                       <UnixTimestamp  

| 字段名 | 必填 | 说明 |
| --- | --- | --- |
| scope | 是 | 指定上传的目标资源空间 Bucket 和资源键 Key（最大为 750 字节）。有三种格式：<bucket>，表示允许用户上传文件到指定的 bucket。在这种格式下文件只能新增（分片上传 v1 版 需要指定 insertOnly 为 1 才是新增，否则也为覆盖上传），若已存在同名资源（且文件内容/etag不一致），上传会失败；若已存在资源的内容/etag一致，则上传会返回成功。 <bucket>:<key>，表示只允许用户上传指定 key 的文件。在这种格式下文件默认允许修改，若已存在同名资源则会被覆盖。如果只希望上传指定 key 的文件，并且不允许修改，那么可以将下面的 insertOnly 属性值设为 1。 <bucket>:<keyPrefix>，表示只允许用户上传指定以 keyPrefix 为前缀的文件，当且仅当 isPrefixalScope 字段为 1 时生效，isPrefixalScope 为 1 时无法覆盖上传。 |
| isPrefixalScope |  | 若为 1，表示允许用户上传以 scope 的 keyPrefix 为前缀的文件。 |
| deadline | 是 | 上传凭证有效截止时间。Unix时间戳，单位为秒。该截止时间为上传完成后，在七牛空间生成文件的校验时间，而非上传的开始时间，一般建议设置为上传开始时间 + 3600s，用户可根据具体的业务场景对凭证截止时间进行调整。 |
| insertOnly |  | 限定为新增语意。如果设置为非 0 值，则无论 scope 设置为什么形式，仅能以新增模式上传文件。 |
| endUser |  | 唯一属主标识。特殊场景下非常有用，例如根据 App-Client 标识给图片或视频打水印。 |
| returnUrl |  | Web 端文件上传成功后，浏览器执行 303 跳转的 URL。通常用于表单上传。文件上传成功后会跳转到 <returnUrl>?upload_ret=<queryString>，<queryString>包含 returnBody 内容。如不设置 returnUrl，则直接将 returnBody 的内容返回给客户端。 |
| returnBody |  | 上传成功后，自定义七牛云最终返回給上传端（在指定 returnUrl 时是携带在跳转路径参数中）的数据。支持魔法变量和自定义变量。returnBody 要求是合法的 JSON 文本。例如 {“key”: $(key), “hash”: $(etag), “w”: $(imageInfo.width), “h”: $(imageInfo.height)}。 |
| callbackUrl |  | 上传成功后，七牛云向业务服务器发送 POST 请求的 URL。必须是公网上可以正常进行 POST 请求并能成功响应的有效 URL。另外，为了给客户端有一致的体验，我们要求 callbackUrl 返回包 Content-Type 为 “application/json”，即返回的内容必须是合法的 JSON 文本。出于高可用的考虑，本字段允许设置多个 callbackUrl（用英文符号 ; 分隔），在前一个 callbackUrl 请求失败的时候会依次重试下一个 callbackUrl。一个典型例子是：http://<ip1>/callback;http://<ip2>/callback，并同时指定下面的 callbackHost 字段。在 callbackUrl 中使用 ip 的好处是减少对 dns 解析的依赖，可改善回调的性能和稳定性。指定 callbackUrl，必须指定 callbackbody，且值不能为空。 |
| callbackHost |  | 上传成功后，七牛云向业务服务器发送回调通知时的 Host 值。与 callbackUrl 配合使用，仅当设置了 callbackUrl 时才有效。 |
| callbackBody |  | 上传成功后，七牛云向业务服务器发送 Content-Type: application/x-www-form-urlencoded 的 POST 请求。业务服务器可以通过直接读取请求的 query 来获得该字段，支持魔法变量和自定义变量。callbackBody 要求是合法的 url query string。例如key=$(key)&hash=$(etag)&w=$(imageInfo.width)&h=$(imageInfo.height)。如果callbackBodyType指定为application/json，则callbackBody应为json格式，例如:{“key”:"$(key)",“hash”:"$(etag)",“w”:"$(imageInfo.width)",“h”:"$(imageInfo.height)"}。 |
| callbackBodyType |  | 上传成功后，七牛云向业务服务器发送回调通知 callbackBody 的 Content-Type。默认为 application/x-www-form-urlencoded，也可设置为 application/json。 |
| persistentType |  | 资源上传成功后触发执行预转持久化处理的任务类型。- 0 为普通任务，1 为闲时任务- 对于闲时任务的功能介绍、使用场景、定价，详见闲时任务策略说明。- 当前只有部分多媒体处理支持设置闲时任务，如下: 1. 普通转码（GPU 转码不支持）2. 锐智转码2.0（1.0 不支持闲时，如需使用请升级到 2.0）3. 音视频拼接4. 音视频分段5. 视频截图：视频单帧缩略图、视频采样缩略图、视频雪碧截图 |
| persistentOps |  | 资源上传成功后触发执行的持久化处理指令列表。每个指令是一个 API 规格字符串以;分隔，可以指定多个数据处理命令,如：avthumb/mp4|saveas/cWJ1Y2tldDpxa2V5;avthumb/flv|saveas/cWJ1Y2tldDpxa2V5Mg==，是将上传的视频文件同时转码成mp4格式和flv格式后另存。fileType=2或3（上传归档存储或深度归档存储文件）时，不支持使用该参数。支持魔法变量和自定义变量。注意： persistentOps  和 persistentWorkflowTemplateID 两个参数只能二选一。 |
| persistentWorkflowTemplateID |  | 资源上传成功后指定工作流模板即可执行媒体处理操作。工作流模板是预先编排好的一系列媒体处理流程（如转码、截图、视频拼接等各类处理），登录 对象存储控制台 ，选择具体空间后，进行创建，详情参考工作流模板操作指南，persistentWorkflowTemplateID 对应工作流模板列表的名称字段，只支持 V1 工作流版本。注意：  persistentWorkflowTemplateID 和 persistentOps  两个参数只能二选一。 |

使用说明：

- Key 必须采用 utf-8 编码，使用非 utf-8 编码的资源名访问时会报错。
- callbackUrl 与 callbackBody 配合使用，returnUrl 与 returnBody 配合使用，callbackXXX 与 returnXXX 不可混用。当同时设置 returnUrl 和 callbackUrl 字段时，优先启用 callbackUrl 回调并返回 callbackBody，更多详情请见自定义响应。
- 文件上传后的命名将遵循以下规则：

源 Bucket 和目标 Bucket 必须在同一区域，即处理结果不能跨区域另存。
forceSaveKey=false，以客户端指定的 Key 为高优先级命名

客户端已指定 Key，以 Key 命名
客户端未指定 Key，上传策略中设置了 saveKey，以 saveKey 的格式命名。
客户端未指定 Key，上传策略中未设置 saveKey，以文件 hash(etag) 命名。


forceSaveKey=true，以上传策略中的 saveKey 为高优先级命名；此时上传策略中的 saveKey 不允许为空

客户端已指定 Key，以上传策略中 saveKey 的格式命名
客户端未指定 Key，以上传策略中 saveKey 的格式命名
- 源 Bucket 和目标 Bucket 必须在同一区域，即处理结果不能跨区域另存。
- forceSaveKey=false，以客户端指定的 Key 为高优先级命名

客户端已指定 Key，以 Key 命名
客户端未指定 Key，上传策略中设置了 saveKey，以 saveKey 的格式命名。
客户端未指定 Key，上传策略中未设置 saveKey，以文件 hash(etag) 命名。
- 客户端已指定 Key，以 Key 命名
- 客户端未指定 Key，上传策略中设置了 saveKey，以 saveKey 的格式命名。
- 客户端未指定 Key，上传策略中未设置 saveKey，以文件 hash(etag) 命名。
- forceSaveKey=true，以上传策略中的 saveKey 为高优先级命名；此时上传策略中的 saveKey 不允许为空

客户端已指定 Key，以上传策略中 saveKey 的格式命名
客户端未指定 Key，以上传策略中 saveKey 的格式命名
- 客户端已指定 Key，以上传策略中 saveKey 的格式命名
- 客户端未指定 Key，以上传策略中 saveKey 的格式命名
- 文件分片上传的创建文件步骤中。若未指定 Key，为达到不覆盖同名资源效果，必须使用 insertOnly 字段。

- 源 Bucket 和目标 Bucket 必须在同一区域，即处理结果不能跨区域另存。
- forceSaveKey=false，以客户端指定的 Key 为高优先级命名

客户端已指定 Key，以 Key 命名
客户端未指定 Key，上传策略中设置了 saveKey，以 saveKey 的格式命名。
客户端未指定 Key，上传策略中未设置 saveKey，以文件 hash(etag) 命名。
- 客户端已指定 Key，以 Key 命名
- 客户端未指定 Key，上传策略中设置了 saveKey，以 saveKey 的格式命名。
- 客户端未指定 Key，上传策略中未设置 saveKey，以文件 hash(etag) 命名。
- forceSaveKey=true，以上传策略中的 saveKey 为高优先级命名；此时上传策略中的 saveKey 不允许为空

客户端已指定 Key，以上传策略中 saveKey 的格式命名
客户端未指定 Key，以上传策略中 saveKey 的格式命名
- 客户端已指定 Key，以上传策略中 saveKey 的格式命名
- 客户端未指定 Key，以上传策略中 saveKey 的格式命名

- 客户端已指定 Key，以 Key 命名
- 客户端未指定 Key，上传策略中设置了 saveKey，以 saveKey 的格式命名。
- 客户端未指定 Key，上传策略中未设置 saveKey，以文件 hash(etag) 命名。

- 客户端已指定 Key，以上传策略中 saveKey 的格式命名
- 客户端未指定 Key，以上传策略中 saveKey 的格式命名

#### persistentOps 详解

persistentOps 字段用于指定预转数据处理命令和保存处理结果的存储空间与资源名。在上传归档存储或深度归档存储文件（fileType=2或3）时，不支持使用该字段。

为此字段指定非空值，则在成功上传一个文件后，会启动一个异步数据处理任务。persistentId 字段，唯一标识此任务。
当 returnBody 中指定了 persistentId 魔法变量时，客户端收到的响应内容 returnBody 中会有 persistentId；当没有指定 returnBody 时，默认也会返回 persistentId。

- 使用默认的存储空间和资源名
当只指定了数据处理命令时，服务端会选择上传文件的 Bucket 作为数据处理结果的存储空间，Key 由七牛服务器自动生成。
- 使用指定的存储空间和资源名
在数据处理命令后用管道符|拼接saveas/<encodedEntryURI>指令，指示七牛服务器使用EncodedEntryURI格式中指定的 Bucket 与 Key 来保存处理结果（需要注意的是，如果指定的 Bucket 中存在同 Key 的文件将会被处理结果覆盖）。如 avthumb/flv|saveas/cWJ1Y2tldDpxa2V5，是将上传的视频文件转码 flv 格式后存储为qbucket:qkey，其中cWJ1Y2tldDpxa2V5是qbucket:qkey的URL安全的Base64编码结果。以上方式可以同时作用于多个数据处理命令，用;分隔，如 avthumb/mp4|saveas/cWJ1Y2tldDpxa2V5;avthumb/flv|saveas/cWJ1Y2tldDpxa2V5Mg==

使用默认的存储空间和资源名

当只指定了数据处理命令时，服务端会选择上传文件的 Bucket 作为数据处理结果的存储空间，Key 由七牛服务器自动生成。

使用指定的存储空间和资源名

在数据处理命令后用管道符|拼接saveas/<encodedEntryURI>指令，指示七牛服务器使用EncodedEntryURI格式中指定的 Bucket 与 Key 来保存处理结果（需要注意的是，如果指定的 Bucket 中存在同 Key 的文件将会被处理结果覆盖）。如 avthumb/flv|saveas/cWJ1Y2tldDpxa2V5，是将上传的视频文件转码 flv 格式后存储为qbucket:qkey，其中cWJ1Y2tldDpxa2V5是qbucket:qkey的URL安全的Base64编码结果。以上方式可以同时作用于多个数据处理命令，用;分隔，如 avthumb/mp4|saveas/cWJ1Y2tldDpxa2V5;avthumb/flv|saveas/cWJ1Y2tldDpxa2V5Mg==

#### 示例

persistentOps与persistentNotifyUrl字段

上传一个视频资源，并在成功后触发两个预转处理（转成 mp4 资源和对原资源进行 HLS 切片）：

Code example:
拷贝{    "scope":                "qiniu-ts-demo",    "deadline":             1390528576,    "persistentOps":        "avthumb/mp4;avthumb/m3u8/noDomain/1/segtime/15/vb/440k",    "persistentNotifyUrl":  "

关于 avthumb 接口的详细信息请参阅音视频转码。

## 6. 数据处理（持久化处理）

七牛云对象存储支持在文件上传后自动触发数据处理操作，如音视频转码、图片处理、文档转换等。这些操作通过上传策略中的 persistentOps 字段配置。

### 6.1 持久化处理概述

持久化处理（Persistent Processing）是指在文件上传成功后，自动执行预定义的数据处理操作。处理结果会保存为新文件，不影响原始文件。

#### 6.1.1 主要特点

- 异步处理：上传完成后立即返回，处理在后台进行
- 多任务支持：可同时触发多个处理任务
- 结果通知：处理完成后可通过回调通知
- 自动保存：处理结果自动保存到指定空间

### 6.2 配置方式

在上传策略中配置 persistentOps 字段：

JSON示例：
{
  "scope": "my-bucket",
  "deadline": 1234567890,
  "persistentOps": "avthumb/mp4/vb/1m|saveas/encoded-bucket:result.mp4",
  "persistentNotifyUrl": "https://api.example.com/notify"
}

### 6.3 常用处理命令

#### 6.3.1 音视频转码（avthumb）

- 格式转换：avthumb/mp4、avthumb/flv
- 码率控制：/vb/1m（视频码率1Mbps）、/ab/128k（音频码率128kbps）
- 分辨率调整：/s/1280x720（设置分辨率）
- 帧率设置：/r/30（设置帧率为30fps）

#### 6.3.2 图片处理（imageView2、imageMogr2）

- 缩放：imageView2/1/w/300/h/200
- 裁剪：imageMogr2/crop/300x200
- 旋转：imageMogr2/rotate/90
- 水印：watermark/1/image/...

#### 6.3.3 文档转换（yifangyun）

- PDF转图片：yifangyun/v1/pdf/page/1
- Office文档预览：yifangyun/v1/preview

### 6.4 处理结果保存

使用 saveas 指令指定处理结果的保存位置：

格式：saveas/<EncodedEntryURI>

其中 EncodedEntryURI 是 URL安全的Base64编码，格式为：bucket:key

示例：
avthumb/mp4|saveas/bXktYnVja2V0OnJlc3VsdC5tcDQ=

### 6.5 处理状态查询

持久化处理任务会返回 persistentId，可通过此ID查询处理状态：

GET /status/get/prefop?id=<persistentId>

返回信息包括：
- 处理状态（0=等待，1=处理中，2=成功，3=失败）
- 处理进度
- 错误信息（如果失败）
- 处理结果的存储位置

## 7. 下载与访问控制

七牛云对象存储提供灵活的下载和访问控制机制，支持公开访问和私有访问两种模式。

### 7.1 访问模式

#### 7.1.1 公开空间

公开空间中的文件可以通过外链直接访问，无需鉴权。适用于：
- 静态网站资源（CSS、JS、图片）
- 公开的媒体内容
- 需要CDN加速的公开文件

访问格式：http(s)://<domain>/<key>

#### 7.1.2 私有空间

私有空间中的文件需要通过下载凭证（Download Token）访问，提供更高的安全性。适用于：
- 用户私密数据
- 付费内容
- 需要访问控制的文件

### 7.2 下载凭证（Download Token）

下载凭证是访问私有空间文件的凭证，由服务端生成。

#### 7.2.1 生成方式

1. 构造下载URL：http(s)://<domain>/<key>?e=<deadline>
2. 使用SecretKey对URL进行HMAC-SHA1签名
3. 将签名进行URL安全的Base64编码
4. 附加到URL：原URL&token=<AccessKey>:<EncodedSign>

#### 7.2.2 有效期控制

通过 e 参数（Unix时间戳）控制下载链接的有效期：
- 短期访问：e = 当前时间 + 3600（1小时）
- 长期访问：e = 当前时间 + 86400*7（7天）
- 永久访问：不设置e参数（不推荐）

### 7.3 防盗链

七牛云支持多种防盗链机制：

#### 7.3.1 Referer防盗链

- 白名单模式：只允许指定域名访问
- 黑名单模式：禁止指定域名访问
- 支持通配符：*.example.com

#### 7.3.2 IP防盗链

- 限制特定IP或IP段访问
- 支持CIDR格式：192.168.1.0/24

#### 7.3.3 时间戳防盗链

- 通过URL中的时间戳参数控制访问有效期
- 配合签名机制防止篡改

### 7.4 断点续传下载

七牛云支持HTTP Range请求，实现断点续传：

请求头示例：
Range: bytes=0-1023  （下载前1024字节）
Range: bytes=1024-   （从1024字节开始下载到结束）

响应头：
Content-Range: bytes 0-1023/102400
Content-Length: 1024

### 7.5 CDN加速

七牛云对象存储与CDN深度集成：

- 自动CDN分发：上传后自动同步到CDN节点
- 智能调度：根据用户位置选择最近节点
- 缓存控制：支持自定义Cache-Control头
- 预取功能：主动将热点内容推送到边缘节点

### 7.6 下载统计

可通过API查询下载统计信息：

- 下载次数
- 下载流量
- 按时间维度统计（小时、天、月）
- 按文件维度统计

## 8. 存储区域与访问域名

七牛云对象存储在全球多个区域部署，每个区域有独立的API端点和CDN加速域名。

### 8.1 存储区域列表

七牛云目前支持以下存储区域：

#### 8.1.1 中国大陆区域

| 区域名称 | 区域标识 | 服务端点 |
| --- | --- | --- |
| 华东-浙江 | z0 | iovip.qbox.me |
| 华北-河北 | z1 | iovip-z1.qbox.me |
| 华南-广东 | z2 | iovip-z2.qbox.me |
| 北美-洛杉矶 | na0 | iovip-na0.qbox.me |
| 亚太-新加坡 | as0 | iovip-as0.qbox.me |

#### 8.1.2 区域选择建议

- 就近原则：选择距离主要用户最近的区域
- 合规要求：根据数据合规要求选择区域
- 成本考虑：不同区域价格可能有差异
- 容灾备份：可在多个区域创建空间实现异地容灾

### 8.2 API端点

不同API操作使用不同的端点域名：

#### 8.2.1 上传端点

- 华东：upload.qiniup.com 或 up.qiniup.com
- 华北：upload-z1.qiniup.com 或 up-z1.qiniup.com
- 华南：upload-z2.qiniup.com 或 up-z2.qiniup.com
- 北美：upload-na0.qiniup.com 或 up-na0.qiniup.com
- 亚太：upload-as0.qiniup.com 或 up-as0.qiniup.com

#### 8.2.2 资源管理端点

- 华东：rs.qbox.me
- 华北：rs-z1.qbox.me
- 华南：rs-z2.qbox.me
- 北美：rs-na0.qbox.me
- 亚太：rs-as0.qbox.me

#### 8.2.3 列举端点

- 华东：rsf.qbox.me
- 华北：rsf-z1.qbox.me
- 华南：rsf-z2.qbox.me
- 北美：rsf-na0.qbox.me
- 亚太：rsf-as0.qbox.me

### 8.3 访问域名

#### 8.3.1 默认域名

创建空间后，七牛云会自动分配一个测试域名：
- 格式：<bucket>.clouddn.com
- 有效期：30天（仅供测试）
- 限制：带宽限制、不支持HTTPS

#### 8.3.2 自定义域名

生产环境建议绑定自定义域名：
1. 添加域名到空间
2. 配置CNAME记录指向七牛CDN
3. 等待DNS生效（通常5-10分钟）
4. 配置HTTPS证书（可选但推荐）

#### 8.3.3 HTTPS配置

七牛云支持免费HTTPS证书：
- 自动申请Let's Encrypt证书
- 自动续期
- 也可上传自有证书
- 支持HTTP/2协议

### 8.4 跨区域访问

#### 8.4.1 镜像存储

配置镜像源后，访问不存在的文件时自动从源站抓取：
- 首次访问从源站获取
- 自动保存到七牛云
- 后续访问直接从七牛云返回

#### 8.4.2 跨区域复制

可配置自动同步到其他区域：
- 异地容灾
- 就近访问
- 负载均衡

## 9. 最佳实践与使用建议

基于七牛云对象存储的特性和实际使用经验，以下是一些重要的最佳实践建议。

### 9.1 命名规范

#### 9.1.1 空间命名

- 使用小写字母和数字
- 避免使用特殊字符
- 建议格式：项目名-环境-用途（如：myapp-prod-images）
- 不同环境使用不同空间（开发、测试、生产）

#### 9.1.2 文件Key命名

- 使用有意义的路径结构：category/date/filename
- 避免中文和特殊字符（使用URL编码）
- 添加时间戳或UUID避免冲突
- 示例：images/2025/11/user123_1731654214_avatar.jpg

### 9.2 安全实践

#### 9.2.1 密钥管理

- 永远不要在客户端代码中硬编码AccessKey/SecretKey
- 使用环境变量或密钥管理服务存储密钥
- 定期轮换密钥
- 为不同应用创建不同的密钥对

#### 9.2.2 上传凭证

- 在服务端生成上传凭证，客户端只负责上传
- 设置合理的过期时间（建议1小时）
- 使用returnBody限制返回内容
- 配置上传策略限制文件大小和类型

#### 9.2.3 访问控制

- 敏感数据使用私有空间
- 配置防盗链保护资源
- 使用时间戳防盗链限制访问时效
- 定期审计访问日志

### 9.3 性能优化

#### 9.3.1 上传优化

- 大文件（>4MB）使用分片上传
- 启用断点续传避免重复上传
- 使用并发上传提高速度
- 选择就近的存储区域

#### 9.3.2 下载优化

- 绑定自定义CDN域名
- 使用图片处理API生成缩略图
- 配置合理的缓存策略
- 使用预取功能提前推送热点内容

#### 9.3.3 列举优化

- 使用前缀和分隔符组织文件
- 避免频繁列举大量文件
- 使用marker实现分页
- 考虑在应用层维护文件索引

### 9.4 成本优化

#### 9.4.1 存储成本

- 定期清理不需要的文件
- 使用生命周期规则自动删除过期文件
- 低频访问数据使用低频存储
- 归档数据使用归档存储

#### 9.4.2 流量成本

- 使用CDN减少回源流量
- 配置合理的缓存时间
- 使用图片处理生成适当尺寸
- 避免不必要的大文件传输

#### 9.4.3 请求成本

- 减少不必要的API调用
- 使用批量操作接口
- 在应用层实现缓存
- 避免频繁的列举操作

### 9.5 可靠性保障

#### 9.5.1 数据备份

- 重要数据启用跨区域复制
- 定期导出关键数据到本地
- 使用版本控制保护误删除
- 配置生命周期规则自动备份

#### 9.5.2 容灾方案

- 在多个区域部署存储空间
- 使用DNS负载均衡实现故障切换
- 配置镜像存储作为备份源
- 定期演练容灾切换流程

#### 9.5.3 监控告警

- 监控存储容量使用情况
- 监控流量和请求量
- 设置异常访问告警
- 监控上传失败率

### 9.6 开发建议

#### 9.6.1 SDK使用

- 优先使用官方SDK而非直接调用API
- 保持SDK版本更新
- 正确处理SDK返回的错误
- 参考SDK示例代码

#### 9.6.2 错误处理

- 实现重试机制（指数退避）
- 记录详细的错误日志
- 对用户友好的错误提示
- 监控错误率并及时处理

#### 9.6.3 测试

- 使用测试空间进行开发测试
- 测试各种边界情况
- 进行压力测试验证性能
- 测试容灾切换流程

## 10. 常见问题与故障排查

在使用七牛云对象存储过程中，可能会遇到一些常见问题。本节提供问题诊断和解决方案。

### 10.1 上传相关问题

#### 10.1.1 上传失败

**问题现象**：文件上传返回错误或超时

**可能原因及解决方案**：

1. **上传凭证过期**
   - 检查凭证生成时间和deadline参数
   - 确保服务器时间准确（使用NTP同步）
   - 建议凭证有效期设置为1小时

2. **上传凭证错误**
   - 验证AccessKey和SecretKey是否正确
   - 检查上传策略JSON格式是否正确
   - 确认scope参数格式：bucket或bucket:key

3. **网络问题**
   - 检查网络连接是否稳定
   - 尝试使用不同的上传域名
   - 大文件使用分片上传并启用断点续传

4. **文件大小限制**
   - 表单上传限制1GB
   - 分片上传单个块限制4MB
   - 检查上传策略中的fsizeLimit设置

#### 10.1.2 上传速度慢

**优化方案**：

- 选择地理位置最近的存储区域
- 使用分片并发上传
- 检查本地网络带宽
- 避免在高峰时段上传

#### 10.1.3 回调失败

**问题现象**：上传成功但回调未触发

**排查步骤**：

1. 检查callbackUrl是否可公网访问
2. 验证回调服务器是否正常响应
3. 检查回调请求的Authorization头
4. 查看七牛云控制台的回调日志

### 10.2 下载相关问题

#### 10.2.1 403 Forbidden

**私有空间**：
- 检查下载凭证是否正确生成
- 验证凭证是否过期
- 确认AccessKey是否有权限

**公开空间**：
- 检查防盗链配置
- 验证Referer是否在白名单
- 检查IP是否被限制

#### 10.2.2 404 Not Found

**排查步骤**：

1. 确认文件key是否正确（区分大小写）
2. 检查文件是否已被删除
3. 验证空间名称是否正确
4. 使用资源管理API查询文件是否存在

#### 10.2.3 下载速度慢

**优化方案**：

- 绑定CDN加速域名
- 检查CDN缓存配置
- 使用图片处理生成合适尺寸
- 考虑使用预取功能

### 10.3 API调用问题

#### 10.3.1 401 Unauthorized

**常见原因**：

1. **签名错误**
   - 检查AccessKey和SecretKey
   - 验证签名算法实现
   - 确认请求头Content-Type是否正确

2. **时间不同步**
   - 服务器时间与标准时间差异超过15分钟
   - 使用NTP同步时间

#### 10.3.2 614 File Exists

**问题说明**：文件已存在且未指定覆盖

**解决方案**：
- 修改文件key使用唯一标识
- 在上传策略中添加insertOnly:0允许覆盖
- 先删除旧文件再上传

#### 10.3.3 631 Bucket Not Exists

**排查步骤**：

1. 确认空间名称拼写正确
2. 检查空间是否已创建
3. 验证AccessKey是否有该空间权限
4. 确认使用正确的存储区域端点

### 10.4 性能问题

#### 10.4.1 列举操作慢

**问题原因**：空间文件数量过多

**优化方案**：

- 使用prefix参数缩小范围
- 减少limit参数值
- 在应用层维护文件索引
- 使用delimiter组织文件结构

#### 10.4.2 批量操作超时

**解决方案**：

- 减少单次批量操作的数量
- 使用异步处理
- 增加超时时间设置
- 实现重试机制

### 10.5 账单异常

#### 10.5.1 流量费用过高

**排查步骤**：

1. 检查是否有异常访问（查看访问日志）
2. 确认CDN缓存配置是否合理
3. 检查是否有大文件被频繁下载
4. 验证防盗链配置是否生效

**优化建议**：

- 配置合理的缓存时间
- 启用防盗链保护
- 使用图片处理减小文件大小
- 监控异常流量并设置告警

#### 10.5.2 存储费用过高

**优化方案**：

- 清理不需要的文件
- 使用生命周期规则自动删除过期文件
- 低频访问数据迁移到低频存储
- 归档数据使用归档存储

### 10.6 调试技巧

#### 10.6.1 使用日志

- 启用SDK的调试日志
- 记录完整的请求和响应
- 保存错误信息和堆栈
- 使用日志分析工具

#### 10.6.2 使用开发者工具

- 浏览器开发者工具查看网络请求
- 使用curl命令测试API
- 使用Postman测试接口
- 查看七牛云控制台的操作日志

#### 10.6.3 联系技术支持

提交工单时提供：
- 完整的错误信息
- 请求ID（X-Reqid响应头）
- 发生时间
- 相关代码片段
- SDK版本信息

### 10.7 常用诊断命令

#### 10.7.1 测试上传

curl命令示例：
curl -X POST http://upload.qiniup.com/ -F file=@test.jpg -F token=<upload_token>

#### 10.7.2 测试下载

curl -I http://<domain>/<key>
检查响应头中的状态码和Content-Type

#### 10.7.3 验证签名

使用七牛云提供的签名验证工具：
https://portal.qiniu.com/tools/signature


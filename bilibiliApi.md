# 哔哩哔哩视频信息获取相关 api

## 获取视频信息

**接口地址：**

> https://api.bilibili.com/x/player/playurl

**请求参数：**

| 请求参数 | 必选 | 说明       |
| -------- | ---- | ---------- |
| bvid     | 是   | 视频 bv 号 |
| cid      | 是   |
| fnval    | 是   |

**返回参数（部分数据, 以下为 data.dash 内数据）：**

| 返回参数 | 参数类型 | 说明             |
| -------- | -------- | ---------------- |
| duration | number   | 时长             |
| video    | array    | 视频播放路径信息 |
| audio    | array    | 视频播放路径信息 |

<br />

> **_video/audio_**

| 名称       | 类型   | 说明                 |
| ---------- | ------ | -------------------- |
| id         | number | 资源品质 id          |
| baseUrl    | number | 播放路径             |
| base_url   | string | 播放路径             |
| backupUrl  | string | 播放路径, 一般有两个 |
| backup_url | array  | 播放路径, 一般有两个 |
| mimeType   | string | 文件类型             |

**返回示例（部分数据）：**

```js
{
    "code": 0,
    "message": "0",
    "data": {
        "timelength": 137087,
        "accept_format": "hdflv2,flv,flv720,flv480,mp4",
        "accept_description": [
            "高清 1080P+",
            "高清 1080P",
            "高清 720P",
            "清晰 480P",
            "流畅 360P"
        ],
        "accept_quality": [
            112,
            80,
            64,
            32,
            16
        ],
        "dash": {
            "duration": 138,
            "minBufferTime": 1.5,
            "min_buffer_time": 1.5,
            "video": [
                {
                    "id": 32,
                    "baseUrl": "http://xxxx",
                    "base_url": "http://xxxx",
                    "backupUrl": [
                        "http://xxxx",
                        "http://xxx"
                    ],
                    "backup_url": [
                        "http://xxxx",
                        "http://xxx"
                    ],
                    "bandwidth": 788205,
                    "mimeType": "video/mp4",
                    "mime_type": "video/mp4",
                    "codecs": "avc1.64001F",
                    "codecid": 7
                }
            ]
            "audio": [
                {
                    "id": 30280,
                    "baseUrl": "http://xxx",
                    "base_url": "http://xxx",
                    "backupUrl": [
                        "http://xxx",
                        "http://xxx"
                    ],
                    "backup_url": [
                        "http://xxx",
                        "http://xxx"
                    ],
                    "bandwidth": 319170,
                    "mimeType": "audio/mp4",
                    "mime_type": "audio/mp4",
                    "codecs": "mp4a.40.2",
                    "codecid": 0
                }
            ]
        }
    }
}
```

## 获取视频 cid

**接口地址：**

> https://api.bilibili.com/x/player/pagelist

**请求参数：**

| 请求参数 | 必选 | 说明       |
| -------- | ---- | ---------- |
| bvid     | 是   | 视频 bv 号 |

**返回参数（部分数据, 以下为 data 内数据）：**

| 返回参数    | 参数类型 | 说明           |
| ----------- | -------- | -------------- |
| cid         | number   | 视频 cid       |
| part        | string   | 视频标题       |
| duration    | number   | 视频时长       |
| first_frame | string   | 视频第一帧画面 |

**返回示例（部分数据）：**

```js
{
    "code": 0,
    "message": "0",
    "data": [
        {
            "cid": 0,
            "part": "标题",
            "duration": 138,
            "first_frame": "http://xxx.jpg"
        }
    ]
}
```

## 关键字搜索

**接口地址：**

> http://api.bilibili.com/x/web-interface/search/all/v2

**说明**

使用此 api 需要传递指定 cookie，否则可能会被拦截，cookie 获取方式见[搜索 api 所需 cookie](#搜索-api-所需-cookie)。

登录用户和未登录用户的搜索结果不同。

**请求参数：**

| 请求参数  | 必选 | 说明                 |
| --------- | ---- | -------------------- |
| page      | 否   | 搜索结果页数         |
| page_size | 否   | 搜索结果一页的数据量 |
| keyword   | 是   | 搜索关键字           |

**参数 search_type 已知可选值**：

| 名称          | 说明     |
| ------------- | -------- |
| bili_user     | 用户     |
| topic         | 话题     |
| live          | 直播     |
| video         | 视频     |
| media_ft      | 影视     |
| article       | 专栏     |
| media_bangumi | 番剧     |
| live_user     | 直播用户 |

**返回参数（部分数据, 以下为 data 内数据）：**

| 返回参数   | 参数类型 | 说明                                                  |
| ---------- | -------- | ----------------------------------------------------- |
| page       | number   | 当前页                                                |
| pagesize   | number   | 一页数据量                                            |
| numResults | number   | 数据量                                                |
| numPages   | number   | 页数                                                  |
| pageinfo   | object   | 不同类型的搜索结果数据量, 携带 search_type 时不会出现 |
| top_tlist  | object   | 不同类型的搜索结果数据量, 携带 search_type 时不会出现 |
| result     | object   | 不同类型的搜索结果数据量                              |

<br />

**_top_tlist（部分数据）_**

| 名称          | 类型   | 说明                     |
| ------------- | ------ | ------------------------ |
| bili_user     | number | 关键字匹配`用户`数据量数 |
| topic         | number | 关键字匹配`话题`数据量   |
| live          | number | 关键字匹配`直播`数据量   |
| video         | number | 关键字匹配`视频`数据量   |
| media_ft      | number | 关键字匹配`影视`数据量   |
| article       | number | 关键字匹配`专栏`数据量   |
| media_bangumi | number | 关键字匹配`番剧`数据量   |

<br />

> **_result_**

| 名称 | 类型   | 说明             |
| ---- | ------ | ---------------- |
| type | string | 数据类型         |
| data | array  | 具体结果信息对象 |

<br />

> **_result.data（部分数据）_**

| 名称        | 类型   | 说明                             |
| ----------- | ------ | -------------------------------- |
| type        | string | 数据类型                         |
| id          | number | 视频 aid                         |
| aid         | number | 视频 aid                         |
| typeid      | number | 视频类型 id                      |
| typename    | string | 视频类型名称                     |
| author      | string | up 主名称                        |
| arcurl      | string | 视频网页 url                     |
| bvid        | string | 视频 bv 号                       |
| title       | string | 视频标题, 关键字使用 em 标签包裹 |
| description | string | 视频简介                         |
| pic         | string | 视频封面图 url                   |
| play        | number | 视频播放数                       |
| favorites   | number | 视频收藏数                       |
| tag         | string | 视频 tag, 逗号分隔               |
| review      | number | 视频评论数                       |
| pubdate     | number | 视频发布时间, 精确到秒           |
| duration    | string | 视频时长                         |
| like        | string | 视频点赞数                       |
| upic        | string | up 主头像图片 url                |
| danmaku     | string | 视频弹幕数                       |

<br />

**返回示例（部分数据）：**

```js
{
    "code": 0,
    "message": "0",
    "data": {
        "page": 1,
        "pagesize": 20,
        "numResults": 1000,
        "numPages": 50,
        "pageinfo": {
            "video": {
                "numResults": 1000,
                "total": 1000,
                "pages": 50
            },
            "user": {
                "numResults": 0,
                "total": 0,
                "pages": 0
            },
        },
        "top_tlist": {
            "bili_user": 1000,用户
            "topic": 7,话题
            "live": 30,直播
            "video": 1000,视频
            "media_ft": 26,影视
            "article": 754,专栏
            "media_bangumi": 36,番剧
        },
         "result": [
            {
                "result_type": "tips",
                "data": []
            },
            {
                "result_type": "video",
                "data": [
                    {
                        "type": "video",类型
                        "id": 0,视频aid
                        "author": "",up主名称
                        "typeid": "28",
                        "typename": "原创音乐",视频类型名称
                        "arcurl": "http://www.bilibili.com/video/xxx",视频路径
                        "aid": 0,视频aid
                        "bvid": "BV1xxx",视频bv号
                        "title": "标题<em class=\"keyword\">关键字</em>",标题, 关键字使用em标签包裹
                        "description": "",视频简介
                        "pic": "http://xxx.jpg",封面
                        "play": 1563032,播放数
                        "favorites": 68068,收藏数
                        "tag": "tag1,tag2,tag3",视频tag
                        "review": 4097,评论
                        "pubdate": 1657513200,发布时间
                        "duration": "2:18",时长
                        "like": 204270,点赞数
                        "upic": "http://xxx.jpg",up主头像
                        "danmaku": 2528,弹幕数
                    }
                ]
            }
        ]
    }
}
```

## 关键字+类型搜索

**接口地址：**

> https://api.bilibili.com/x/web-interface/search/type

| 请求参数    | 必选 | 说明                 |
| ----------- | ---- | -------------------- |
| page        | 否   | 搜索结果页数         |
| page_size   | 否   | 搜索结果一页的数据量 |
| keyword     | 是   | 搜索关键字           |
| search_type | 是   | 搜索关键字           |

**参数 search_type 已知可选值**：[`video`, `bili_user`, `topic`, `media_ft`, `article`, `media_bangumi`]

**返回参数（省略部分信息, 以下为 data 内数据）：**

| 返回参数   | 参数类型 | 说明         |
| ---------- | -------- | ------------ |
| page       | number   | 当前页       |
| pagesize   | number   | 一页数据量   |
| numResults | number   | 数据量       |
| numPages   | number   | 页数         |
| result     | array    | 搜索结果数据 |

<br />

> **_result（不同类型有不同字段信息，以下为用户类型结果字段）_**

| 名称             | 类型   | 说明                       |
| ---------------- | ------ | -------------------------- |
| type             | string | 数据类型                   |
| uname            | string | 用户名称                   |
| usign            | string | 用户简介                   |
| fans             | number | 粉丝数                     |
| videos           | number | 发布视频数                 |
| level            | number | 用户等级                   |
| gender           | number | 1 男，2 女，3 未知         |
| is_upuser        | number | 是否为 up 主，1 是，0 否   |
| is_live          | number | 是否正在直播，1 是，0 否   |
| room_id          | number | 直播房间 id                |
| official_verify  | object | 小闪电信息                 |
| face_nft         | number | 是否有 nft，1 有，0 无     |
| face_nft_type    | number | nft 类型，目前已知有 1、2  |
| is_senior_member | number | 是否是资深会员，1 是，0 否 |
| res              | array  | 发布的视频信息             |

<br />

> **_official_verify_**

| 名称 | 类型   | 说明                                                       |
| ---- | ------ | ---------------------------------------------------------- |
| type | number | 标记类型，1 是蓝色小闪电，0 是黄色小闪电，127 是没有小闪电 |
| desc | string | 小闪电说明文字                                             |

**返回参数（部分数据）：**

```js
{
    "code": 0,
    "message": "0",
    "ttl": 1,
    "data": {
        "page": 1,
        "pagesize": 20,
        "numResults": 36,
        "numPages": 2,
        "result": [
            {

                "type": "bili_user",
                "mid": 0,
                "uname": "",
                "usign": "",
                "fans": 40,
                "videos": 0,
                "upic": "http://www.gif",
                "face_nft": 0,
                "face_nft_type": 0,
                "level": 4,
                "gender": 3,
                "is_upuser": 0,
                "is_live": 0,
                "room_id": 0,
                "res": [],
                "official_verify": {
                    "type": 127,
                    "desc": ""
                },
                "is_senior_member": 0
            }
        ]
    }
}

```

## 搜索 api 所需 cookie

**接口地址：**

> https://api.bilibili.com/x/frontend/finger/spi

**请求参数：** 无

**返回参数（以下为 data 内数据）：**

| 返回参数 | 参数类型 | 说明                           |
| -------- | -------- | ------------------------------ |
| b_3      | string   | 使用搜索 api 需要携带的 cookie |
| b_4      | string   |                                |

**返回示例（省略部分信息）：**

```js
{
    "code": 0,
    "data": {
        "b_3": "51AB8234-A561-5B51-6888-01E2Cfoc",
        "b_4": "7CA2F9DF-9353-EC50-C0A1-56F44730-023-o/FdW6FI6g=="
    },
    "message": "ok"
}
```

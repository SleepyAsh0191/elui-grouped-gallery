# elui-grouped-gallery
The simple grouped gallery that using element-ui/基于Element UI制作的简易分组相册

该项目的前身是本人曾制作的“尼群黑历史”网站，由于涉及到隐私问题，这里不公布网站地址。

`public/assets` 文件夹用于存放各种资源：
 * `audio` 文件夹存放音频。
 * `pic` 文件夹存放图片。
 * `video` 文件夹存放视频。
 
`data.js` 用于存放数据，用于分组，结构大致为：
```javascript
export const contentData = [
    {
        name: "first",
        content: [
            {
                text: "11223344",
                link: "some.images",
            },
            {
                text: "114514",
                link: "same.of.first.images",
            },
        ],
    },
    {
        name: "second",
        content: [
            {
                text: "11111",
                type: "audio",
                link: "some.files.here"
            },
        ]
    }
]
```

# Creator微信小游戏开发问题收集整理

## Q: 微信锁屏后卡死的问题 
引擎代码中找到下面代码，并屏蔽掉，可以解决微信锁屏后卡死的问题</br>
//opts["preserveDrawingBuffer"] = true;

## Q: Sprite的filled模式出问题了？
在图集中禁用旋转</br>
http://forum.cocos.com/t/sprite-filled/43661</br>
补充：物理引擎生成多边形刚体时，也要禁止旋转</br>

## Q: 微信小游戏中超越好友出现不显示的问题？
wx.getFriendCloudStorage不能频繁调用，可以在游戏一开始调用一次，然后在游戏中直接用就可以了

## Q: 图片加载

            this.node.getComponent(cc.Sprite).spriteFrame = new cc.SpriteFrame(cc.url.raw('resources/texture/icon-libao.png'));

            // 加载本地图片 SpriteFrame
            cc.loader.loadRes("texture/maxscore.png", cc.SpriteFrame, function (err, spriteFrame) {
                self.moreGame.spriteFrame = spriteFrame;
            });

	    // 加载远程图片
            let self = this;
            let remoteUrl = Global.linkGames[this.linkGameIndex].linkImage;
            cc.loader.load(remoteUrl, function (err, texture) {
                self.moreGame.spriteFrame = new cc.SpriteFrame(texture);
            });

## Q: ip定位
    // 判断分享模式
    getLocation: function () {
        let self = this;
        this.sendHttpRequest('http://api.map.baidu.com/location/ip?ak=ia6HfFL660Bvh43exmH9LrI6', (xhr) => {
            console.log('getIp', xhr);
            let data = JSON.parse(xhr.responseText);
            console.log('data ', data);
            console.log('获取的具体位置:', data.content.address_detail.province + "," + data.content.address_detail.city);
        }, (error) => {
            console.log('error', error);
        })
    },

## Q: 定制js引擎gulp build失败？
CLI version 3.9.1</br>
Local version 3.9.1</br>
这两个版本一定要一致

## Q: A星寻路算法在cocoscreator里的用法？
首先选择JS版本的实现，也可以自己写，但是效率不一定高。</br>
我找的JS版本的A星算法参考：https://github.com/bgrins/javascript-astar </br>
在creator里选择作为插件导入js文件，即可使用。

## Q: 2.0.9版本构建ios项目成功后，编译失败?
错误提示：tool 'xcodebuild' requires Xcode, but active developer directory '/Library/Developer/CommandLineTools' is a command line tools instance </br>
解决办法：[因为mac中多个xcode存在，被重命名了](https://blog.csdn.net/jymn_chen/article/details/21613745)
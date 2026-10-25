# 前言

VRChat改模(其实是无料小东西下多了)改多了,硬盘里的素材就多了.怎么整理就成了问题.目前使用过3款booth素材整理软件,把使用的感受整理如下:

# 软件使用对比

## 1/ KonoAsset

项目地址 [https://github.com/siloneco/KonoAsset/](https://github.com/siloneco/KonoAsset/)

KonoAsset是用过的第一款booth素材整理软件,软件有自己的存储位置设定.素材包拖动到软件后,添加booth商品页链接,默认抓取第1张商品图(可选择或上传其他图片作为软件内素材展示图),自己手动填写分类/tag信息,完成.

## 2/ booth-vault-toolhub

项目地址 [https://github.com/VRChatCN-Kipfel/booth-vault-toolhub](https://github.com/VRChatCN-Kipfel/booth-vault-toolhub)

软件有自己的存储位置设定,把带有booth id的压缩包,拖动到软件后,软件自动检测booth上的分类,将源文件移动到存储目录的各个分类文件夹,抓取1张商品图和商品信息,完成.

## 3/ BoothNest

项目地址 [https://github.com/VoidCloudCloud/BoothNest](https://github.com/VoidCloudCloud/BoothNest)

软件没有自己的存储位置设定,玩家如果原本有分类存储的习惯,可以直接在软件里指定素材目录.软件会自动读取各个文件的booth id,抓取所有商品图和商品信息,完成

# 软件特点对比

<table data-nomo-table="semantic"><tbody><tr><th><p></p></th><th><p>KonoAsset</p></th><th><p>booth-vault-toolhub</p></th><th><p>BoothNest</p></th></tr><tr><td><p>商品图预览</p></td><td><p>有,导入时选择商品图或者自行上传</p></td><td><p>软件本身没有预览图,但是文件夹图</p><p>标是下载的商品图,需要在资源管理</p><p>器中预览</p></td><td><p>有,所有商品页图片都可以在网页终</p><p>端查看</p></td></tr><tr><td><p>分类</p></td><td><p>完全手动,规避原作者不合适的分类</p><p>或者你有自己的分类规则,比较繁琐</p></td><td><p>自动抓取booth分类</p></td><td><p>自动抓取booth分类</p></td></tr><tr><td><p>商品信息</p></td><td><p>不抓取原商品页信息,手动编辑,可自</p><p>行添加想要的信息</p></td><td><p>自动抓取原商品页信息,但是需要进</p><p>入文件目录查看txt文件</p></td><td><p>自动抓取原商品页信息,可以在网页</p><p>终端查看商品页信息</p></td></tr><tr><td><p>存储</p></td><td><p>源文件和软件存储空间各一份,双倍</p><p>快乐</p></td><td><p>移动源文件到软件存储空间</p><p><sub><em>*注:拖动文件夹到软件后,慎用"纠正</em></sub></p><p><sub><em>错位"功能,可能导致文件被删除,不</em></sub></p><p><sub><em>在回收</em></sub><sub>站</sub></p></td><td><p>不改变原有存档目录结构,不碰源文</p><p>件,只在软件配置目录存储商品信息</p><p>和缩略图</p></td></tr></tbody></table>

综合来看,BoothNest目前最符合我的需求,但KonoAsset的商品手动备注手动分类功能,以及booth-vault-toolhub的漂亮文件夹图标,是BoothNest目前所不具备的
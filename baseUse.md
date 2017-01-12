#这里简单的介绍一下使用方法,包括自定义cell
1. 先初始化collectView需要用到的图层

```
let cellLayout = UICollectionViewFlowLayout()
self.cellLayout.scrollDirection = .vertical //设置滚动方向
self.cellLayout.itemSize = CGSize.init(width: 200, height: 70)   //设置cell的size
self.cellLayout.minimumLineSpacing = 10 //上下间隔
self.cellLayout.minimumInteritemSpacing = 5 //左右间隔
self.cellLayout.headerReferenceSize = CGSize.init(width: 20, height: 20)    //头部
self.cellLayout.footerReferenceSize = CGSize.init(width: 20, height: 20)    //尾部
```

#使用自定义的layout
1.创建一个类，继承于UICollectionViewFlowLayout(类似于tabelView)
2.通过重写prepare来初始化属性
```
override func prepare() {
    self.scrollDirection = .vertical  //垂直滚动
    self.itemSize = CGSize.init(width:200,height:70)  //设置cell的大小
}
```
3.刷新布局时调用该函数
```
override func layoutAttributesForItem(at indexPath: IndexPath) -> UICollectionViewLayoutAttributes? {
        let attrs = UICollectionViewLayoutAttributes.init(forCellWith: indexPath)
        return attrs
}
```
4.通过重写layourAttributesForElements(rect)来描述可见区域(自定义区域)
```
override func layourAttributesForElements(in rect: CGRect) -> [UICollectionViewLayourAttributes]? {
  let attributesArray = super.layoutAttributesForElements(in:rect)
  return attributesArray
}
```
5.显示范围变化后是否重新布局
```
override func shouldInvalidateLayout(forBoundsChange newBounds: CGRect) -> Bool {
        return true
}

```

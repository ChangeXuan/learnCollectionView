#自定义layout继承与UICollectionViewFlowLayout
```Swift
class dynamicPop:UICollectionViewFlowLayout {
    
    //入口初始化
    override func prepare() {
        super.prepare()
        
        self.scrollDirection = .vertical //设置滚动方向
        self.itemSize = CGSize.init(width: 200, height: 70)   //设置cell的size
    }
    
    //重新刷新布局时候调用
    override func layoutAttributesForItem(at indexPath: IndexPath) -> UICollectionViewLayoutAttributes? {
        let attrs = UICollectionViewLayoutAttributes.init(forCellWith: indexPath)
        return attrs
    }
    
    //返回指定矩形中所有单元格和视图的布局属性.
    override func layoutAttributesForElements(in rect: CGRect) -> [UICollectionViewLayoutAttributes]? {
        
        //可见范围内的矩形
        let attributesArray = super.layoutAttributesForElements(in: rect)
        
        let centerY = (self.collectionView?.contentOffset.y)! + (self.collectionView?.frame.size.height)!*0.5;
        for arrs in attributesArray! {
            //cell中心和collectionview的中心距离
            let margin = abs(centerY - arrs.center.y);
            //cell缩放比例
            let scale = 1-(margin / (self.collectionView?.frame.size.height)!);
            if (scale>0.9) {
                arrs.alpha = 1;
            }else
            {
                arrs.alpha = 0.5;
            }
            arrs.transform3D = CATransform3DMakeScale(scale, scale, scale);
        }
        
        return attributesArray
    }
    
    //显示范围发生变化后是否重新布局
    override func shouldInvalidateLayout(forBoundsChange newBounds: CGRect) -> Bool {
        return true
    }
    
}
```

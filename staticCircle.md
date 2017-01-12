#自定义layout继承与UICollectionViewLayout
```Swift
class staticCircle:UICollectionViewLayout {
    
    private var cellCount:Int!
    private var collectionSize:CGSize!
    private var viewCenter:CGPoint!
    private var viewRadius:CGFloat!
    
    override func prepare() {
        super.prepare()
        
        self.cellCount = self.collectionView?.numberOfItems(inSection: 0)   //取得section=0时的cell的个数
        self.collectionSize = self.collectionView?.frame.size   //取得collectionView的frame大小
        self.viewCenter = CGPoint.init(x: self.collectionSize.width/2, y: self.collectionSize.height/2) //设置中心点
        self.viewRadius = min(self.collectionSize.width, self.collectionSize.height) / 2    //设置围成圆的半径大小
        
    }
    override func layoutAttributesForItem(at indexPath: IndexPath) -> UICollectionViewLayoutAttributes? {
        let attrs = UICollectionViewLayoutAttributes.init(forCellWith: indexPath)
        //定义cell的大小
        attrs.size = CGSize.init(width: 80, height: 80)
        //计算构成圆形的center点集
        let x = self.viewCenter.x + self.viewRadius*cos(CGFloat(2*Double(indexPath.item)*M_PI)/CGFloat(self.cellCount))
        let y = self.viewCenter.y + self.viewRadius*sin(CGFloat(2*Double(indexPath.item)*M_PI)/CGFloat(self.cellCount))
        attrs.center = CGPoint.init(x: x, y: y)
        return attrs
    }
    
    override func layoutAttributesForElements(in rect: CGRect) -> [UICollectionViewLayoutAttributes]? {

        var attributesArray = [UICollectionViewLayoutAttributes]()
        
        for i in 0..<self.cellCount {
            let indexPath = IndexPath.init(item: i, section: 0)
            let attributes = self.layoutAttributesForItem(at: indexPath)
            attributesArray.append(attributes!)
        }
        
        return attributesArray
    }
    
}

```

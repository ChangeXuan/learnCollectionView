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
2. 初始化collectView
```
var collect:UICollectionView!
self.collect = UICollectionView(frame:self.view.frame,collectionViewLayout:self.cellLayout)//这里一定要把layout加上
self.collect.backgroundColor = UIColor.white
self.collect.delegate = self
self.collect.dataSource = self
self.collect.collectionViewLayout = self.cellLayout
self.view.addSubview(collect)
```
3. 初始化cell中需要加载的xib文件
```
let nib = UINib.init(nibName: "cellXib", bundle: .main)//xib的文件名为cellXib
self.collect.register(nib, forCellWithReuseIdentifier: "selfCell")//id为selfCell
```
4. 重写collectView协议中的3个必要函数(UICollectionViewDelegate和UICollectionViewDataSource)
```
//section的个数
func numberOfSections(in collectionView: UICollectionView) -> Int {
        return 1
}
//cell的个数
func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int {
        return 100
}
//描述每个cell
func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
        let id = "selfCell"
        let cell = collectionView.dequeueReusableCell(withReuseIdentifier: id, for: indexPath) as! cellClass
        cell.showLabel.text = "day\(indexPath.row)"
        cell.backgroundColor = UIColor.yellow
        return cell
    }
```

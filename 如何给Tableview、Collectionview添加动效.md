## 如何给Tableview、Collectionview添加动效
> OneSwift - iOS Tips Only Based On Swift

TableView和CollectionView在开发产品中使用非常频繁，不管是独立使用还是组合使用，掌握它们都是所有iOS开发者必备的技能。



今天为大家来分享我使用它们时，如何实现动效的？内容分两部分：

**1.加载动效**

**2.点击动效**



### 一、加载Cell的动效

当组件加载时，为了让页面显得动感有趣，可以为TableView、CollectionView整体添加动效。

主要用到的方法是：UIView.animate



#### 方案一，Cell逐个呈现，例如OneDay的首页加载。

![image](/img/OneDay首页加载.gif)

​实现方法是在TableView加载后增加整体的动效，通过循环和延迟，让每个cell从不同的时间开始经历相同的时间动效结束。

函数代码：

```
func animateTable() {

        let cells = HomeTableView.visibleCells

        let tableHeight: CGFloat = HomeTableView.bounds.size.height

        for (index, cell) in cells.enumerated() {

            cell.transform = CGAffineTransform(translationX: 0, y: tableHeight)

            UIView.animate(withDuration: 1.0, delay: 0.05 * Double(index), usingSpringWithDamping: 0.8, initialSpringVelocity: 0, options: [], animations: {

                cell.transform = CGAffineTransform(translationX: 0, y: 0);



            }, completion: nil)

        }

}
```

在ViewWillAppear中调用：

```
override func viewWillAppear(_ animated: Bool) {

        super.viewDidAppear(animated)

    self.animateTable()

}
```


#### 方案二，Cell同时呈现，例如OneClock的菜单加载。



​实现方式是在Collectionview加载后，为整体增加动效，因为不需要做延迟处理，所以可以直接以CollectionView整体做动效。

函数代码：

```
func animateAll(){

        let animateView = self.SettingCollection

        let btnHeight:CGFloat = self.SettingCollection.bounds.size.height

        print(btnHeight)

        animateView?.transform = CGAffineTransform(translationX: 0, y: 80)

        UIView.animate(withDuration: 1.0, delay: 0.0, usingSpringWithDamping: 0.8, initialSpringVelocity: 0, options: [], animations: {

            animateView?.transform = CGAffineTransform(translationX: 0, y: 0);

        }, completion: nil)

}
```


在ViewWillAppear中调用:
```
override func viewWillAppear(_ animated: Bool) {

        self.SettingCollection.reloadData()

        self.animateAll()

}
```


### 二、点击Cell的动效

`TableView` 和 `CollectionView` 在被点击时可以添加一定的动效，同时在点击完成后我们需要恢复最初始的状态。

用到的方法是：`didHighlightItemAt`、`didUnhighlightItemAt`、`CGAffineTransform`



`Tablview`的点击效果，例如**OneDay**的列表点击。



​实现代码：
```
func tableView(_ tableView: UITableView, didHighlightRowAt indexPath: IndexPath) {

        let cell = tableView.cellForRow(at: indexPath) as! CustomTableViewCell

        UIView.beginAnimations(nil, context: nil)

        UIView.setAnimationDuration(0.2) //设置动画时间

        cell.transform =  CGAffineTransform(scaleX: 0.9, y: 0.9)

        UIView.commitAnimations()



    }
```

```
func tableView(_ tableView: UITableView, didUnhighlightRowAt indexPath: IndexPath) {

        let cell = tableView.cellForRow(at: indexPath) as! CustomTableViewCell

        UIView.beginAnimations(nil, context: nil)

        UIView.setAnimationDuration(0.2) //设置动画时间

        cell.transform =  CGAffineTransform(scaleX: 1.0, y: 1.0)

        UIView.commitAnimations()

}
```


`Collection`的点击效果，例如**OneClock**的菜单点击。



实现代码：
```
func collectionView(_ collectionView: UICollectionView, didHighlightItemAt indexPath: IndexPath) {

        let cell = collectionView.cellForItem(at: indexPath) as! SettingCollectionViewCell

        cell.WidthCons.constant = 10

        cell.HeightCons.constant = 10

    }
```

```
func collectionView(_ collectionView: UICollectionView, didUnhighlightItemAt indexPath: IndexPath) {

        let cell = collectionView.cellForItem(at: indexPath) as! SettingCollectionViewCell

        cell.WidthCons.constant = 0

        cell.HeightCons.constant = 0

}
```


推荐大家使用比较平滑的方式实现，如果直接修改大小，点击效果显得非常生硬。



返回首页：[OneSwift](/index.md).

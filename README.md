# TableRefresher
Quick implementation of a pull to refresh action.

## Usage:

In the table's ViewController add

### Init
```
private var refresher: TableRefresher

init() {
    ...
    self.refresher = TableRefresher()
}

override func viewDidLoad() {
    ...
    // set the spinner to be used (this is optional)
    self.refresher.set(spinner: self.spinner)
}
```

### Suscribe to this method to perform the pull refresh
```
func scrollViewDidEndDecelerating(_ scrollView: UIScrollView) {
    refresher.validatePullRefresh(withDirection: .up,
        for: categoryView.categoriesTableView,
        with: getCocktailCategories)
}
```

### Suscribe to this method to check the direction in which the user pulls
```
func scrollViewWillEndDragging(_ scrollView: UIScrollView, withVelocity
    velocity: CGPoint, targetContentOffset: UnsafeMutablePointer<CGPoint>) {

    let table = categoryView.categoriesTableView!
    refresher.set(offset: table.contentOffset.y)

    if targetContentOffset.pointee.y > scrollView.contentOffset.y {
        refresher.set(direction: .up)
    } else {
        refresher.set(direction: .down)
    }
}
```

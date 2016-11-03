闲来无事....写个UICollectionView Demo
![这里写图片描述](http://img.blog.csdn.net/20161103143140553)

```
//
//  ViewController.m
//  CollectionViewDemo
//
//  Created by 赵伟争 on 2016/11/3.
//  Copyright © 2016年 zwz. All rights reserved.
//

#import "ViewController.h"

@interface ViewController ()<UICollectionViewDataSource, UICollectionViewDelegate, UICollectionViewDelegateFlowLayout>
{
    UICollectionViewFlowLayout *_customLayout;
    UICollectionView *_collectionView;
    BOOL isLogin; //YES: 登录, NO: 不是
}
@end
static NSString *cellIdentifier = @"CELL";
static NSString *headerIdentifier = @"header";
static NSString *footIdentifier = @"foot";
@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    
    isLogin = YES; //判断是否登录,手动设置,  或者登录后设置, 刷新整个CollectionView
    UICollectionViewFlowLayout *layout = [[UICollectionViewFlowLayout alloc] init];
    
    //滚动方向
    layout.scrollDirection = UICollectionViewScrollDirectionVertical;
    UICollectionView *collectionView = [[UICollectionView alloc] initWithFrame:self.view.frame collectionViewLayout:layout];
    
    collectionView.backgroundColor = [UIColor whiteColor];
    collectionView.dataSource = self;
    collectionView.delegate = self;
    
    //UICollectionViewCell 可以自定义
    [collectionView registerClass:[UICollectionViewCell class] forCellWithReuseIdentifier:cellIdentifier];
    
    
    //[collectionView registerClass:[ChoosePictureHeader class] forSupplementaryViewOfKind:UICollectionElementKindSectionHeader withReuseIdentifier:headerIdentifier];
    //[collectionView registerClass:[UICollectionReusableView class] forSupplementaryViewOfKind:UICollectionElementKindSectionFooter withReuseIdentifier:footIdentifier];
    
    [self.view addSubview:collectionView];

    // Do any additional setup after loading the view, typically from a nib.
}
#pragma mark - UICollectionView数据源
// 返回有多少个cell
- (NSInteger)collectionView:(UICollectionView *)collectionView numberOfItemsInSection:(NSInteger)section
{
    if (section == 0) {
        if (isLogin) {
            return 4;
        } else {
            return 8;
        }
        
    } else {
        return 8;
    }
    //    return 30;
}

- (NSInteger)numberOfSectionsInCollectionView:(UICollectionView *)collectionView;
{
    if (isLogin) {
        return 2;
    } else {
        return 1;
    }
    
}

// 返回每个cell长什么样子
- (UICollectionViewCell *)collectionView:(UICollectionView *)collectionView cellForItemAtIndexPath:(NSIndexPath *)indexPath
{
    //可以自定义UICollectionViewCell
    UICollectionViewCell *cell = [collectionView dequeueReusableCellWithReuseIdentifier:cellIdentifier forIndexPath:indexPath];
    
    cell.backgroundColor = [UIColor redColor];
    return cell;
}

- (void)didReceiveMemoryWarning {
    [super didReceiveMemoryWarning];
    // Dispose of any resources that can be recreated.
}

//设置item的大小
- (CGSize)collectionView:(UICollectionView *)collectionView layout:(UICollectionViewLayout*)collectionViewLayout sizeForItemAtIndexPath:(NSIndexPath *)indexPath {
    CGFloat width = [UIScreen mainScreen].bounds.size.width;
    
    if (indexPath.section == 0) {
        if (isLogin) {
            CGFloat oneSectionWidth = width/2;
            return CGSizeMake(oneSectionWidth-1.5, oneSectionWidth/2);
        } else {
            CGFloat oneSectionWidth = width/4;
            return CGSizeMake(oneSectionWidth-1.5, oneSectionWidth-1.2);
        }
        
    } else {
        CGFloat oneSectionWidth = width/4;
        return CGSizeMake(oneSectionWidth-1.5, oneSectionWidth-1.2);
    }
    
}

//UIEdgeInsetsMake(CGFloat top, CGFloat left, CGFloat bottom, CGFloat right)
- (UIEdgeInsets)collectionView:(UICollectionView *)collectionView layout:(UICollectionViewLayout*)collectionViewLayout insetForSectionAtIndex:(NSInteger)section {
    return UIEdgeInsetsMake(15, 1, 5, 1);
}
//最小行间距
- (CGFloat)collectionView:(UICollectionView *)collectionView layout:(UICollectionViewLayout*)collectionViewLayout minimumLineSpacingForSectionAtIndex:(NSInteger)section {
    return 1.0f;
}
//item之间的最小距离
- (CGFloat)collectionView:(UICollectionView *)collectionView layout:(UICollectionViewLayout*)collectionViewLayout minimumInteritemSpacingForSectionAtIndex:(NSInteger)section {
    return 1.0f;
}
@end

```
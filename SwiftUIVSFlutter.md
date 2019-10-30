# SwiftUI 和 Flutter开发对比

## SwiftUI是什么

苹果WWDC‘19有许多大的更新并且发布了新技术，其中有一个令开发者非常兴奋的新技术就是发布了SwiftUI。一个declarative UI框架用于构建iOS, iPadOS, macOS, watchOS, tvOS下的“跨”苹果平台的应用，理论上SwiftUI的一套declarative UI代码可以在这些平台上运行。

![swuftui.png](http://p7.qhimg.com/t010a0bba1647f25c8d.png)

另外为什么说开发者会很兴奋，这是因为苹果也加入了现代且先进的declarative UI编程。苹果的开发者们不用再坐在边上看React Native或Flutter带来的如下特性而无法享用了，

+ 简化代码
+ 声明语法
+ 提高开发效率
+ 热更新
+ 跨平台

Google在今年的I/O‘19大会上也发布了Jetpack Compose，一个新的Android declarative UI框架，可以看出declarative UI在移动端上的应用越来越多充分说明了它所带来的开发优势。苹果今年宣布SwiftUI正好赶在了这个间隙，也就引起开发者的共鸣。

## Flutter是什么
Flutter应该不是新技术了，谷歌在两年前已经给出了它的beta版，现在稳定版也已经发了几个版本了。它是UI框架，可以快速在iOS和Android上构建高质量的原生性能的用户界面。Flutter可以与现有的代码一起工作，它正在被越来越多的开发者和组织使用，并且Flutter是完全免费、开源的。特点如下：

+ Declaraive UI
+ 跨平台
+ 快速开发
+ 原生的性能
+ 多种多样的Widget，目前官方Widget数量已经有150+
+ 统一的应用开发体验
+ 访问本地功能和大量的PlugIn支持

## Declarative UI是什么

说了很多的declarative UI那具体它什么，众所周知现在的应用程序开发，尤其是UI部分的开发已经变的很复杂。传统的Objective-C开发的iOS应用，UI和业务分解不好的UIViewController代码直逼万行甚至更多，这里大部分代码是在处理数据变化引起的UI变化和用户的交互及下面这些问题：

+ 控件事件响应
+ 设备响应，旋转、陀螺仪等
+ 动态字体大小
+ 不同主题
+ 用户自定义视图、布局
+ A/B测试等

然后又要加各种的动效让用户和UI交互起来自然、简单和便捷。上面这些都是一个叫imperative方式来实现的，在这种方式下一个登录可以是如下过程：

+ 首先构建出整个登录界面
+ 当用户点击登录按钮
+ 显示一个加载中的视图，接着后台请求数据
+ 数据返回，隐藏加载中
+ 根据数据结果要么跳转到主页要么弹出登录错误框

declarative模式中首先你要定义界面的描述，这个描述会在不同的平台上用那个平台对应的UI控件展示出来。界面的数据和事件等都可以看做是这个界面的状态，描述中绑定这些状态，在状态改变时更新界面。比如用户点击登录按钮是个状态，点击一下状态就改变；用户登录是一个状态，如果登录了显示主页否则显示登录页。

下面再举个例子，如图我们要改变ViewB的子视图，删除c1和c2，添加c3且改变背景色

![swuftui.png](http://p0.qhimg.com/t01d2edbda3eb3c0cad.png)

+ Imperative方法，首先找到ViewB的实例然后在它上面修改
	
	```swift
	ViewB b = getViewB
	b.setColor(red)
	b.clearChildren()
	ViewC c3 = new ViewC(...)
	b.add(c3)
	```
+ Declarative方法，直接返回声明的新ViewB

	```swift
	if (changed_state) {
		return ViewB(
			color: red,
			child: ViewC(...),
		)
	}
	else {
		return ViewB(
			color: yellow,
			Childrens: [
				ViewC1,
				ViewC2
			]
		)
	}
	```

## 开发对比

接下来我们将通过苹果SwiftUI课程中创建的App Landmarks来对比一下SwiftUI和Flutter开发。选择这个课程的App是因为有开发者用Flutter作了一个一样的Landmarks应用，这样我们在有的地方就可以利用里面的代码做更直观的比较，下图是这个App的首页截图对比

![SwifuUI code](http://p8.qhimg.com/t013528d46859e68183.png)

### 开发环境

+ SwiftUI - XCode

	![XCode](http://p8.qhimg.com/t01a1f7a11ecd606eec.png)
	
	XCode对SwiftUI的支持是不用说的，从图中可以看出从左向右依次是工程列表、编辑文件和SwiftUI的预览Canvas。
	
+ Flutter - Android Studio / Visual Stuio Code

	![Android Studio](http://p3.qhimg.com/t01843d52914c922f93.png)

	左向右依次是工程列表、代码编辑器和Flutter的布局大纲。另外Visual Stuio Code也可以用于Flutter的开发，在安装完Flutter的扩展后和Audroid Studio的功能基本一样，只是比Android Studio要轻量级一些。

	我们在苹果的SwiftUI课程中发现Xcode所带的这个预览功能还是十分强大的，在预览上做修改可以直接同步修改代码，并且这个预览界面还有编程的入口，可以通过代码修改预览行为也可以指定预览Canvas的大小或是直接指定设备，这整个过程都不用编译代码。相比Android Studio没有这方面的功能。

### UI

+ SwiftUI - View
	
	View是一个Protocol，SwiftUI中的自定义视图都要遵从与这个协议且必须实现body属性来提供自定义视图。如下图所示代码会在屏幕中间显示文案Hello World!。这里的contenView继承于View接着实现了body属性。另外contenView_Previews结构是用于预览的代码，这里直接创建ContentView，可以直接在右边的预览中看到效果。

	![SwifuUI code](http://p0.qhimg.com/t0192d18c723d3fb6d4.png)
	
	View还定义了一些操作如：尺寸、剪切、阴影、描边等等。[苹果View文档](https://developer.apple.com/documentation/swiftui/view)
	
+ Flutter - Widget

	Flutter的UI元素都继承于Widget类，如下代码创建一个无状态的widget在屏幕中间输出Hello World!。它继承于StatelessWidget，StatelessWidget又继承于Widget。这里的build方法是必须实现且返回UI内容的。

	```dart
	import 'package:flutter/material.dart';

	class ContentView extends StatelessWidget {
	  @override
	  Widget build(BuildContext context) {
	    return Center(
	      child: Text("Hello World!"),
	    );
	  }
	}
	```

	可以看到对于declarative UI的SwiftUI和Flutter这里创建一个自定义的UI基本一样，只是Flutter的stateful和stateless在SwiftUI中是没有的。另外Flutter没有实时预览所以也没有预览部分的代码。

### 布局

SwiftUI的Stacks对应Flutter的Flex widgets，Row、Column和Stack都是在一维上显示子视图。下表是他们对应关系

SwiftUI | Flutter | 描述 
---- | ---- | ----
HStack | Row | 行布局
VStack | Column | 列布局
ZStack | Stack | 重叠布局

我们这里看一下前面说的Landmarks应用，它首页是个列表，其中每行是个水平布局，如下图：

![Landmarks cell](http://p1.qhimg.com/t018134e0796c9371ab.png)

SwiftUI直接使用HStack然后里面嵌入基本UI元素，Image、Text和Spacer。Flutter则是使用Row布局，它的children中也是一些基本UI Widgets。

![Landmarks cell](http://p9.qhimg.com/t019494405fe2692bc2.png)


SwiftUI

```swift
HStack {
    landmark.image
        .resizable()
        .frame(width: 50, height: 50)
    Text(verbatim: landmark.name)
    Spacer()

    if landmark.isFavorite {
        Image(systemName: "star.fill")
            .imageScale(.medium)
            .foregroundColor(.yellow)
    }
}
```

Flutter

```dart
Row(
  children: <Widget>[
    Image.asset(
      'assets/${landmark.imageName}.jpg',
      width: 50.0
    ),
    SizedBox(
      width: 16,
    ),
    Text(
      landmark.name,
      style: TextStyle(fontSize: 16),
    ),
    Expanded(
      child: Container(),
    ),
    landmark.isFavorite ? StarButton(isFavorite: landmark.isFavorite) : Container(),
    Icon(
      Icons.arrow_forward_ios,
      size: 15.0,
      color: const Color(0xFFD3D3D3),
    ),
  ]
)
```

代码中的landmark是数据模型对象，对应下面的JSON数据

```json
{
    "name": "Turtle Rock",
    "category": "Rivers",
    "city": "Twentynine Palms",
    "state": "California",
    "id": 1001,
    "isFeatured": true,
    "isFavorite": true,
    "park": "Joshua Tree National Park",
    "coordinates": {
        "longitude": -116.166868,
        "latitude": 34.011286
    },
    "imageName": "turtlerock"
}
```

可以看出由于SwiftUI在间距控制上有默认值所以少了一些间距的控制代码看起来更简洁一点。但是Flutter对布局Widgets的命名如：Row、Column和Stack看起来更直观。当然布局的元素还有很多就不再对比了。

### 列表

UIKit的TableView在SwiftUI中是List。你可以把所有的子内容放在List里。这对比于UITableView去实现多个代理方法是极大的进步。

在Flutter上你可以有多个选择，你可以用ListView来显示多行内容或是用SingleChildScrollView来显示一屏可以滚动的内容。更高级的可以控制导航栏效果的可以用CustomScrollView，它的子视图需要用一系列的Sliver widgets。

在前面说的Landmarks应用中，首页就是一个列表。SwiftUI使用ForEach来创建这个列表的元素，Flutter列表用了SliverList。下面是两者的代码：

SwiftUI

```swift
List {
    ForEach(landmarks) { landmark in
    	LandmarkRow(landmark: landmark)
    }
}
```

Flutter

```dart
SliverList(
  delegate: SliverChildBuilderDelegate(
    (context, index) {
      final landmark = landmarks[index];
      return LandmarkCell(
        landmark: landmark,
      );
    },
    childCount: landmarks.length,
  ),
),
 
```

其中landmarks是数据数组，其中的每条数据是之前的JSON数据。SwiftUI的LandmarkRow和Flutter的LandmarkCell是前面布局中说的每行的UI。

### 导航即页面跳转能力
#### 进入新页面
导航页面跳转在UI开发中是非常重要的，方便的提供页面跳转能力也是一个UI框架好坏的关键。SwiftUI中的导航要借助NavigationView和NavigationLink实现，Flutter则是靠Route和Navigator。下面看实例代码：

SwiftUI

```swift
var body: some View {
    NavigationView {
        List {
            ForEach(userData.landmarks) { landmark in
                NavigationLink(
                    destination: LandmarkDetail(landmark: landmark)
                ) {
                    LandmarkRow(landmark: landmark)
                }
            }
        }
        .navigationBarTitle(Text("Landmarks"))
    }
}
```
说明：

1. body中直接嵌入NavigationView，它会提供导航栏及导航栏的title动画。
2. NavigationView的子视图是List
3. List的行是NavigationLink
3. NavigationLink的子视图是 LandmarkRow
4. NavigationLink的destination参数指明了要打开的新页面LandmarkDetail以及传递的参数
5. 最后的navigationBarTitle指定Title文案。

Flutter

```dart
SliverList(
  delegate: SliverChildBuilderDelegate(
    (context, index) {
      final landmark = landmarks[index];
      return LandmarkCell(
        landmark: landmark,
        onTap: () {
          Navigator.push(
            context,
            Route(
              builder: (context) => LandmarkDetail(
                    landmark: landmark,
                  ),
            ),
          );
        },
      );
    },
    childCount: landmarks.length,
  ),
)
```

1. SliverList中构建每行LandmarkCell
2. 处理LandmarkCell的onTap点击事件
3. 用Navigator.push方法进入新页面
4. Navigator.push的参数是个Route其中定义了新页面名称和传递的参数

SwiftUI的代码很简单直观，不需要处理点击事件。

#### 返回上页

SwiftUI和Flutter用上面的方法导航栏都会自带返回按钮。两者也都可以通过代码返回，这个不再说明。但是SwiftUI还是beta阶段，一些介绍说了它没有Navigation stack的管理，不能像UIKit那样直接Pop到任意页面，相比Flutter的Navigator有这个能力。

### 使用Native功能

还是以Landmarks应用为例在点击首页的列表后会进入下面的详情页，可以看到页面上面的地图不再是基本UI元素。在SwiftUI中用的是UIKit的MapKit，Flutter中用的是插件google_maps_flutter。

![landmarks_details_page](http://p0.qhimg.com/t01e921f68ab5c67052.png)

SwiftUI使用MapKit的代码如下：

```swift
struct MapView: UIViewRepresentable {
    var coordinate: CLLocationCoordinate2D

    func makeUIView(context: Context) -> MKMapView {
        MKMapView(frame: .zero)
    }

    func updateUIView(_ view: MKMapView, context: Context) {
        let span = MKCoordinateSpan(latitudeDelta: 0.02, longitudeDelta: 0.02)
        let region = MKCoordinateRegion(center: coordinate, span: span)
        view.setRegion(region, animated: true)
    }
}
```
这里不再继承于View而是UIViewRepresentable，当然UIViewRepresentable还继承于View，makeUIView方法创建UIView元素，updateUIView更新view，这里设置地图的坐标。

Flutter

```dart
Widget _mapView() {
return GoogleMap(
  mapType: MapType.normal,
  initialCameraPosition: CameraPosition(
    target: LatLng(landmark.coordinates.latitude, landmark.coordinates.longitude),
    zoom: 13.70,
  ),
  myLocationButtonEnabled: false,
  onMapCreated: (GoogleMapController controller) {
    _controller.complete(controller);
  },
);
}
```
这里看Flutter使用google_maps_flutter插件也不是很复杂，但是这个插件是基于Flutter的Platform-view实现的，在Flutter中实现这样一个插件还是很费时的，Flutter的插件一般都是支持iOS和Android的。在对原生功能的使用上苹果的SwiftUI在苹果平台上必然是非常方便的。

### 状态管理
状态管理是指在数据发生变化时更新UI。Landmarks应用中首页的Switch按钮过滤标星的行就是用状态触发更新界面。如下图：

![landmarks_details_page](http://p4.qhimg.com/t01a97a378524ffe1ca.png)

SwiftUI和Flutter在状态管理的实现上还是不一样的，

+ SwiftUI的状态管理是通过设置数据是有状态的然后绑定数据实现的
+ Flutter里是通过数据改变后调用setState方法实现的

SwiftUI

```swift
struct LandmarkList: View {
    @State var showFavoritesOnly = true

    var body: some View {
        NavigationView {
            List {
                Toggle(isOn: $showFavoritesOnly) {
                    Text("Favorites only")
                }

                ForEach(landmarkData) { landmark in
                    if !self.showFavoritesOnly || landmark.isFavorite {
                        NavigationLink(destination: LandmarkDetail(landmark: landmark)) {
                            LandmarkRow(landmark: landmark)
                        }
                    }
                }
            }
            .navigationBarTitle(Text("Landmarks"))
        }
    }
}
```
通过在属性showFavoritesOnly前加@State修饰符来表明这个数据是有状态的，Toggle是那个Switch按钮它的值通过$符绑定在了showFavoritesOnly属性上，当点击按钮值变化时body会自动再次执行，ForEach根据self.showFavoritesOnly的值来过滤列表。SwiftUI中还有别的方式进行状态管理这里不再说了。

Flutter

```dart
CupertinoSwitch(
  value: _showFavoritesOnly,
  onChanged: (state) {
    setState(() {
      _showFavoritesOnly = state;
    });
  },
)
```

CupertinoSwitch是Switch按钮，onChanged方法会在值发生变化时调用，这时调用setState方法给变量_showFavoritesOnly设置新值接着界面的build方法就会被调用，我们根据_showFavoritesOnly的值来设置新的数据源，下面的List就会用新的数据源展示列表，代码如下：

```dart
 Widget build(BuildContext context) {
    final landmarks = _showFavoritesOnly ? favoriteLandmarks : allLandmarks;
    
    // 构建列表
    ...
}
```

## 总结
文章中只是从开发中的几个方面对比了SwiftUI和Flutter的实现方法，当然还有很多可以比较的地方比如：数据存储、消息通知、动画、绘制等。通过上面的比较可以看出基于declarative UI的方式两者有不少的相似处，也有一些不同。

代码复杂度，可以看出Flutter的代码量和复杂度要高于SwiftUI，这个由于SwiftUI是苹果设计的运行在自己的系统上的框架，它可以很深度的优化，再加上苹果一贯的简约风格和简化开发的理念造成了SwiftUI的代码量和复杂度都比Flutter低，但是这就造成了定制性不强。相反Flutter是开源的可修改定制的地方就多。

SwiftUI刚刚开始，现在还没发布正式版，且只能支持iOS13以上系统，这就表明SwiftUI至少还要再发展一段时间才能有更多的使用并进入主流。相比Flutter已经发展了多年了，且有大量的应用，兼容的设备也是相当广泛的。

## 参考
苹果SwiftUI课程<br/>
https://developer.apple.com/tutorials/swiftui

苹果SwiftUI文档<br/>
https://developer.apple.com/documentation/swiftui

Building the SwiftUI Sample App in Flutter<br/>
https://github.com/VGVentures/flutter_landmarks

SwiftUI or Flutter? <br/>
https://juejin.im/post/5d05b45bf265da1bcc193ff4
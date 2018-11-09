# React Navigation 2.X 的使用
> **更新于 2018.11.08**

**目录**
[TOC]

*****

## Navigation Props
- **this.props.navigation**
    - navigate - 跳转到另一个屏幕
    ~~~javascript
    1. navigation.navigate({ routeName, params, action, key })
    2. navigation.navigate(routeName, params, action)
    
    ~~~
    - goBack - 关闭当前屏幕并返回上一个屏幕
    ~~~javascript
    ~~~
    - addListener - 添加对路由的监听
    ~~~javascript
    ~~~
    - isFocused
    ~~~javascript
    ~~~
    - state
    ~~~javascript
    ~~~
    - setParams
    ~~~javascript
    ~~~
    - getParam
    ~~~javascript
    ~~~
    - dispatch
    ~~~javascript
    ~~~
    - dangerouslyGetParent
    ~~~javascript
    ~~~
- **如果是StackNavigator, this.props.navigation还有如下方法**
    - push
    ~~~javascript
    ~~~
    - pop
    ~~~javascript
    ~~~
    - popToTop
    ~~~javascript
    ~~~
    - replace
    ~~~javascript
    ~~~
    - reset
    ~~~javascript
    ~~~
    - dismiss
    ~~~javascript
    ~~~
- **如果是DrawerNavigator, this.props.navigation还有如下方法**
    - openDrawer
    ~~~javascript
    ~~~
    - closeDrawer
    ~~~javascript
    ~~~
    - toggleDrawer
    ~~~javascript
    ~~~

## Navigation Actions
> ~~~javascript
> import { NavigationActions } from 'react-navigation';
> ~~~

- navigate
    ~~~javascript
    ~~~
- back
    ~~~javascript
    ~~~
- setParams
    ~~~javascript
    ~~~

## Stack Actions
> ~~~javascript 
> import { StackActions } from 'react-navigation';
> ~~~

- reset
    ~~~javascript
    ~~~
- replace
    ~~~javascript
    ~~~
- push
    ~~~javascript
    ~~~
- pop
    ~~~javascript
    ~~~
- popToTop
    ~~~javascript
    ~~~

## Drawer Actions
> ~~~javascript 
> import { DrawerActions } from 'react-navigation-drawer';
> ~~~

- openDrawer - 打开抽屉
    ~~~javascript
    this.props.navigation.dispatch(DrawerActions.openDrawer());
    ~~~
- closeDrawer - 关闭抽屉
    ~~~javascript
    this.props.navigation.dispatch(DrawerActions.closeDrawer());
    ~~~
- toggleDrawer - 切换抽屉
    ~~~javascript
    this.props.navigation.dispatch(DrawerActions.toggleDrawer());
    ~~~

## createStackNavigator
> ~~~javascript 
> createStackNavigator(RouteConfigs, StackNavigatorConfig);
> ~~~

### <span id="routeConfigs">RouteConfigs</span>
- screen
- path
- navigationOptions
    - title
    - header
    - headerTitle
    - headerTitleAllowFontScaling
    - headerBackImage
    - headerBackTitle
    - headerTruncatedBackTitle
    - headerRight
    - headerLeft
    - headerStyle
    - headerForceInset
    - headerTitleStyle
    - headerBackTitleStyle
    - headerLeftContainerStyle
    - headerRightContainerStyle
    - headerTitleContainerStyle
    - headerTintColor
    - headerPressColorAndroid
    - headerTransparent
    - headerBackground
    - gesturesEnabled
    - gestureResponseDistance
        - horizontal 
        - vertical 
    - gestureDirection

### StackNavigatorConfig
- initialRouteName 
- initialRouteParams 
- initialRouteKey 
- navigationOptions 
- paths 
- mode 
    - card 
    - modal 
- headerMode 
    - float 
    - screen 
    - none 
- headerBackTitleVisible 
- headerTransitionPreset 
- headerLayoutPreset 
- cardStyle 
- transitionConfig 
    - transitionProps 
    - prevTransitionProps 
    - isModal 
- onTransitionStart 
- onTransitionEnd 
- transparentCard 

Navigator Props
~~~javascript
const SomeStack = createStackNavigator({
  // config
});

<SomeStack
  screenProps={/* this prop will get passed to the screen components as this.props.screenProps */}
/>
~~~

## createSwitchNavigator
> ~~~javascript 
> createSwitchNavigator(RouteConfigs, SwitchNavigatorConfig);
> ~~~

### RouteConfigs - <a href="#routeConfigs">同createStackNavigator的RouteConfigs</a>
### SwitchNavigatorConfig
- initialRouteName 
- resetOnBlur 
- paths 
- backBehavior 

## createDrawerNavigator
> ~~~javascript 
> createDrawerNavigator(RouteConfigs, DrawerNavigatorConfig);
> ~~~

### RouteConfigs - <a href="#routeConfigs">同createStackNavigator的RouteConfigs</a>
- navigationOptions
    - title
    - drawerLabel
    - drawerIcon
    - drawerLockMode
### DrawerNavigatorConfig
- drawerWidth 
- drawerPosition 
- contentComponent 
    - items 
    - activeItemKey 
    - activeTintColor 
    - activeBackgroundColor 
    - inactiveTintColor 
    - inactiveBackgroundColor 
    - onItemPress(route)
    - itemsContainerStyle 
    - itemStyle 
    - labelStyle 
    - activeLabelStyle 
    - inactiveLabelStyle 
    - iconContainerStyle 
- contentOptions 
- useNativeAnimations 
- drawerBackgroundColor 
- initialRouteName 
- order 
- paths 
- backBehavior 
  

## createTabNavigator
> ~~~javascript 
> createTabNavigator(RouteConfigs, TabNavigatorConfig);
> ~~~

### RouteConfigs - <a href="#routeConfigs">同createStackNavigator的RouteConfigs</a>
- navigationOptions 
    - title
    - tabBarVisible
    - swipeEnabled
    - tabBarIcon
    - tabBarLabel
    - tabBarOnPress
### TabNavigatorConfig
- tabBarComponent 
    - TabBarBottom - (IOS默认)
        - tabBarOptions 
            - activeTintColor 
            - activeBackgroundColor 
            - inactiveTintColor 
            - inactiveBackgroundColor 
            - showLabel 
            - style 
            - labelStyle 
            - tabStyle 
            - allowFontScaling 
            - safeAreaInset 
    - TabBarTop - (Android默认)
        - tabBarOptions 
            - activeTintColor 
            - inactiveTintColor 
            - showIcon 
            - showLabel 
            - upperCaseLabel 
            - pressColor 
            - pressOpacity 
            - scrollEnabled 
            - tabStyle 
            - indicatorStyle 
            - labelStyle 
            - iconStyle 
            - style 
            - allowFontScaling 
- tabBarPosition 
- swipeEnabled 
- animationEnabled 
- lazy 
- removeClippedSubviews 
- initialLayout 
- tabBarOptions 
- initialRouteName 
- order 
- paths 
- backBehavior 

## createBottomTabNavigator
> ~~~javascript 
> createBottomTabNavigator(RouteConfigs, BottomTabNavigatorConfig);
> ~~~

### RouteConfigs - <a href="#routeConfigs">同createStackNavigator的RouteConfigs</a>
- navigationOptions 
    - title
    - tabBarVisible
    - tabBarIcon
    - tabBarLabel
    - tabBarButtonComponent
    - tabBarAccessibilityLabel
    - tabBarTestID
    - tabBarOnPress
### BottomTabNavigatorConfig
- initialRouteName 
- order 
- paths 
- backBehavior 
- tabBarComponent 
- tabBarOptions 
    - activeTintColor 
    - activeBackgroundColor 
    - inactiveTintColor 
    - inactiveBackgroundColor 
    - showLabel 
    - showIcon 
    - style 
    - labelStyle 
    - tabStyle 
    - allowFontScaling 
    - safeAreaInset 

## createMaterialBottomTabNavigator
> ~~~javascript 
> npm install react-navigation-material-bottom-tabs
> 
> createMaterialBottomTabNavigator(RouteConfigs, MaterialBottomTabNavigatorConfig);
> ~~~



## createMaterialTopTabNavigator

## withNavigation

## withNavigationFocus

## NavigationEvents

## 实战
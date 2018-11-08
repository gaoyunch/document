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

## Stack Actions

## Drawer Actions
> ~~~javascript 
> import { DrawerActions } from 'react-navigation-drawer';
> ~~~

- openDrawer - 打开抽屉
    ~~~javascript
    this.props.navigation.dispatch(DrawerActions.openDrawer())
    ~~~
- closeDrawer - 关闭抽屉
    ~~~javascript
    this.props.navigation.dispatch(DrawerActions.closeDrawer())
    ~~~
- toggleDrawer - 切换抽屉
    ~~~javascript
    this.props.navigation.dispatch(DrawerActions.toggleDrawer())
    ~~~

## createStackNavigator

## createSwitchNavigator

## createDrawerNavigator

## createTabNavigator

## createBottomTabNavigator

## createMaterialBottomTabNavigator

## createMaterialTopTabNavigator

## withNavigation

## withNavigationFocus

## NavigationEvents

## 实战
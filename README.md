# Android-Navigation-Jetpack-Template
This is an example of Android Drawer- and Android Bottom-Navigation using Android Navigation Component (part of Android Jetpack)
## Setup
In order to use Android navigation component you should add this dependencies to ```app/build.gradle``` file.
```
  implementation "androidx.navigation:navigation-fragment:2.3.0-alpha04"
  implementation "androidx.navigation:navigation-ui:2.3.0-alpha04"
````
## Setup App theme
Make sure you change your app theme and add this themes to your ``` app/src/main/res/values/styles.xml``` file.
```
    <style name="AppTheme" parent="Theme.MaterialComponents.Light.NoActionBar">
     <!-- Customize your theme here. --> 
     </style>
    <style name="AppTheme.AppBarOverlay" parent="ThemeOverlay.MaterialComponents.Dark.ActionBar"/>
    <style name="AppTheme.PopupOverlay" parent="ThemeOverlay.MaterialComponents.Light"/>
```
## Setup Drawer Resources (Menus)
First create a ```menu_drawer_navigation.xml``` file. It should be located in ```app/src/main/res/menu/menu_drawer_navigation.xml```. If you don't have a menu folder, you should create one. To create a menu folder you should right click res folder -> New -> Android Resource Directory -> Resource type: menu.
```
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">

    <group android:checkableBehavior="single">

        <item
            android:id="@+id/first_fragment"
            android:title="@string/menu_first_fragment" />

        <item
            android:id="@+id/second_fragment"
            android:title="@string/menu_second_fragment" />

    </group>
</menu>
```
## Setup Navigation
In ```app/src/main/res``` create a folder navigation and add a ```nav_graph.xml``` file. At the end the path should look so ``` app/src/main/res/navigation/nav_graph.xml```. In ```nav.graph.xml``` you should define your fragments.\
**Important notice** Make sure, that your fragments IDs match MenuItems IDs in ```menu_drawer_navigation.xml```  Reason: *If the id of the MenuItem matches the id of the destination, the NavController can then navigate to that destination.*

```
<navigation xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/nav_graph"
    app:startDestination="@id/first_fragment">

    <fragment
        android:id="@+id/first_fragment"
        android:name="com.example.navigationtemplate.FirstFragment"
        android:label="@string/menu_first_fragment"
        tools:layout="@layout/fragment_first" />

    <fragment
        android:id="@+id/second_fragment"
        android:name="com.example.navigationtemplate.SecondFragment"
        android:label="@string/menu_second_fragment"
        tools:layout="@layout/fragment_second" />

</navigation>
```

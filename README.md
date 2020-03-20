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

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
You should follow the same steps if you want to build bottom navigation. You should create a new menu file ```app/src/main/res/menu/menu_bottom_navigation.xml``` with the following code:

```
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

**Important notice** Make sure, that your fragments IDs match MenuItems IDs in ```menu/menu_drawer_navigation.xml```  or/and ```menu/menu_bottom_navigation.xml```  Reason: *If the id of the MenuItem matches the id of the destination, the NavController can then navigate to that destination.*

## Setup Navigation
In ```app/src/main/res``` create a folder navigation and add a ```nav_graph.xml``` file. At the end the path should look so ``` app/src/main/res/navigation/nav_graph.xml```. In ```nav.graph.xml``` you should define your fragments.\

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

## Setup Drawer in Activity 
For detailed information please look at the comments in the following code.

``` <?xml version="1.0" encoding="utf-8"?>
<androidx.drawerlayout.widget.DrawerLayout
    android:id="@+id/drawer_layout"
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:fitsSystemWindows="true">

    <!-- This LinearLayout represents the contents of the screen  -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <!-- This represents the toolbar of the application  -->
        <com.google.android.material.appbar.AppBarLayout
            android:id="@+id/appbar_layout"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:theme="@style/AppTheme.AppBarOverlay">

            <androidx.appcompat.widget.Toolbar
                android:id="@+id/toolbar"
                android:layout_width="match_parent"
                android:layout_height="?attr/actionBarSize"
                app:popupTheme="@style/AppTheme.PopupOverlay"/>

        </com.google.android.material.appbar.AppBarLayout>

        <!-- This is container for the fragments  -->
        <fragment
            android:id="@+id/fragment_nav_host"
            android:name="androidx.navigation.fragment.NavHostFragment"
            android:layout_width="match_parent"
            android:layout_height="0dp"
            android:layout_weight="1"
            app:defaultNavHost="true"
            app:navGraph="@navigation/nav_graph" />

        <!-- Bottom navigation bar that -->
        <com.google.android.material.bottomnavigation.BottomNavigationView
            android:id="@+id/bottom_navigation"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            app:itemTextColor="@color/colorPrimaryDark"
            <!-- Link the menus to the view -->
            app:menu="@menu/menu_bottom_navigation" />

    </LinearLayout>

    <!-- The navigation drawer that comes from the left -->
    <com.google.android.material.navigation.NavigationView
        android:id="@+id/navigation_view"
        style="@style/Widget.Design.NavigationView"
        android:layout_width="wrap_content"
        android:layout_height="match_parent"
        android:layout_gravity="start"
        <!-- If you don't need a header you can delete this line. -->
        <!-- But if you want to use it you should create a header_layout. -->
        <!-- NOTICE: Look at layout code in the repository.-->
        app:headerLayout="@layout/layout_nav_header"
        <!-- Link the menus to the view -->
        app:menu="@menu/menu_drawer_navigation"/>

</androidx.drawerlayout.widget.DrawerLayout>
```
Now let's set up the navigation in our activity ``` app/src/main/java/com/example/navigationtemplate/MainActivity.java```.\
Setup drawer navigation:

```
    private void setUpNavigation() {
        DrawerLayout drawerLayout = findViewById(R.id.drawer_layout);
        Toolbar toolbar = findViewById(R.id.toolbar);
        NavigationView navigationView = findViewById(R.id.navigation_view);

        //Each menu is a top level destination
        appBarConfiguration = new AppBarConfiguration.Builder(R.id.first_fragment, R.id.second_fragment)
                .setOpenableLayout(drawerLayout)
                .build();

        navController = Navigation.findNavController(this, R.id.fragment_nav_host);

        //IMPORTANT When you use theme with NoActionBar you should pass appBar as a configuration
        NavigationUI.setupWithNavController(toolbar, navController, appBarConfiguration);
        //Connect view with the controller
        NavigationUI.setupWithNavController(navigationView, navController);
    }
```

Setup bottom navigation:

```
 private void setUpBottomNavigation() {
        BottomNavigationView bottomNavigationView = findViewById(R.id.bottom_navigation);
        //Connect view with the controller
        NavigationUI.setupWithNavController(bottomNavigationView, navController);
    }
```
To make your navigation work you should override ```onSupportNavigateUp```.
```
  @Override
    public boolean onSupportNavigateUp() {
        return NavigationUI.navigateUp(navController, appBarConfiguration)
                || super.onSupportNavigateUp();
    }
```
At the end don't forget to call your set up methods.
```
 @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        setUpNavigation();
        setUpBottomNavigation();
    }
```

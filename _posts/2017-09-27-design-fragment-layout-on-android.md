---
published: true
---
## Implement Main Layout


* Create a Manefist xml file **AndroidManifest.xml** and write the following code.

```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
          package="com.ray.fragment_demo">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity
            android:name=".MainActivity"
            android:label="@string/app_name"
            android:theme="@style/AppTheme.NoActionBar">
            <intent-filter>
                <action android:name="android.intent.action.MAIN"/>

                <category android:name="android.intent.category.LAUNCHER"/>
            </intent-filter>
        </activity>
        <meta-data
            android:name="io.fabric.ApiKey"
            android:value="fd7a915e23767c83f3f24669deb956f70aa90d9d" />
    </application>

    <uses-permission android:name="android.permission.INTERNET" />
</manifest>
```


* Create a class named **MainActivity.java** and write the following code.


```java
package com.ray.fragment_demo;

import android.os.Build;
import android.os.Bundle;
import android.support.design.widget.NavigationView;
import android.support.v4.view.GravityCompat;
import android.support.v4.widget.DrawerLayout;
import android.support.v7.app.AppCompatActivity;
import android.view.Gravity;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.view.Window;
import android.view.WindowManager;
import android.widget.ImageView;

import com.crashlytics.android.Crashlytics;

import io.fabric.sdk.android.Fabric;

import static com.ray.fragment_demo.NavigationDrawerPreferencesManager.NAVIGATION_LED;
import static com.ray.fragment_demo.NavigationDrawerPreferencesManager.NAVIGATION_NOTIFICATION;
import static com.ray.fragment_demo.NavigationDrawerPreferencesManager.NAVIGATION_RING;
import static com.ray.fragment_demo.NavigationDrawerPreferencesManager.NAVIGATION_VIBRATION;

public class MainActivity extends AppCompatActivity
        implements NavigationView.OnNavigationItemSelectedListener {
    public final static String TAG = MainActivity.class.getName();
    public final static String USER_ID = "USER_ID";
    public final static String FRAGMENT_LAYOUT_ID = "FRAGMENT_LAYOUT_ID";
    private EntryActivityManager entryActivityManager;
    private NavigationDrawerPreferencesManager navigationDrawerPreferencesManager;
    private DrawerLayout drawerLayout;


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.KITKAT) {
            Window window = getWindow();
            window.setFlags(
                    WindowManager.LayoutParams.FLAG_TRANSLUCENT_STATUS,
                    WindowManager.LayoutParams.FLAG_TRANSLUCENT_STATUS);
            window.setFlags(
                    WindowManager.LayoutParams.FLAG_TRANSLUCENT_NAVIGATION,
                    WindowManager.LayoutParams.FLAG_TRANSLUCENT_NAVIGATION);
        }

        setContentView(R.layout.activity_main);
        Fabric.with(this, new Crashlytics());

        getWindow().setSoftInputMode(WindowManager.LayoutParams.SOFT_INPUT_ADJUST_PAN);
        entryActivityManager = EntryActivityManager.getInstance().setEntryActivity(this);

        navigationDrawerPreferencesManager = NavigationDrawerPreferencesManager.getInstance().setActivity(this).initializeNavigationDrawer();

        drawerLayout = (DrawerLayout) findViewById(R.id.drawer_layout);
        ImageView toggleButton = (ImageView) findViewById(R.id.entry_fragment_toggle_button);
        toggleButton.bringToFront();
        toggleButton.invalidate();
        toggleButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                drawerLayout.openDrawer(Gravity.LEFT);
            }
        });

        if (savedInstanceState == null) {
            entryActivityManager.commitFragmentTransaction(R.layout.fragment_entry, null);
        } else {
            entryActivityManager.commitFragmentTransaction(savedInstanceState.getInt(FRAGMENT_LAYOUT_ID), null);
        }
    }

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        // Inflate the menu; this adds items to the action bar if it is present.
        getMenuInflater().inflate(R.menu.main, menu);
        return true;
    }
    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        // Handle action bar item clicks here. The action bar will
        // automatically handle clicks on the Home/Up button, so long
        // as you specify a parent activity in AndroidManifest.xml.
        int id = item.getItemId();

        if (id == R.id.action_settings) {
            return true;
        }

        return super.onOptionsItemSelected(item);
    }

    @SuppressWarnings("StatementWithEmptyBody")
    @Override
    public boolean onNavigationItemSelected(MenuItem item) {
        // Handle navigation view item clicks here.
        int id = item.getItemId();
        if (id == R.id.nav_home_page) {
            entryActivityManager.commitFragmentTransaction(R.layout.fragment_entry, null);
        } else if (id == R.id.nav_2nd_page) {
            entryActivityManager.commitFragmentTransaction(R.layout.fragment_chat, null);
        } else if (id == R.id.nav_contact) {
            entryActivityManager.sendFeedbackViaEmail(this, "some@email.com", "", "");
        } else if (id == R.id.nav_set_notification) {
            navigationDrawerPreferencesManager.setSwitchPreferences(this, NAVIGATION_NOTIFICATION, true);
            navigationDrawerPreferencesManager.setCheckedWithGroupSettingsRule();
        } else if (id == R.id.nav_set_ring) {
            navigationDrawerPreferencesManager.setSwitchPreferences(this, NAVIGATION_RING, true);
        } else if (id == R.id.nav_set_vibrate) {
            navigationDrawerPreferencesManager.setSwitchPreferences(this, NAVIGATION_VIBRATION, true);
        } else if (id == R.id.nav_set_led) {
            navigationDrawerPreferencesManager.setSwitchPreferences(this, NAVIGATION_LED, true);
        }

        drawerLayout.closeDrawer(GravityCompat.START);
        return true;
    }

    @Override
    public void onBackPressed() {
        DrawerLayout drawer = (DrawerLayout) findViewById(R.id.drawer_layout);
        if (drawer.isDrawerOpen(GravityCompat.START)) {
            drawer.closeDrawer(GravityCompat.START);
        } else {
            entryActivityManager.getCurrentFragment().onBackPressed(this);
        }
    }
}
```


* Create a layout xml file named **activity_main.xml** and write the following code.


```
<?xml version="1.0" encoding="utf-8"?>
<android.support.v4.widget.DrawerLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/drawer_layout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:fitsSystemWindows="true"
    tools:openDrawer="start">

    <include
        layout="@layout/app_bar_main"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>

    <android.support.design.widget.NavigationView
        android:id="@+id/nav_view"
        android:layout_width="wrap_content"
        android:layout_height="match_parent"
        android:layout_gravity="start"
        android:fitsSystemWindows="true"
        app:menu="@menu/activity_main_drawer"/>

</android.support.v4.widget.DrawerLayout>
```


* Create a layout xml file named **app_bar_main.xml** and write the following code.


```
<?xml version="1.0" encoding="utf-8"?>
<android.support.design.widget.CoordinatorLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.ray.fragment_demo.MainActivity">

    <ImageView
        android:id="@+id/entry_fragment_toggle_button"
        android:layout_width="50dp"
        android:layout_height="50dp"
        android:layout_alignParentTop="true"
        android:layout_alignParentLeft="true"
        android:layout_marginBottom="@dimen/activity_vertical_margin"
        android:layout_marginLeft="@dimen/activity_horizontal_margin"
        android:layout_marginRight="@dimen/activity_horizontal_margin"
        android:layout_marginTop="@dimen/activity_vertical_margin"
        android:src="@drawable/toggle_icon_pink"
        android:background="@null"
    />

    <include layout="@layout/content_main"/>

</android.support.design.widget.CoordinatorLayout>
```


## Implement Fragment Pages

* Create a super class named **AbstractFragment.xml** and write the following code.


```java
package com.ray.fragment_demo;

import android.app.Activity;
import android.app.Fragment;

public abstract class AbstractFragment extends Fragment {

    public abstract void onBackPressed(Activity activity);

}

```


* Create a layout class named **EntryFragment.xml** and write the following code.


```java
package com.ray.fragment_demo;

import android.app.Activity;
import android.os.Bundle;
import android.support.v4.widget.DrawerLayout;
import android.view.Gravity;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ImageView;

public class EntryFragment extends AbstractFragment {
    public final static String TAG = EntryFragment.class.getName();
    private EntryActivityManager entryActivityManager;

    @Override
    public void onBackPressed(Activity activity) {
        activity.finish();
    }

    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
        ViewGroup root = (ViewGroup) inflater.inflate(R.layout.fragment_entry, null);

        entryActivityManager = EntryActivityManager.getInstance().setEntryActivity((MainActivity) this.getActivity());

        final DrawerLayout drawer = (DrawerLayout) getActivity().findViewById(R.id.drawer_layout);

        return root;
    }

}
```


* Create a layout class named **ChatFragment.xml** and write the following code.



```java
package com.ray.fragment_demo;

import android.app.Activity;
import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;

public class ChatFragment extends AbstractFragment {
    public final static String TAG = ChatFragment.class.getName();

    @Override
    public void onBackPressed(Activity activity) {
    }

    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
        final ViewGroup root = (ViewGroup) inflater.inflate(R.layout.fragment_chat, null);

        return root;
    }

    @Override
    public void onResume() {
        super.onResume();
    }

    @Override
    public void onDestroy() {
        super.onDestroy();
    }

}
```


* Create a layout xml file named **fragment_entry.xml** and write the following code.



```java
<RelativeLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/content_entry"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    app:layout_behavior="@string/appbar_scrolling_view_behavior"
    >

    <TextView android:layout_width="wrap_content" android:layout_height="wrap_content"
              android:layout_centerInParent="true"
              android:textSize="50sp"
              android:text="HOME"/>

</RelativeLayout>

```


* Create a layout xml file named **fragment_chat.xml** and write the following code.


```java
<RelativeLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    xmlns:android="http://schemas.android.com/apk/res/android">

    <TextView android:layout_width="wrap_content" android:layout_height="wrap_content"
              android:layout_centerInParent="true"
              android:textSize="50sp"
              android:text="2nd"/>

</RelativeLayout>
```


## Implement Supportive Manager Classes

* Create a manager singleton class named **EntryActivityManager.java** and write the following code.


```java
package com.ray.fragment_demo;

import android.app.Activity;
import android.app.ActivityManager;
import android.app.Fragment;
import android.app.FragmentTransaction;
import android.content.ComponentName;
import android.content.Context;
import android.content.Intent;
import android.net.Uri;
import android.os.Build;
import android.os.Bundle;
import android.os.PowerManager;
import android.support.annotation.Nullable;

import java.util.List;
import java.util.Locale;

import static android.content.Context.ACTIVITY_SERVICE;

public class EntryActivityManager {
    public final static String TAG = EntryActivityManager.class.getName();

    public final static int NUM_UNIT_SECOND = 1000;

    final static String[] fragments = {
            EntryFragment.class.getCanonicalName(),
            ChatFragment.class.getCanonicalName()
    };

    private static EntryActivityManager instance = null;
    private MainActivity entryActivity;
    private AbstractFragment currentFragment;
    private int currentFragmentLayoutId = -1;

    protected EntryActivityManager() {

    }

    public static EntryActivityManager getInstance() {
        if (instance == null) {
            synchronized (EntryActivityManager.class) {
                if (instance == null) {
                    instance = new EntryActivityManager();
                }
            }
        }

        return instance;
    }

    public static String getUserDeviceLanguage() {
        return Locale.getDefault().getDisplayLanguage(Locale.US).toUpperCase(Locale.US); // CHINESE
//        return Locale.getDefault().getLanguage().toUpperCase(Locale.US); // ZH
//        return Locale.getDefault().toString().toUpperCase(Locale.US); // ZH_TW
    }

    public static void sendFeedbackViaEmail(final Activity activity, String feedbackEmail, String feedbackSubject, String feedbackBody) {
        Intent email = new Intent(Intent.ACTION_SENDTO, Uri.fromParts("mailto", feedbackEmail, null));
        email.putExtra(Intent.EXTRA_SUBJECT, feedbackSubject);
        email.putExtra(Intent.EXTRA_TEXT, feedbackBody);
        activity.startActivity(Intent.createChooser(email, "Send email to..."));
    }

    public static boolean isEmailSyntaxCorrect(String emailAddressString) {
        return emailAddressString.matches("[a-zA-Z]+[0-9a-zA-Z\\-_]*@[0-9a-zA-Z\\-_]+\\.[a-z]+");
    }

    public static String byte2HexFormatted(byte[] arr) {
        StringBuilder str = new StringBuilder(arr.length * 2);
        for (int i = 0; i < arr.length; i++) {
            String h = Integer.toHexString(arr[i]);
            int l = h.length();
            if (l == 1) h = "0" + h;
            if (l > 2) h = h.substring(l - 2, l);
            str.append(h.toUpperCase());
            if (i < (arr.length - 1)) str.append(':');
        }
        return str.toString();
    }

    public static boolean isApplicationOnTopOfStack(Activity activity) {
        ActivityManager am = (ActivityManager) activity.getSystemService(ACTIVITY_SERVICE);

        // get the info from the currently running task
        List<ActivityManager.RunningTaskInfo> taskInfo = am.getRunningTasks(1);

        ComponentName componentInfo = taskInfo.get(0).topActivity;
        if (componentInfo.getPackageName().equalsIgnoreCase(activity.getPackageName())) {
            return true;
        } else {
            return false;
        }
    }

    public static boolean isScreenOn(Activity activity) {
        PowerManager pm = (PowerManager) activity.getSystemService(Context.POWER_SERVICE);
        if (Build.VERSION.SDK_INT < Build.VERSION_CODES.KITKAT_WATCH) {
            return pm.isScreenOn();
        } else {
            return pm.isInteractive();
        }
    }

    public synchronized EntryActivityManager setEntryActivity(MainActivity entryActivity) {
        this.entryActivity = entryActivity;
        return instance;
    }

    public AbstractFragment getCurrentFragment() {
        return currentFragment;
    }

    public synchronized void setCurrentFragment(AbstractFragment currentFragment) {
        this.currentFragment = currentFragment;
    }

    public int getCurrentFragmentLayoutId() {
        return currentFragmentLayoutId;
    }

    public synchronized void setCurrentFragmentLayoutId(int fragmentLayoutId) {
        this.currentFragmentLayoutId = fragmentLayoutId;
    }

    public synchronized void commitFragmentTransaction(int layoutId, @Nullable Bundle bundle) {
        FragmentTransaction tx = entryActivity.getFragmentManager().beginTransaction();
        AbstractFragment fragment = (AbstractFragment) Fragment.instantiate(entryActivity, getFragmentClassNameByLayoutId(layoutId));
        fragment.setArguments(bundle);
        setCurrentFragment(fragment);
        setCurrentFragmentLayoutId(layoutId);
        tx.replace(R.id.main_activity_fragment_layout, fragment);
//        tx.addToBackStack(null);
        tx.commit();
    }

    public static synchronized String getFragmentClassNameByLayoutId(int layoutId) {
        switch (layoutId) {
            case R.layout.fragment_entry:
                return fragments[0];
            case R.layout.fragment_chat:
                return fragments[1];
        }
        return fragments[0];
    }

}

```


* Create a  manager singleton class named **NavigationDrawerPreferencesManager.java** and write the following code.



```java
package com.ray.fragment_demo;

import android.app.Activity;
import android.content.Context;
import android.content.res.ColorStateList;
import android.graphics.Color;
import android.support.design.widget.NavigationView;
import android.support.v7.widget.SwitchCompat;
import android.widget.CompoundButton;

public class NavigationDrawerPreferencesManager {
    public final static String TAG = NavigationDrawerPreferencesManager.class.getName();
    public final static int NAVIGATION_GROUP_SETTINGS = 2;
    public final static String NAVIGATION_NOTIFICATION = "nav_notification";
    public final static String NAVIGATION_RING = "nav_ring";
    public final static String NAVIGATION_VIBRATION = "nav_vibration";
    public final static String NAVIGATION_LED = "nav_led";
    public final static String[] NAVIGATION_SWITCH_KEYS = new String[]{
            NAVIGATION_NOTIFICATION,
            NAVIGATION_RING,
            NAVIGATION_VIBRATION,
            NAVIGATION_LED
    };

    private static NavigationDrawerPreferencesManager instance = null;
    private SharedPreferencesManager sharedPreferencesManager;
    private NavigationView navigationView;
    private Activity activity;

    protected NavigationDrawerPreferencesManager() {
        sharedPreferencesManager = SharedPreferencesManager.getInstance();
    }

    public static NavigationDrawerPreferencesManager getInstance() {
        if (instance == null) {
            synchronized (NavigationDrawerPreferencesManager.class) {
                if (instance == null) {
                    instance = new NavigationDrawerPreferencesManager();
                }
            }
        }
        return instance;
    }

    public NavigationDrawerPreferencesManager setActivity(Activity activity) {
        this.activity = activity;
        return this;
    }

    public NavigationDrawerPreferencesManager initializeNavigationDrawer() {
        final NavigationView navigationView = (NavigationView) activity.findViewById(R.id.nav_view);
        setNavigationView(navigationView);

        navigationView.setItemTextColor(ColorStateList.valueOf(Color.BLACK));
        MyLogManager.i(TAG, String.format("onCreateView: menu size %d, submenu size %d, (0) %s, %s", navigationView.getMenu().size(), navigationView.getMenu().getItem(NAVIGATION_GROUP_SETTINGS).getSubMenu().size(), navigationView.getMenu().getItem(1).getSubMenu().getItem(0).getTitle(), navigationView.getMenu().getItem(0).getTitle()));
        for (int a = 0; a < navigationView.getMenu().getItem(NAVIGATION_GROUP_SETTINGS).getSubMenu().size(); a++) {
            final int index = a;
            SwitchCompat switchCompat = ((SwitchCompat) navigationView.getMenu().getItem(NAVIGATION_GROUP_SETTINGS).getSubMenu().getItem(a).getActionView().findViewById(R.id.drawer_switch));
            switchCompat.setChecked(instance.getSwitchPreferences(activity, NavigationDrawerPreferencesManager.NAVIGATION_SWITCH_KEYS[index], true));
            setCheckedWithGroupSettingsRule();
            switchCompat.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
                @Override
                public void onCheckedChanged(CompoundButton compoundButton, boolean b) {
                    MyLogManager.i(TAG, String.format("onCreateView onCheckedChanged: %s %s", NAVIGATION_SWITCH_KEYS[index], "" + b));
                    instance.setSwitchPreferences(activity, NAVIGATION_SWITCH_KEYS[index], b);

                    if (NAVIGATION_SWITCH_KEYS[index].equals(NAVIGATION_NOTIFICATION)) setCheckedWithGroupSettingsRule();

                }
            });
        }

        navigationView.setNavigationItemSelectedListener((MainActivity) activity);
        return this;
    }

    public NavigationDrawerPreferencesManager setNavigationView(NavigationView navigationView) {
        this.navigationView = navigationView;
        return this;
    }

    public void setSwitchPreferences(Context context, String key, boolean value) {
        sharedPreferencesManager.setBooleanValue(context, key, value);
    }

    public boolean getSwitchPreferences(Context context, String key, boolean defaultValue) {
        return sharedPreferencesManager.getBooleanValue(context, key, defaultValue);
    }

    public void setCheckedWithGroupSettingsRule() {
        // if close notification, then ring, vibration, led will be disabled at the same time
        int[] disableTargets = {1, 2, 3};
        for (int c = 0; c < disableTargets.length; c++) {
            ((SwitchCompat) navigationView.getMenu().getItem(NAVIGATION_GROUP_SETTINGS).getSubMenu().getItem(disableTargets[c]).getActionView().findViewById(R.id.drawer_switch)).setEnabled(
                    getSwitchPreferences(activity, NAVIGATION_NOTIFICATION, true)
            );
        }
    }

}
```


* Create a manager singleton class named **SharedPreferencesManager.java** and write the following code.


```java
package com.ray.fragment_demo;

import android.content.Context;
import android.content.SharedPreferences;
import android.support.annotation.Nullable;

import static android.content.Context.MODE_PRIVATE;

public class SharedPreferencesManager {
    public final static String PREFERENCES_APP = "PREFERENCES_APP";

    private static SharedPreferencesManager instance = null;

    public static SharedPreferencesManager getInstance() {
        if (instance == null) {
            synchronized (SharedPreferencesManager.class) {
                if (instance == null) {
                    instance = new SharedPreferencesManager();
                }
            }
        }
        return instance;
    }

    protected SharedPreferencesManager() {

    }

    public static synchronized void setStringValues(Context context, String[] key, String[] value) {
        if (key == null || value == null || key.length != value.length) return;

        SharedPreferences.Editor editor = context.getSharedPreferences(PREFERENCES_APP, MODE_PRIVATE).edit();
        for (int a=0; a<key.length; a++) {
            editor.putString(key[a], value[a]);
        }

        editor.apply();
    }

    public static synchronized void setStringValue(Context context, String key, String value) {
        SharedPreferences.Editor editor = context.getSharedPreferences(PREFERENCES_APP, MODE_PRIVATE).edit();
        editor.putString(key, value);

        editor.apply();
    }

    public static String getStringValue(Context context, String key, @Nullable String defaultValue) {
        SharedPreferences preferences = context.getSharedPreferences(PREFERENCES_APP, MODE_PRIVATE);
        return preferences.getString(key, defaultValue);
    }

    public static synchronized void setBooleanValue(Context context, String key, boolean value) {
        SharedPreferences.Editor editor = context.getSharedPreferences(PREFERENCES_APP, MODE_PRIVATE).edit();
        editor.putBoolean(key, value);

        editor.apply();
    }

    public static boolean getBooleanValue(Context context, String key, @Nullable boolean defaultValue) {
        SharedPreferences preferences = context.getSharedPreferences(PREFERENCES_APP, MODE_PRIVATE);
        return preferences.getBoolean(key, defaultValue);
    }

    public static synchronized void setIntegerValue(Context context, String key, int value) {
        SharedPreferences.Editor editor = context.getSharedPreferences(PREFERENCES_APP, MODE_PRIVATE).edit();
        editor.putInt(key, value);

        editor.apply();
    }

    public static int getIntegerValue(Context context, String key, @Nullable int defaultValue) {
        SharedPreferences preferences = context.getSharedPreferences(PREFERENCES_APP, MODE_PRIVATE);
        return preferences.getInt(key, defaultValue);
    }
}

```


## Coding Resources

* Create a resource file named **res/values/strings.xml** and write the following code.


```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="app_name">Fragment Demo</string>
    <string name="action_settings">Action Settings</string>

    <string name="navigation_drawer_title_home_fragment">Home</string>
    <string name="navigation_drawer_title_2nd_fragment">2nd Page</string>

    <string name="navigation_drawer_title_group_shortcut">Fragment Shortcut</string>

    <string name="navigation_drawer_title_contact_support">Contact Me</string>
    <string name="navigation_drawer_title_settings">Settings</string>
    <string name="navigation_drawer_title_notification_switch">Notification</string>
    <string name="navigation_drawer_title_ring_switch">Ring</string>
    <string name="navigation_drawer_title_vibration_switch">Vibration</string>
    <string name="navigation_drawer_title_led_switch">LED Blink</string>
</resources>

```


* Create a resource file named **res/values/styles.xml** and write the following code.


```
<?xml version="1.0" encoding="utf-8"?>
<resources>

    <!-- Base application theme. -->
    <style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
        <!-- Customize your theme here. -->

        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>
    </style>
    <style name="AppTheme.NoActionBar">
        <item name="windowActionBar">false</item>
        <item name="windowNoTitle">true</item>
        <item name="android:windowTranslucentStatus">true</item>
        <item name="android:windowTranslucentNavigation">true</item>
    </style>
    <style name="AppTheme.AppBarOverlay" parent="ThemeOverlay.AppCompat.Dark.ActionBar"/>
    <style name="AppTheme.PopupOverlay" parent="ThemeOverlay.AppCompat.Light"/>
    <style name="ChatDrawer">
        <item name="android:textSize">18sp</item>
    </style>
    <style name="BrandedSwitch">
        <item name="colorAccent">@color/colorAccent</item>
    </style>
</resources>

```


* Create a resource file named **res/menu/activity_main_drawer.xml** and write the following code.


```
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:app="http://schemas.android.com/apk/res-auto">

    <group android:checkableBehavior="single">

        <item
            android:id="@+id/nav_contact"
            android:icon="@mipmap/ic_launcher"
            app:itemTextColor="@color/colorAccent"
            android:title="@string/navigation_drawer_title_contact_support"/>
    </group>

    <item android:title="@string/navigation_drawer_title_group_shortcut">
        <menu>
            <item
                android:id="@+id/nav_home_page"
                android:icon="@mipmap/ic_launcher"
                android:title="@string/navigation_drawer_title_home_fragment"/>
            <item
                android:id="@+id/nav_2nd_page"
                android:icon="@mipmap/ic_launcher"
                android:title="@string/navigation_drawer_title_2nd_fragment"/>
        </menu>
    </item>

    <item android:title="@string/navigation_drawer_title_settings">
        <menu>
            <item
                android:id="@+id/nav_set_notification"
                app:actionLayout="@layout/drawer_switch"
                android:icon="@mipmap/ic_launcher"
                android:title="@string/navigation_drawer_title_notification_switch"/>
            <item
                android:id="@+id/nav_set_ring"
                app:actionLayout="@layout/drawer_switch"
                android:icon="@mipmap/ic_launcher"
                android:title="@string/navigation_drawer_title_ring_switch"/>
            <item
                android:id="@+id/nav_set_vibrate"
                app:actionLayout="@layout/drawer_switch"
                android:icon="@mipmap/ic_launcher"
                android:title="@string/navigation_drawer_title_vibration_switch"/>
            <item
                android:id="@+id/nav_set_led"
                app:actionLayout="@layout/drawer_switch"
                android:icon="@mipmap/ic_launcher"
                android:title="@string/navigation_drawer_title_led_switch"/>
        </menu>
    </item>

</menu>

```


* Create a resource file named **res/layout/drawer_switch.xml** and write the following code.


```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="horizontal" android:layout_width="match_parent"
              android:layout_height="match_parent">

    <android.support.v7.widget.SwitchCompat
        android:id="@+id/drawer_switch"
        android:layout_width="fill_parent"
        android:layout_height="match_parent"
        android:theme="@style/BrandedSwitch"
        android:checked="true"
        android:text=""/>

</LinearLayout>
```

![Home Fragment]({{site.baseurl}}/images/Screenshot_1506502739.png =200x) | ![Drawer Layout]({{site.baseurl}}/images/Screenshot_1506502686.png =200x) | ![2nd Fragment]({{site.baseurl}}/images/Screenshot_1506502684.png =200x)

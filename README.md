## ez-utils
this is an WIP project, a collection of utility and tools for faster and better development

## Import:

#### Step 1. Add the JitPack repository to your build file

Add it in your root build.gradle at the end of repositories:

	allprojects {
		repositories {
			...
			maven { url 'https://jitpack.io' }
		}
	}

#### Step 2. Add the dependency

    dependencies {
	        implementation 'com.github.MansourM.ez-utils:{$module}:{$version}'
	}

###### Current Version 
[![](https://jitpack.io/v/MansourM/ez-utils.svg)](https://jitpack.io/#MansourM/ez-utils)

### Modules
"android-font-awesome" : use font awesome icons in android textviews or set them as drawables ([parent project](https://github.com/ravi8x/Android-Font-Awesome "parent project"))

Referring Icon:
-----
Font Awesome provides three set of icons **Regular**, **Solid** and **Brand**. All the icons can be referred from `Strings` resource file. For example,

`@string/fa_map` - Regular map icon

`@string/fa_heart_solid` - Solid heart icon

`@string/fa_facebook` - Facebook brand icon.

Displaying Text Icon: FontTextView
----
To display an icon in xml layout, use the **FontTextView** widget. This class is extended from **TextView**, so all the TextView related properties will apply.
```java
<ir.masterz.mansour.ez.fontawesome.FontTextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/fa_calendar_check_solid"
            android:textColor="@color/icon_color"
            android:textSize="@dimen/icon_size"
            app:solid_icon="true" />
```

`solid_icon`: Use this attribute to display a solid icon (true / false).
`brand_icon`: Use this attribute to display a brand icon (true / false).

Displaying drawable Icon: FontDrawable
----
If you want to set an icon to a widget (buttons, menus, bottom sheet, navigation drawer), use the **FontDrawable** class to create font awesome drawable.

Here [Paper Plane](https://fontawesome.com/icons/paper-plane?style=solid) icon is set to **Floating Action Button**
```java
FloatingActionButton fab = findViewById(R.id.fab);

// using paper plane icon for FAB
FontDrawable drawable = new FontDrawable(this, R.string.fa_paper_plane_solid, true, false);

// white color to icon
drawable.setTextColor(ContextCompat.getColor(this, android.R.color.white));
fab.setImageDrawable(drawable);
```

Displaying Icons in Menus (Bottom Navigation, Navigation Drawer, Toolbar etc.,)
----
You can also display Font Awesome icons in UI elements those use menu file to render items. In the below example, font awesome icons are set to Navigation Drawer items.
```java
public class MainActivity extends AppCompatActivity
        implements NavigationView.OnNavigationItemSelectedListener {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        intDrawerLayout();
    }

    /**
     * Changing navigation drawer icons
     * This involves looping through menu items and applying icons
     */
    private void intDrawerLayout() {
        NavigationView navigationView = findViewById(R.id.nav_view);
        navigationView.setNavigationItemSelectedListener(this);

        ImageView iconHeader = navigationView.getHeaderView(0).findViewById(R.id.nav_header_icon);
        FontDrawable drawable = new FontDrawable(this, R.string.fa_font_awesome, false, true);
        drawable.setTextColor(ContextCompat.getColor(this, android.R.color.white));
        drawable.setTextSize(50);
        iconHeader.setImageDrawable(drawable);

        int[] icons = {
                R.string.fa_home_solid, R.string.fa_calendar_alt_solid, R.string.fa_user_solid,
                R.string.fa_heart_solid, R.string.fa_comment_solid, R.string.fa_dollar_sign_solid, R.string.fa_gift_solid
        };
        renderMenuIcons(navigationView.getMenu(), icons, true, false);

        int[] iconsSubmenu = {R.string.fa_cog_solid, R.string.fa_sign_out_alt_solid};

        renderMenuIcons(navigationView.getMenu().getItem(7).getSubMenu(), iconsSubmenu, true, false);
    }

    /**
     * Looping through menu icons are applying font drawable
     */
    private void renderMenuIcons(Menu menu, int[] icons, boolean isSolid, boolean isBrand) {
        for (int i = 0; i < menu.size(); i++) {
            MenuItem menuItem = menu.getItem(i);
            if (!menuItem.hasSubMenu()) {
                FontDrawable drawable = new FontDrawable(this, icons[i], isSolid, isBrand);
                drawable.setTextColor(ContextCompat.getColor(this, R.color.icon_nav_drawer));
                drawable.setTextSize(22);
                menu.getItem(i).setIcon(drawable);
            }
        }
    }
}
```

![Demo](https://www.androidhive.info/wp-content/uploads/2019/03/android-font-awesome-navigation-drawer.png)

Note:
-----
This library includes the **Free** font awesome icons only, premium icons are not available.
	

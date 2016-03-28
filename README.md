# SmartTabLayout
[![Maven Central][maven_central_badge_svg]][maven_central_badge_app] [![Android Arsenal][android_arsenal_badge_svg]][android_arsenal_badge_link] [![Android Weekly][android_weekly_badge_svg]][android_weekly_badge_link]

![icon][demo_icon]

A custom ViewPager title strip which gives continuous feedback to the user when scrolling.

This library has been added some features and utilities based on [android-SlidingTabBasic][google_slidingtabbasic] project of Google Samples.


![SmartTabLayout Demo1][demo1_gif] ![SmartTabLayout Demo2][demo2_gif]
![SmartTabLayout Demo3][demo3_gif] ![SmartTabLayout Demo4][demo4_gif]
![SmartTabLayout Demo5][demo5_gif] ![SmartTabLayout Demo6][demo6_gif]
![SmartTabLayout Demo7][demo7_gif]


Try out the sample application on the Play Store.

[![Get it on Google Play][googleplay_store_badge]][demo_app]

# Usage

_(For a working implementation of this project see the demo/ folder.)_

Add the dependency to your build.gradle.

```
dependencies {
    compile 'com.ogaclejapan.smarttablayout:library:1.6.0@aar'

    //Optional: see how to use the utility.
    compile 'com.ogaclejapan.smarttablayout:utils-v4:1.6.0@aar'

    //Optional: see how to use the utility.
    compile 'com.ogaclejapan.smarttablayout:utils-v13:1.6.0@aar'
}
```

Include the SmartTabLayout widget in your layout.
This should usually be placed above the ViewPager it represents.

```xml

<com.ogaclejapan.smarttablayout.SmartTabLayout
    android:id="@+id/viewpagertab"
    android:layout_width="match_parent"
    android:layout_height="48dp"
    app:stl_indicatorAlwaysInCenter="false"
    app:stl_indicatorWithoutPadding="false"
    app:stl_indicatorInFront="false"
    app:stl_indicatorInterpolation="smart"
    app:stl_indicatorGravity="bottom"
    app:stl_indicatorColor="#40C4FF"
    app:stl_indicatorThickness="4dp"
    app:stl_indicatorWidth="auto"
    app:stl_indicatorCornerRadius="2dp"
    app:stl_overlineColor="#4D000000"
    app:stl_overlineThickness="0dp"
    app:stl_underlineColor="#4D000000"
    app:stl_underlineThickness="1dp"
    app:stl_dividerColor="#4D000000"
    app:stl_dividerThickness="1dp"
    app:stl_defaultTabBackground="?attr/selectableItemBackground"
    app:stl_defaultTabTextAllCaps="true"
    app:stl_defaultTabTextColor="#FC000000"
    app:stl_defaultTabTextSize="12sp"
    app:stl_defaultTabTextHorizontalPadding="16dp"
    app:stl_defaultTabTextMinWidth="0dp"
    app:stl_distributeEvenly="false"
    app:stl_clickable="true"
    app:stl_titleOffset="24dp"
    app:stl_drawDecorationAfterTab="false"
    />

<android.support.v4.view.ViewPager
    android:id="@+id/viewpager"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:layout_below="@id/viewpagertab"
    />

```

In your onCreate method (or onCreateView for a fragment), bind the widget to the ViewPager.
(If you use a utility together, you can easily add items to PagerAdapter)

e.g. ViewPager of v4.Fragment

```java

FragmentPagerItemAdapter adapter = new FragmentPagerItemAdapter(
        getSupportFragmentManager(), FragmentPagerItems.with(this)
        .add(R.string.titleA, PageFragment.class)
        .add(R.string.titleB, PageFragment.class)
        .create());

ViewPager viewPager = (ViewPager) findViewById(R.id.viewpager);
viewPager.setAdapter(adapter);

SmartTabLayout viewPagerTab = (SmartTabLayout) findViewById(R.id.viewpagertab);
viewPagerTab.setViewPager(viewPager);

```

(Optional) If you use an OnPageChangeListener with your view pager you should set it in the widget rather than on the pager directly.


```java

viewPagerTab.setOnPageChangeListener(mPageChangeListener);

```

(Optional) Using the FragmentPagerItemAdapter of utility, you will be able to get a position in the Fragment side.

```java

int position = FragmentPagerItem.getPosition(getArguments());

```

This position will help to implement the parallax scrolling header that contains the ViewPager :P

# Attributes

There are several attributes you can set:

| attr | description |
|:---|:---|
| stl_indicatorAlwaysInCenter | 如果设置为true，有源标签总是显示在中心（如报刊亭的谷歌应用程序），默认为false |
| stl_indicatorWithoutPadding | 如果设置为真，画出没有填充标签的指标，默认为假 |
| stl_indicatorInFront | 在前面的下划线，默认的假画 |
| stl_indicatorInterpolation | 指标的行为：: 'linear' or 'smart' |
| stl_indicatorGravity | 指示器的位置: 'bottom' or 'top' or 'center', default 'bottom' |
| stl_indicatorColor | 指示剂颜色 |
| stl_indicatorColors | 该指标的多个颜色，可以设置每个标签的颜色 |
| stl_indicatorThickness | 指标的厚度 |
| stl_indicatorWidth | 指标的宽度(width), default 'auto' |
| stl_indicatorCornerRadius | 圆角半径的指示器 |
| stl_overlineColor | 顶线的颜色 |
| stl_overlineThickness | 顶线厚度 |
| stl_underlineColor | 底线的颜色 |
| stl_underlineThickness | 底线的厚度 |
| stl_dividerColor | 标签的颜色之间的分隔 |
| stl_dividerColors | 制表符分隔的多个颜色，可以设置每个标签的颜色 |
| stl_dividerThickness | 间隔(divider)的厚度 |
| stl_defaultTabBackground | 背景中每个选项卡。一般来说，设置statelistdrawable |
| stl_defaultTabTextAllCaps | 如果设置为真，所有标签的标题将是大写的，default true |
| stl_defaultTabTextColor | 默认的选项卡的文本颜色 |
| stl_defaultTabTextSize | 默认的选项卡的文本大小 |
| stl_defaultTabTextHorizontalPadding | 默认情况下包含的选项卡的文本布局填充 |
| stl_defaultTabTextMinWidth | tab最小宽度 |
| stl_customTabTextLayoutId | 布局标识自定义选项卡。如果不指定布局，使用默认选项卡 |
| stl_customTabTextViewId | 自定义选项卡布局中的文本视图标识。如果你不确定customtabtextlayoutid，不工作 |
| stl_distributeEvenly | 如果设置为真，每个标签都有相同的权重, default false |
| stl_clickable | 如果设置为假，请禁用选项卡的选择, default true |
| stl_titleOffset | 如果设置为“auto_center，滑块位置的标签中会不断向中心。如果指定一个维度将它从左边偏移，默认24dp|
| stl_drawDecorationAfterTab | Draw the decoration(indicator and lines) after drawing of tab, default false 绘制标签后的装饰（指标和线） |

*__Notes:__ Both 'stl_indicatorAlwaysInCenter' and 'stl_distributeEvenly' if it is set to true, it will throw UnsupportedOperationException.*

# How to customize the tab

The customization of tab There are three ways.

* Customize the attribute
* SmartTabLayout#setCustomTabView(int layoutResId, int textViewId)
* SmartTabLayout#setCustomTabView(TabProvider provider)

If set the TabProvider, can build a view for each tab.

```java

public class SmartTabLayout extends HorizontalScrollView {

    //...

    /**
     * Create the custom tabs in the tab layout. Set with
     * {@link #setCustomTabView(com.ogaclejapan.smarttablayout.SmartTabLayout.TabProvider)}
     */
    public interface TabProvider {

        /**
         * @return Return the View of {@code position} for the Tabs
         */
        View createTabView(ViewGroup container, int position, PagerAdapter adapter);

    }

    //...
}

```

# How to use the utility

Utility has two types available to suit the Android support library.

* utils-v4 library contains the PagerAdapter implementation class for _android.support.v4.app.Fragment_
* utils-v13 library contains the PagerAdapter implementation class for _android.app.Fragment_

The two libraries have different Android support libraries that depend,
but implemented functionality is the same.

## PagerAdapter for View-based Page

```java

ViewPagerItemAdapter adapter = new ViewPagerItemAdapter(ViewPagerItems.with(this)
        .add(R.string.title, R.layout.page)
        .add("title", R.layout.page)
        .create());

viewPager.setAdapter(adapter);

//...

public void onPageSelected(int position) {

  //.instantiateItem() from until .destroyItem() is called it will be able to get the View of page.
  View page = adapter.getPage(position);

}


```

## PagerAdapter for Fragment-based Page

Fragment-based PagerAdapter There are two implementations.
Please differences refer to the library documentation for Android.

* FragmentPagerItemAdapter extends FragmentPagerAdapter
* FragmentStatePagerItemAdapter extends FragmentStatePagerAdapter

```java

FragmentPagerItemAdapter adapter = new FragmentPagerItemAdapter(
        getSupportFragmentManager(), FragmentPagerItems.with(this)
        .add(R.string.title, PageFragment.class),
        .add(R.string.title, WithArgumentsPageFragment.class, new Bundler().putString("key", "value").get()),
        .add("title", PageFragment.class)
        .create());

viewPager.setAdapter(adapter);

//...

public void onPageSelected(int position) {

  //.instantiateItem() from until .destoryItem() is called it will be able to get the Fragment of page.
  Fragment page = adapter.getPage(position);

}

```

*__Notes:__ If using fragment inside a ViewPager, Must be use [Fragment#getChildFragmentManager()](http://developer.android.com/reference/android/support/v4/app/Fragment.html#getChildFragmentManager).*

# Apps Using SmartTabLayout

* [Qiitanium][qiitanium]
* [Ameba](https://play.google.com/store/apps/details?id=jp.ameba&hl=ja)

# LICENSE

```
Copyright (C) 2015 ogaclejapan
Copyright (C) 2013 The Android Open Source Project

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

[demo1_gif]: https://raw.githubusercontent.com/ogaclejapan/SmartTabLayout/master/art/demo1.gif
[demo2_gif]: https://raw.githubusercontent.com/ogaclejapan/SmartTabLayout/master/art/demo2.gif
[demo3_gif]: https://raw.githubusercontent.com/ogaclejapan/SmartTabLayout/master/art/demo3.gif
[demo4_gif]: https://raw.githubusercontent.com/ogaclejapan/SmartTabLayout/master/art/demo4.gif
[demo5_gif]: https://raw.githubusercontent.com/ogaclejapan/SmartTabLayout/master/art/demo5.gif
[demo6_gif]: https://raw.githubusercontent.com/ogaclejapan/SmartTabLayout/master/art/demo6.gif
[demo7_gif]: https://raw.githubusercontent.com/ogaclejapan/SmartTabLayout/master/art/demo7.gif
[demo_app]: https://play.google.com/store/apps/details?id=com.ogaclejapan.smarttablayout.demo&referrer=utm_source%3Dgithub
[demo_icon]: https://raw.githubusercontent.com/ogaclejapan/SmartTabLayout/master/art/icon.png
[googleplay_store_badge]: https://developer.android.com/images/brand/en_generic_rgb_wo_60.png
[maven_central_badge_svg]: https://maven-badges.herokuapp.com/maven-central/com.ogaclejapan.smarttablayout/library/badge.svg?style=flat
[maven_central_badge_app]: https://maven-badges.herokuapp.com/maven-central/com.ogaclejapan.smarttablayout/library
[android_arsenal_badge_svg]: https://img.shields.io/badge/Android%20Arsenal-SmartTabLayout-brightgreen.svg?style=flat
[android_arsenal_badge_link]: http://android-arsenal.com/details/1/1683
[android_weekly_badge_svg]: https://img.shields.io/badge/AndroidWeekly-%23148-blue.svg
[android_weekly_badge_link]: http://androidweekly.net/issues/issue-148
[qiitanium]: https://github.com/ogaclejapan/Qiitanium
[google_slidingtabbasic]: https://github.com/googlesamples/android-SlidingTabsBasic

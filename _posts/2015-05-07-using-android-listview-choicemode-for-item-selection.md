---
layout: post
title: "Using ListView Built-in Item ChoiceMode for Item Selection"
date: 2015-04-28 23:13:29
category: Android
tags: [Android, ListView, GridView, AbsListView]
---

### ListVIew Item Selection

**Q: Should we need to track/untrack item state by ourself?**

A: NO. You don't need to do this. Let ListView(or GridView) built-in [ChoiceMode](http://developer.android.com/reference/android/widget/AbsListView.html#attr_android:choiceMode) help you to do this. If we want to mark some item(s) been selected, we don't need to add an extra property (maybe named checked or something...) to track. Just [setChoiceMode]( http://developer.android.com/reference/android/widget/AbsListView.html#setChoiceMode(int) )

    mListView.setChoiceMode(AbsListView.CHOICE_MODE_SINGLE);

When we done this, the mListView object will track the selected item (or position), you could call the follwing realted APIs to get the information.

    mListView.getCheckedItemCount() //get the count of selected items
    mListView.getCheckedItemIds() //get the ids of selected items
    mListView.getCheckedItemPosition() //get the selected item
    mListView.getCheckedItemPositions() //get the all the selected items

**Q: What if we want to mark the selected item on UI?**

A: In the past, I'm not familiar with ListView, I usually implement this feature like this way

    public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
        view.setSelected(true);
    }

, and the view object applied with an selector drawable resource with a condition **android:state_selected="true"**.

Nevertheless, we don't need to implement like this way.

Reference to Android [AbsListView source](http://grepcode.com/file/repository.grepcode.com/java/ext/com.google.android/android/5.0.0_r1/android/widget/AbsListView.java#AbsListView.updateOnScreenCheckedViews%28%29), an AbsListView will update all checked items as **activated**, or update as **checked** when the view is an instance of [Checkable](http://developer.android.com/reference/android/widget/Checkable.html). So, just create a drawable selector like this

    <?xml version="1.0" encoding="utf-8"?>
    <selector xmlns:android="http://schemas.android.com/apk/res/android">

        <!-- pressed -->
        <item android:drawable="@color/material_blue_grey_800" android:state_pressed="true" />
        <!-- focused -->
        <item android:drawable="@color/material_blue_grey_800" android:state_activated="true" />
        <!-- default -->
        <item android:drawable="@color/background_floating_material_light" />
    </selector>

and apply this selector to you item layout.

#### Recursive State Activated

When a parent layout is set as **state_activated**, all the children are set as **state_activated**. Therefore, you don't need to handle the change of state for each child, jsut create a selector resource and apply it to children you want to do some UI viration when the state is set as activated.

#### OnItemClickListener

Basically, if you implement [ ListView/GridView](http://developer.android.com/reference/android/widget/AbsListView.html) with [ChoiceMode](http://developer.android.com/reference/android/widget/AbsListView.html#attr_android:choiceMode), you already could select item(s) which been touched without need to setup an [OnItemClickListener](http://developer.android.com/reference/android/widget/AdapterView.OnItemClickListener.html) to track/untrack state of clicked items. We only do this when we really want to handle some things while item is clicked.

when you using some [Checkable](http://developer.android.com/reference/android/widget/Checkable.html) view in item layout and want to set it as checked, you have to handle this by yourself with OnItemClickListener.

    public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
        ViewGroup vp = (ViewGroup) view;

        final int count = vp.getChildCount();

        for(int i = 0; i < count; i++) {
            final View child = vp.getChildAt(i);
            if(child instanceof Checkable) {
                ((Checkable) child).setChecked(true);
            }
        }

        mCount.setText(String.format(getResources().getString(R.string.item_count), getListView().getCheckedItemCount()));
    }

#### References
> [sample code](https://github.com/shinja/ListViewItemSelection)

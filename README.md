# TagSelectorView
TagSelectorView

A tag selector with animation


![gif](https://github.com/Rock610/TagSelectorView/blob/master/gif/gif2.gif)


#useage

- gradle

in project build.gradle
```
allprojects {
    repositories {
        maven {
            url  "http://dl.bintray.com/rock610/maven"
        }
    }
}

```

in module build.gradle
```
dependencies {
    compile 'com.rock.android:tagselector:1.0'
}

```

- in xml
```
<com.rock.android.tagselector.views.TagSelectView
        android:id="@+id/tagSelectView"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
```

- in your activity
```
TagSelectView tagSelectView = (TagSelectView) findViewById(R.id.tagSelectView);

List<Tags<DataBean>> dataList = new ArrayList<>();

int count = 2;
List<DataBean> dataBeanList = new ArrayList<>();
for (int i = 0; i < count; i++) {
    dataBeanList.add(new MyDataBean("item A" + i));
}

dataList.add(new Tags<DataBean>().
                setDefaultTag(dataBeanList.get(0).name)
                .setTags(dataBeanList)
                .setChangeAfterClicked(true)
                .setSelectFirst(false);

```
data source must extend the DataBean
- to insert a data to any tab
```
ITagSelectorTabView tagSelectorView = tagSelectView.getTabView(0).getTagSelectorView();
tagSelectorView.getData().add(0, new MyDataBean("im new"));
tagSelectorView.refresh();
```

- get the selected tag
```
tagSelectView.setOnTagSelectedListener(new TagSelectView.OnTagSelectedListener() {
            @Override
            public void onTagSelected(int selectorListPosition, int tabPosition) {
                DataBean dataBean = dataList.get(tabPosition).tags.get(selectorListPosition);
                MyDataBean d = (MyDataBean) dataBean;
                //do something like request the network

            }
        });

```

- listening the tab
```
tagSelectView.setOnTagViewStatusChangedListener(new TagSelectView.OnTagViewStatusChangedListener() {
            @Override
            public void onOpened(ITagSelectorTabView openedView) {
              
            }

            @Override
            public void onClosed(ITagSelectorTabView closedView) {
              
            }
        });

```


---
layout: post
title: MaterialSearchView
comments: true
tags:
- Android
- Python
- Material
---

# Prologue
I was developing a little example to test some things when I came across to implementing a SearchView. After reading the documentation in the Material Design guidelines, I started searching for a third party library to easily implement it. I didn’t find anything useful, so I developed it myself.

# What is MaterialSearchView?
MaterialSearchView is a cute library to implement SearchView in a Material Design Approach.

![sample](https://raw.githubusercontent.com/MiguelCatalan/MaterialSearchView/master/art/voice.gif) ![sample](https://raw.githubusercontent.com/MiguelCatalan/MaterialSearchView/master/art/default.gif)

<a href=“https://play.google.com/store/apps/details?id=com.miguelcatalan.materialsearchview.sample”>
  <img alt=“Get it on Google Play”
       src=“https://developer.android.com/images/brand/en_generic_rgb_wo_60.png” />
</a>

# How do I use it?
**Add the dependencies to your gradle file:**

	dependencies {
    	compile ‘com.miguelcatalan:materialsearchview:1.0.0’
	}

**Add MaterialSearchView to your layout file along with the Toolbar** *(Add this block at the bottom of your layout, in order to display it over the rest of the view)*:

	<!— Must be last for right layering display —>
    <RelativeLayout
        android:id=“@+id/toolbar_container”
        android:layout_width=“match_parent”
        android:layout_height=“wrap_content”>

        <android.support.v7.widget.Toolbar
            android:id=“@+id/toolbar”
            android:layout_width=“match_parent”
            android:layout_height=“?attr/actionBarSize”
            android:background=“@color/theme_primary” />

        <com.miguelcatalan.materialsearchview.MaterialSearchView
            android:id=“@+id/search_view”
            android:layout_width=“match_parent”
            android:layout_height=“wrap_content” />
    </RelativeLayout>

**Add the search item into the menu file:**

	<item
        android:id=“@+id/action_search”
        android:icon=“@drawable/ic_action_action_search”
        android:orderInCategory=“100”
        android:title=“@string/abc_search_hint”
        app:showAsAction=“always” />

**Add define it in the *onCreateOptionsMenu*:**

		@Override
		public boolean onCreateOptionsMenu(Menu menu) {
        getMenuInflater().inflate(R.menu.menu_main, menu);

        MenuItem item = menu.findItem(R.id.action_search);
        searchView.setMenuItem(item);

        return true;
    }

**Set the listeners:**

	MaterialSearchView searchView = (MaterialSearchView) findViewById(R.id.search_view);
	searchView.setOnQueryTextListener(new MaterialSearchView.OnQueryTextListener() {
            @Override
            public boolean onQueryTextSubmit(String query) {
                //Do some magic
                return false;
            }

            @Override
            public boolean onQueryTextChange(String newText) {
                //Do some magic
                return false;
            }
        });

        searchView.setOnSearchViewListener(new MaterialSearchView.SearchViewListener() {
            @Override
            public void onSearchViewShown() {
                //Do some magic
            }

            @Override
            public void onSearchViewClosed() {
                //Do some magic
            }
        });

# Use VoiceSearch
**Allow/Disable it in the code:**

	searchView.setVoiceSearch(true); //or false

**Handle the response:**

	@Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        if (requestCode == MaterialSearchView.REQUEST_VOICE && resultCode == RESULT_OK) {
            ArrayList<String> matches = data.getStringArrayListExtra(RecognizerIntent.EXTRA_RESULTS);
            if (matches != null && matches.size() > 0) {
                String searchWrd = matches.get(0);
                if (!TextUtils.isEmpty(searchWrd)) {
                    searchView.setQuery(searchWrd, false);
                }
            }

            return;
        }
        super.onActivityResult(requestCode, resultCode, data);
    }

# Add suggestions
**Define them in the resources as a *string-array*:**

	<string-array name=“query_suggestions”>
        <item>Android</item>
        <item>iOS</item>
        <item>SCALA</item>
        <item>Ruby</item>
        <item>JavaScript</item>
    </string-array>
**Add them to the object:**	

	searchView.setSuggestions(getResources().getStringArray(R.array.query_suggestions));

# Style it!
	<style name=“MaterialSearchViewStyle”>
        <!— Background for the search bar—>
        <item name=“searchBackground”>@color/theme_primary</item>

        <!— Change voice icon—>
        <item name=“searchVoiceIcon”>@drawable/ic_action_voice_search_inverted</item>

        <!— Change clear text icon—>
        <item name=“searchCloseIcon”>@drawable/ic_action_navigation_close_inverted</item>

        <!— Change up icon—>
        <item name=“searchBackIcon”>@drawable/ic_action_navigation_arrow_back_inverted</item>

        <!— Change background for the suggestions list view—>
        <item name=“searchSuggestionBackground”>@android:color/white</item>

        <!— Change text color for edit text. This will also be the color of the cursor—>
        <item name=“android:textColor”>@color/theme_primary_text_inverted</item>

        <!— Change hint text color for edit text—>
        <item name=“android:textColorHint”>@color/theme_secondary_text_inverted</item>

        <!— Hint for edit text—>
        <item name=“android:hint”>@string/search_hint</item>
    </style>
    
# Bonus
**Close on backpressed:**

	@Override
    public void onBackPressed() {
        if (searchView.isSearchOpen()) {
            searchView.closeSearch();
        } else {
            super.onBackPressed();
        }
    }

# Help me
Pull requests are more than welcome, help me and others improve this awesome library.

The code is based in the Krishnakapil original concept.

# Download
**MaterialSearchView** is  hosted with GitHub. Head to the <a href=“https://github.com/MiguelCatalan/MaterialSearchView”>GitHub repository</a> for downloads, bug reports, and features requests.<span class=“blinking-cursor-post”>|</span>

# License
	Copyright 2015 Miguel Catalan Bañuls

	Licensed under the Apache License, Version 2.0 (the “License”);
	you may not use this file except in compliance with the License.
	You may obtain a copy of the License at

		http://www.apache.org/licenses/LICENSE-2.0

	Unless required by applicable law or agreed to in writing, software
	distributed under the License is distributed on an “AS IS” BASIS,
	WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
	See the License for the specific language governing permissions and
	limitations under the License.
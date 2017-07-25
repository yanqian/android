# Style and Theme

## What is style
It's like a CSS class, you want to define a style and use it in many elements to keep the same style. 
Change once and Apply Everywhere.
It's widely used in widget element.

### how to define a style
1.touch a new xml file in value directory
```
<style name="yan_style">
	<item android:layout_width>wrap_content</item>
	<item android:layout_height>wrap_content</item>
	/* attributes and so on */
</style>
```

Note:
`<style name="yan_style.child_style">` is a format of inherting from your customed style.
`<style name="child_style" parent="android:xxxstyle">` is a format of inherting from android system style.

2.use it in activity xml files
```
<TextView style="@style/yan_style"
android:id=""
android:layout_width=""
<!-- attributes and so on  -->
/>
```

## What is theme
Apply to activity and application, like android theme light or something.

### how to difine a theme

1.Touch a new xml file in value directory
```
<resource>
	<color name="yan_bg_color">#000000</color>
	<style name="yanTheme" parent="android:Theme.Light">
		<item name="android:windowsBackgroudColor">"@color/yan_bg_color"</item>
		/* attributes and so on */
	</style>
</resource>
```

2.In Manifest xml file
```
<application theme="@style/yanTheme"/>
<activity theme="@style/yanTheme"/>
```


# Fragment

## What is fragment

- A layout widget in andriod activity
- Reused like header and buttom frame in a webpage

## How fragment communicate

Fragments does not talk to each other. So activity is the media.

Fragment Top --> Activity --> Fragment Buttom 
and vice verse.

## Steps to create two fragments 

1. Create fragment Top layout xml file.
2. Create a java class to inflate from fragment Top layout xml file and return the view. The code is `inflater.inflate(R.id.fragment_a)` 
3. Do the same thing to create fragment Buttom layout file
4. In main acitivity layout file, add fragment Top and Buttom by Custome -> Fragment -> Drag Top and Buttom. 
5. In Fragment Top java class, 
```
	//find the button and add a button listener with a method onClicked(View v).

	//define an interface in fragment to be implemented in main activity.
	TopSectionListener activityCommand;
	public interface TopSectionListener{
		public void createMeme(String top, String buttom);
	}

	//the button listerer method onClick will be like
	onClick(View v){
		activityCommand.createMeme(firstInput.getText(), secondInput.getText());
	}
	// attach main activity to make sure activity will communicate with this frament
	public void onAttach(Activity activity){
		activityCommand = (TopSectionListener)activity;
	}
```
6. MainActivity implements TopSectionListener, so 
```
	public void createMeme(String top, String buttom){
		// get Fragment Button by activity method
		ButtonFragment buttomFrament = （ButtonFragment）getSupportFragmentManager().findFragmentById(R.id.buttom_fragment);
		buttomFrament.setMemeText(String top, String buttom)
	}
```
7. In buttom Fragment java file, define a method setMemeText to set text of 2 text views.
```
	public void setMemeText(String top, String buttom){
		buttomFrament.setMemeText(topTextView.getText(), buttomTextView.getText())
	}
```

## Conclusion

When the Fragment Top button is clicked, then it will pass the string to Main Activity which will do the actual action, so the Main Activity will find Fragment B and pass the string to Fragment B method to set the Text.
The above is the process of how fragments interacts.







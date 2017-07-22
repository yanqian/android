# Video and Camera

## How to play a video in Android

1. Add a VideoView in layout file

2. Add internet permission in manifest file

3. find the video view and start it in mainActivity file
```
VideoView drawvideo = (VideoView)findViewById(R.id.drawvideo);
drawvideo.setVideoPath("VIDEO_URL");

// MediaControl to set the video adjust horizonal or vertical.
MediaControl dVideoControler = new MediaControl(this);
dVideoControler.setAnchorView(drawvideo);
drawvideo.setMediaControl(dVideoControler);
```

## How to capture a camera in Android

1. Add user feature camera in manifest file
2. Check camera in MainActivity file
```
boolean hasCrame = getPackageManager().getSystemFeature(PackageManager.FEATURE_CAMERA_ANY);
```

3. Start Camera
```
public LaunchCamera(View view){
	private REQUEST_CODE = 1;
	Intent intent = new Inent(MediaStore.ACTION_IMAGE_CAPTURE);
	//If REQUEST_CODE >= 0, this code will be returned in onActivityResult() when the activity exits.
	startActivityForResult(i, REQUEST_CODE);
}
```

4. Capture the picture and show it
```
protected onActivityResult(int requestCode, int resultCode, Intent data){
	if(requestCode == REQUEST_CODE && resultCode == RESULT_OK){
		Bundle extra = data.getExtra();
		Bitmap photo = (Bitmap)extra.get("data");
		imageView.setImageBitmap(photo);
	}
}
```



# ListView

## What is ListView
Android widget.
Image what social stream feeds are. Those are made of ListView.

## How does it look like

      |  ListItem 0  |
      |  ListItem 1  |
      |  ListItem 2  | ---> ListView
      |  ListItem 3  |
      |  ListItem 4  |

## How to use ListView

1. make an adapter
Java code  --(Adapter)--> ListItem 
```
//Adapter converts String to ListItem:
String foods = ["a","b","b","b","b","b"];
ListAdapter adapter = new ListAdapter<String>(this, android.layout.simple_list_item_1, foods);
```
2. set Adapter to ListView `listView.setAdpater(adapter)`
3. add listener to ListItem

```
listView.setOnItemClickedListener(new AdapterView.OnItemClickedListener(){
    public void onItemClicked(AdapterView<?> parent, View view, int positon, long id){
        // android os will do the stuff to pass the ListView who is the parent of ListItem and position to the listener
        String value = String.valueOf(parent.getItemAtPostion(positon))
        Toast.make(value);
    }
});
```


## Make a customed Adapter

1. Create a row layout file so we can use it again and again like a for loop.
2. Super construct in Adapter Class
```
Class MyAdapter extends ArrayAdapter<String>{
  public MyAdpater(Context context, String[] foods){
      super(context, R.layout.customer_row, foods)
  }  
}
```
3. override getView
```
public View getView(int positon, View convertView, ViewGroup parent){
    // get inflater
    LayoutInflater inflater = LayoutInflater.from(getContext());
    View customerView = inflater.inflate(R.layout.customer_row, parent, false);
    // get Item value
    String food = getItem(positon)
    // set TextView text and ImageView image resource
    (TextView)customerView.findViewById(R.id.text).setText(food);
    (ImageView)customerView.findViewById(R.id.image).setImageResoure(R.id.image_pic);

    return customerView;
  }
```
4. Replace and new a Adapter in MainActivity

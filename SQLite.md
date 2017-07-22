# SQLite
## Model
Define a product model with getter and setter.

## DBHandler
A java class handles all the issues about database.

1. constructor
```
public class MyDBHandler extends DBHandler{
	public MyDBHandler(Context context, String name, SQLiteDatabase.CursorFactory factory, int version){
	super(context, "DB_NAME", factory, DB_VERSION);
	}
}

```
2. override methods
```
@Override
public onCreate(SQLiteDatabase db){
	sqlQuery = "Create A Table";
	db.execSQL(sqlQuery);
}
@Override
public onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion){
	db.execSQL("DROP A TABLE");
	onCreate(db);
}
```
3. add and delete and select in query
```
public void addProduct(Product product){
	//ContentValue transforms model attribute to db column
	ContentValue value = new ContextValue();
	value.put("columeName", product.getName());
	SQLiteDatabase db = getWritableDatabase();
	db.insert("table_name", null, value)
	db.close();
}
public void deteleProduct(String productName){
	db.execSQL("Delete from TABLE where productName");
}
public void databaseToString(){
	// define a string
	// use a cursor to loop over the rows selected 
	// return a string
	return "database all the rows in string"
}
```

## MainActivity

1. find Views of add and delete button and inputView and textView.

2. define their listener

3. use DBHandler to add, delete and show message in the view

4. it should work fine
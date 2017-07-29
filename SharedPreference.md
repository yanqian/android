# Shared Preference

If someone want to save some small piece of data to a app and do not want to use the database, then SharePreference is the easiest way to do it.

The android system creates an xml file in private app directory and put key value into it as a column, just like a YAML file.
The values can be updated, created and deleted and so on.

## Save to sharedpreference
```
SharedPreference sharePref = getSharedPreference("userInfo", Context.MODE_PRIVATE);
SharedPreference.Editor editor = sharePref.edit();
editor.putString("key", "value");
editor.apply();
```

## Read from sharedpreference
```
SharedPreference sharePref = getSharedPreference("userInfo", Context.MODE_PRIVATE);
String value = sharePref.getString("key", "defaultValue");
```

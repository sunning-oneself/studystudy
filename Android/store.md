# 持久化

## 文件存储

Context类中提供了一个openFileOutput()方法，可以用于讲数据存储到指定的文件中这个方法接收两个参数，第一个参数是文件名，在文件创建的时候使用的就是这个名称，注意指定的文件名不可以包含路径，因为所有的文件都是默认存储到/data/data/<packagename>/files/目录下，第二个参数是文件的操作模式，主要有两种模式可选，MODE_PRIVATE（默认，有同名文件时覆盖文件）和MODE_APPEND（有同名文件时追加）。

openFileOutput()方法返回的是FileOutputStream对象。

Context类中还提供了一个openFileInput()方法，用于从文件中读取数据，只接受一个参数，要读取的文件名，然后系统会自动到/data/data/<packagename>/files/目录下去去加载这个文件，并返回一个FileInputStream对象


```java
public class MainActivity extends AppCompatActivity {

    private EditText edit;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        edit = findViewById(R.id.edit);
        String inputText = load();
        if (!TextUtils.isEmpty(inputText)) {
            edit.setText(inputText);
            edit.setSelection(inputText.length());
            Toast.makeText(this, "Restoring succeeded", Toast.LENGTH_SHORT).show();
        }
    }

    public String load() {
        FileInputStream in;
        BufferedReader reader = null;
        StringBuilder content = new StringBuilder();
        try {
            in = openFileInput("data");
            reader = new BufferedReader(new InputStreamReader(in));
            String line;
            while ((line = reader.readLine()) != null) {
                content.append(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (reader != null) {
                try {
                    reader.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            return content.toString();
        }
    }


    @Override
    protected void onDestroy() {
        super.onDestroy();
        String inputText = edit.getText().toString();
        save(inputText);
    }
    public void save(String inputText) {
        FileOutputStream out;
        BufferedWriter writer = null;
        try {
            out = openFileOutput("data", Context.MODE_PRIVATE);
            writer = new BufferedWriter(new OutputStreamWriter(out));
            writer.write(inputText);
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if (writer != null) {
                    writer.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
`


## SharedPreferences存储

使用键值对的方式来存储数据

1. 将数据存储到SharePreferences中

要想使用SharePreferences来存储数据，首先需要获取到SharePreferences对象。Android中主要提供了3重方法：

- Context类中的getSharedPreferences()方法
- Activity类中的getPreferences()方法
- PreferenceManager类中的getDefaultSharePreferences()方法


# <p align="center">[Flutter] 1. ù��° �� ������, part 2</p>
  ![img](/img/flutter.jpg)
> flutter ���� ������ https://flutter.dev/docs/get-started/codelab ������     
> �������� �籸���Ͽ����ϴ�. 

## 1. �Ұ�
Flutter�� iOS �� Android���� ��ǰ���� �⺻ �������̽��� ������ ���ִ� Google ����� SDK�Դϴ�. Flutter�� ���� �ڵ�� �Բ� �۵��ϸ� �� ���� ������ �� �������� ���Ǹ� �����̸� ���� �ҽ��Դϴ�.

�� �ڵ� �������� ��ȭ �� ����� �����ϵ��� �⺻ Flutter ���� Ȯ���մϴ�. 
���� ����ڰ� Ž�� �� �� �ִ� �� ��° ������(called a _route_)�� ����ϴ�. ���������� �� �׸�(color)�� �����մϴ�.
�� �ڵ� ���� Part 1 , _Create a Lazily Loaded List_�� Ȯ�� ������ Part 2�� �����Ϸ��� ��� 
���� �ڵ带 �����մϴ�.

### Part 2���� ��� ����
* iOS�� Android ��ο��� �ڿ������� ���̴� Flutter ���� �ۼ��ϴ� ���
* �� ���� �����ֱ⸦ ���� �� ���ε� ���.
* ���� ���� ������ ��ȭ �� ����� �߰��ϴ� ���
* �� ��° ȭ���� ����� Ž���ϴ� ���
* �׸��� ����Ͽ� ���� ����� �����ϴ� ���


### Part 2���� ���� ����
���� ȸ�翡 ���� ���� �� �̸��� ������ ����� �����ϴ� ������ ����� ������ �����մϴ�.
�� �ڵ� ���� ������ ����ڴ� �̸��� �����ϰų� ���� �����Ͽ� �ֻ��� �̸��� ������ �� �ֽ��ϴ�. 
�� ���� ������ ��ܿ��ִ� ��� �������� ������ ��� ã�� �̸� �� ���� �ϴ� �� ������(_route_)�� 
�̵� �մϴ�.

�ִϸ��̼� GIF�� �ϼ� �� ���� �۵� ����� �����ݴϴ�.    
![img](/img/flutter06.gif)     
(The app from part2)

## 2. Flutter ȯ�� ����
Part 1�� �Ϸ����� ���� ��� Flutter ������ ���� ȯ���� �����Ϸ��� ù ��° Flutter �� �ۼ�(Part 1)���� 
Flutter ȯ�� ������ ���� �Ͻʽÿ�.

## 3. ���� �� �ޱ�
�� �ڵ� ���� Part 1���� �۾� �� ��� �̹� ���� �� startup_namer�� �ֽ��ϴ�. 
�׷��ٸ� ���� �ܰ�� ������ �� �ֽ��ϴ�.

����� startup_namer�� ���� ��� �Ʒ��� ���� �����Ͻø� �˴ϴ�.

* Part 1 ù ��° Flutter �� �����ϱ��� ��ħ�� ���� ������ ���ø� Flutter ���� ����ϴ�. 
myapp ��� ������Ʈ startup_namer�� �̸��� �����Ͻʽÿ�.

* lib/main.dart ���� ��� �ڵ带 Part 1�� �ڵ�� �����ϼ���.

* pubspec.yaml�Ʒ��� ���� ���� �ܾ� ��Ű���� �߰��Ͽ� ������Ʈ �Ͻʽÿ�.

``` dart
dependencies:
  flutter:
    sdk: flutter

  cupertino_icons: ^0.1.2
  english_words: ^3.1.0    // Add this line.
```

���� �ܾ� ��Ű���� �������� ���� �̸����� ���Ǵ� ������ �ܾ� ���� �����մϴ�.

* Android Studio�� �����⺸�⿡�� pubspec�� ���鼭 ������ ����� ��Ű�� ���� ���⸦ Ŭ���Ͻʽÿ�.
��Ű���� ������Ʈ�� �����ɴϴ�. �ֿܼ� ������ ǥ�õǾ���մϴ�.
``` dart
flutter packages get
Running "flutter packages get" in startup_namer...
Process finished with exit code 0
```
���� �����Ͻʽÿ�. ���� �� ���� �̸��� ���������� �����Ͽ� ���ϴ¸�ŭ ��ũ���Ͻʽÿ�.


## 4. ��Ͽ� ������ �߰�    

�� �ܰ迡���� �� �࿡ ��Ʈ �������� �߰��մϴ�. 
���� �ܰ迡���� �� �����ϰ� ��� ã�⸦ �����մϴ�.

* _savedRandomWordsState�� ��Ʈ�� �߰��Ͻʽÿ� . 
�� ��Ʈ�� ����ڰ� ��ȣ�ϴ� �ܾ� ���� �����մϴ�. 
�ùٸ��� ���� �� Set�� �ߺ� �׸��� ������� �����Ƿ� Set�� List���� ��ȣ�˴ϴ�.

``` dart
class RandomWordsState extends State<RandomWords> {
  final List<WordPair> _suggestions = <WordPair>[];
  final Set<WordPair> _saved = Set<WordPair>();   // Add this line.
  final TextStyle _biggerFont = TextStyle(fontSize: 18.0);
  ...
}
```

* �� _buildRow��ɿ��� alreadySaved�ܾ� ���� ��� ã�⿡ ���� �߰����� �ʾҴ��� Ȯ���Ͻʽÿ�.

``` dart
Widget _buildRow(WordPair pair) {
  final bool alreadySaved = _saved.contains(pair);  // Add this line.
  ...
}
```

���� _buildRow()������ ��� �������� ListTile ��ü�� �߰��Ͽ� ��ȣ���� ���� �� �ֽ��ϴ�.
���� �ܰ迡���� ���� �����ܰ� ��ȣ �ۿ��ϴ� ����� �߰��մϴ�.

* �Ʒ��� ���� �������� �߰��Ͻʽÿ�.

``` dart
Widget _buildRow(WordPair pair) {
  final bool alreadySaved = _saved.contains(pair);
  return ListTile(
    title: Text(
      pair.asPascalCase,
      style: _biggerFont,
    ),
    trailing: Icon(   // Add the lines from here... 
      alreadySaved ? Icons.favorite : Icons.favorite_border,
      color: alreadySaved ? Colors.red : null,
    ),                // ... to here.
  );
}
```

* ���� �� ���ε��Ͻʽÿ�. ���� �� �࿡ ���� ������ ǥ�õ����� ���� ��ȭ ���� �ƴմϴ�.    

![img](/img/flutter07.png)     
(Android & iOS)    


## 5. ��ȭ �� ��� �߰� (interactivity)
�� �ܰ迡���� heart �������� ���Ҽ� �ְ� �մϴ�. 
����ڰ� ��Ͽ��� �׸��� ������ "favorited"���·� ��ȯ�ǰ� �ش� �ܾ� ���� ����� 
��� ã�� ��Ʈ���� �߰��ǰų� ���ŵ˴ϴ�.

�̸� ���� _buildRow����� �����մϴ�. �ܾ� �׸��� �̹� ��� ã�⿡ �߰� �� ��� 
�ܾ� �׸��� �ٽ� ������ ��� ã�⿡�� ���ŵ˴ϴ�. 
Ÿ���� ���ϸ� �Լ� setState()�� ���°� ����Ǿ����� �����ӿ�ũ�� �˸��� ���� ȣ���մϴ�.

* onTap �Ʒ��� ���̸� �߰��Ͻʽÿ�.

``` dart
Widget _buildRow(WordPair pair) {
  final alreadySaved = _saved.contains(pair);
  return ListTile(
    title: Text(
      pair.asPascalCase,
      style: _biggerFont,
    ),
    trailing: Icon(
      alreadySaved ? Icons.favorite : Icons.favorite_border,
      color: alreadySaved ? Colors.red : null,
    ),
    onTap: () {      // Add 9 lines from here...
      setState(() {
        if (alreadySaved) {
          _saved.remove(pair);
        } else { 
          _saved.add(pair); 
        } 
      });
    },               // ... to here.
  );
}
```

``` bash
Tip: Flutter�� ���� ��Ÿ�� ������ ��ũ���� ȣ�� �ϸ� State ��ü setState()�� build () �޼��忡    
���� ȣ���� Ʈ���� �Ǿ� UI�� ������Ʈ�˴ϴ�.
```

���� �� ���ε��Ͻʽÿ�. �׸��� ��� ã�� �Ǵ� ��� ã��� Ÿ���� ���� �� �־���մϴ�. 
Ÿ���� �ε帮�� �� ����Ʈ���� ������ �Ϲ��� ��ũ ��� �ִϸ��̼��� �����˴ϴ�.    

![img](/img/flutter08.png)     
(Android & iOS)    


## 6. ���ο� ȭ������ �̵�
�� �ܰ迡���� ���ã�⸦ ǥ���ϴ� �� ������(Fluter �� ���)�� �߰��մϴ�. 
Ȩ ��ο� �� ��� ���̸� Ž���ϴ� ����� ���ϴ�.

Flutter���� Navigator�� ���� ��ΰ� ���� �� ������ �����մϴ�. 
��θ� �׺������ �������� Ǫ���ϸ� ���÷��̰� �ش� ��η� ������Ʈ�˴ϴ�. 
�׺�������� ���ÿ��� ��θ� ã�� ���� ���÷��̰� ���� ��η� ���ư��ϴ�.

�������� RandomWordsState�� ���� �޼ҵ忡�� AppBar�� ��� �������� �߰��մϴ�. 
����ڰ� ��� �������� Ŭ���ϸ� ����� ��� ã�Ⱑ ���� �� �� ��ΰ� �׺�����ͷ� 
Ǫ�õǾ� �������� ǥ�õ˴ϴ�.

* �����ܰ� �ش� ��ġ�� build�޼ҵ忡 �߰��Ͻʽÿ�.

``` dart
class RandomWordsState extends State<RandomWords> {
  ...
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Startup Name Generator'),
        actions: <Widget>[      // Add 3 lines from here...
          IconButton(icon: Icon(Icons.list), onPressed: _pushSaved),
        ],                      // ... to here.
      ),
      body: _buildSuggestions(),
    );
  }
  ...
}
```

``` bash
�� : �Ϻ� ���� Ư���� ���� ����(child)�� ���ϰ� ��ġ�� ���� �ٸ� Ư�� children�� ���ȣ ([])��     
ǥ�õȴ�� ���� �迭( )�� ���մϴ� .
```

* _pushSaved()RandomWordsState Ŭ������ �Լ��� �߰��Ͻʽÿ� .

``` dart
  void _pushSaved() {
  }
```

* ���� �� ���ε��Ͻʽÿ�. �� �����ܿ� ��� ������ ( )�� ��Ÿ���ϴ�. _pushSaved�Լ��� ��� �����Ƿ� �ƹ� �͵� ������ �ʽ��ϴ� .

�������� ��θ� ����� �׺�������� �������� Ǫ���մϴ�. �� ��ġ�� ȭ���� �����Ͽ� 
�� ��θ� ǥ���մϴ�. �� �������� ���� builder�� �͸� �Լ� �� MaterialPageRoute�� 
�Ӽ��� ����Ǿ� �ֽ��ϴ�.

* Navigator.push�Ʒ��� ������ ȣ�� �ϸ� ��ΰ� �׺�������� �������� Ǫ�õ˴ϴ�. 
IDE�� ��ȿ���� ���� �ڵ忡 ���� ���������� ���� ���ǿ��� �����մϴ�.

``` dart
void _pushSaved() {
  Navigator.of(context).push(
  );
}
```

�������� MaterialPageRoute�� �ش� ������ �߰��մϴ�. 
������ ListTile ���� �����ϴ� �ڵ带 �߰��Ͻʽÿ�. 
divideTiles()ListTile �� �޼ҵ�� �� ListTile ���̿� ���� ������ �߰��մϴ�. 
divided����, toList() ���� ��� ������� ��ȯ �� ���� ���� �����ϰ� �ֽ��ϴ�.

�Ʒ��� ���� �ڵ带 �߰��Ͻʽÿ�.

``` dart
void _pushSaved() {
  Navigator.of(context).push(
    MaterialPageRoute<void>(   // Add 20 lines from here...
      builder: (BuildContext context) {
        final Iterable<ListTile> tiles = _saved.map(
          (WordPair pair) {
            return ListTile(
              title: Text(
                pair.asPascalCase,
                style: _biggerFont,
              ),
            );
          },
        );
        final List<Widget> divided = ListTile
          .divideTiles(
            context: context,
            tiles: tiles,
          )
          .toList();
      },
    ),                       // ... to here.
  );
}
```

���� Ư���� "����� ����"�̶�� �� ����� �� ǥ�� ���� ���� �� ��ĳ ���带 �����մϴ�.
�� ����� ������ ListTiles ���� �����ϴ� ListView�� �����˴ϴ�. �� ���� �й��� ���е˴ϴ�.

* �Ʒ��� ���� ���� ���м��� �߰��Ͻʽÿ�.

``` dart
void _pushSaved() {
  Navigator.of(context).push(
    MaterialPageRoute<void>(
      builder: (BuildContext context) {
        final Iterable<ListTile> tiles = _saved.map(
          (WordPair pair) {
            return ListTile(
              title: Text(
                pair.asPascalCase,
                style: _biggerFont,
              ),
            );
          },
        );
        final List<Widget> divided = ListTile
          .divideTiles(
            context: context,
            tiles: tiles,
          )
              .toList();

        return Scaffold(         // Add 6 lines from here...
          appBar: AppBar(
            title: Text('Saved Suggestions'),
          ),
          body: ListView(children: divided),
        );                       // ... to here.
      },
    ),
  );
}
```

* ���� �� ���ε��Ͻʽÿ�. ������ �׸� �� �Ϻθ� ��� ã���ϰ� �� �ٿ��� ��� �������� �����ϴ�.
��� ã�Ⱑ ���� �� �� ��ΰ� ��Ÿ���ϴ�. �׺�����ʹ� "�ڷ�"��ư�� �� ǥ�� �ٿ� �߰��մϴ�.  
Navigator.pop�� ��� ������ ������ �ʿ�� �����ϴ�. Ȩ ��ư���� ���ư����� �ڷ� ��ư�� ���Ͻʽÿ�.    

![img](/img/flutter09.png)     
(Android & iOS)    


## 7. �׸��� ����Ͽ� UI ����

�� �ܰ迡���� �� �׸��� �����մϴ�. ������ ���� ���� ������ �����մϴ�. 
���� ��ġ �Ǵ� ���ķ����Ϳ� ���� �� �⺻ �׸��� ����ϰų� �귣���� �ݿ��ϵ��� 
�׸��� ����� ���� �� �� �ֽ��ϴ�.

ThemeData Ŭ���� �� �����Ͽ� �� �׸��� ���� ������ �� �ֽ��ϴ�.
�� ���� ���� �⺻ �׸��� ��������� ���� �⺻ ������ ������� �����մϴ�.

* MyApp Ŭ�������� ������ �����Ͻʽÿ�.

``` dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Startup Name Generator',
      theme: ThemeData(          // Add the 3 lines from here... 
        primaryColor: Colors.white,
      ),                         // ... to here.
      home: RandomWords(),
    );
  }
}
```
* ���� �� ���ε��Ͻʽÿ�. ���� ��ü ����� ������� �ٲ�� ������ �� �ٵ� �ֽ��ϴ�.

���ڸ����� �������� ThemeData�� ����Ͽ� UI�� �ٸ� ������ �����Ͻʽÿ�.
Material ���̺귯�� �� Colors Ŭ������ ����� ���ִ� ���� ���� ����� �����ϸ� 
�� ���ε�� UI�� ������ ���� ���� �� �� �ֽ��ϴ�.    


![img](/img/flutter10.png)     
(Android & iOS)    

## 8. Well done!
iOS�� Android���� ��� ����Ǵ� ��ȭ�� Flutter ���� �ۼ��߽��ϴ�. 
�� �ڵ� �������� ������ �����߽��ϴ�.

* ��Ʈ �ڵ� �ۼ�
* �� ���� �����ֱ⸦ ���� �� ���ε带 ����߽��ϴ�.
* �ۿ� ��ȭ �� ����� �߰��Ͽ� ���� ���� ������ �����߽��ϴ�.
* Ȩ ��ο� �� ��� ���̸� �̵��ϱ����� ��θ� ����� ���� �߰��߽��ϴ�.
* �׸��� ����Ͽ� �� UI�� ����� �����ϴ� ����� ���� ������ϴ�.

9. Next steps

Flutter SDK�� ���� �ڼ��� �˾ƺ��ʽÿ�.

* Flutter Ʃ�丮�� ���� ���̾ƿ� �ۼ� https://flutter.dev/docs/development/ui/layout
* ��ȭ �� �ڽ��� �߰� https://flutter.dev/docs/development/ui/interactive
* ���� �Ұ� https://flutter.dev/docs/development/ui/widgets-intro
* �ȵ���̵� �����ڸ����� Flutter https://flutter.dev/docs/get-started/flutter-for/android-devs
* React Native �����ڸ����� Flutter https://flutter.dev/docs/get-started/flutter-for/react-native-devs
* �� �����ڸ����� �÷��� https://flutter.dev/docs/get-started/flutter-for/web-devs
* Flutter�� ��Ʃ�� ä�� https://www.youtube.com/flutterdev

�ٸ� �ڷ�� :

* Flutter (���� Udacity �ڽ�)�� ����Ƽ�� ����� �� ���� https://www.udacity.com/course/build-native-mobile-apps-with-flutter--ud905
* �÷��� �丮 å https://flutter.dev/docs/cookbook/
* �ڹٿ��� ��Ʈ �ڵ� ������ https://codelabs.developers.google.com/codelabs/from-java-to-dart/#0
* ��Ʈ�� ��Ʈ ��Ʈ�� : �� ���� �� �˾ƺ��� https://flutter.dev/docs/resources/bootstrap-into-dart
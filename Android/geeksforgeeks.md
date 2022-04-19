1. [Introduction to Android Development](https://www.geeksforgeeks.org/introduction-to-android-development/)
2. [History of Android](https://www.geeksforgeeks.org/history-of-android/)
3. [WebView in Android](https://www.geeksforgeeks.org/how-to-use-webview-in-android/)
4. [Android Architecture Patterns](https://www.geeksforgeeks.org/android-architecture-patterns/)
5. [MVC (Model View Controller) Architecture Pattern in Android with Example](https://www.geeksforgeeks.org/mvc-model-view-controller-architecture-pattern-in-android-with-example/)
    > 使用 java 的观察者模式
6. [MVP (Model View Presenter) Architecture Pattern in Android with Example](https://www.geeksforgeeks.org/mvp-model-view-presenter-architecture-pattern-in-android-with-example/)
    > **Presenter**: Fetch the data from the model and applies the UI logic to decide what to display. It manages the state of the View and takes actions according to the user’s input notification from the View.  
    > 视图和模型通过 Presenter 通信,约定好接口后,通过类的组合,视图有一个 Presenter 属性, 在视图的构造函数中初始化 Presenter , Presenter 的初始化需要注入之前生成的 View 类实例(`this`),和一个模型实例(用于保存数组). 之后,把View上组件用户事件传递给 Presenter , Presenter 通过传入的视图实例和模型实例和约定的接口,来操作数据和UI
7. [MVVM (Model View ViewModel) Architecture Pattern in Android](https://www.geeksforgeeks.org/mvvm-model-view-viewmodel-architecture-pattern-in-android/)

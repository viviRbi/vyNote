# JavaFX

### Download link

JavaFX link: https://gluonhq.com/products/javafx/
SceneBuilder: https://gluonhq.com/products/scene-builder/
Note to me: duoc tai xuong tai thu muc IntelliJ o dia e Program

### Setup JavaFx with IntelliJ

- Create a new JavaFX project
- Select jdk version

- Import javaFx library by File -> Project Structure -> Library -> + button -> Java -> JavaFx location/lib (13 cannot found error fixed)

- Run -> Edit Configuration -> Main -> Modify optiopns v -> VM options : --module-path ${PATH_TO_FX} --add-modules javafx.fxml,javafx.controls,javafx.graphics
- File -> settings -> Path variables -> + button -> PATH_TO_FX: fx position/lib
(JavaFx runtime Component are missing fixed)

### Setup SceneBuilder

- Cut paste SceneBuilder to your favourite location (optional)
Origianl SceneBuilder location: C:\Users\vy\AppData\Local or C:\Program Files

- Click sample.fxml -> SceneBuilder -> click link and download things it everything it recommend -> done

- If moved, Click on the warning Configurate Scene Builde Path, choose SceneBuilder.exe file

### Write some code with SceneBuilder and JavaFx

- In sceneBuilder, grid -> fill out prefix height and width nase on ```primaryStage.setScene(new Scene(root, 700, 500));```

- controller -> add a button. Give it an id (fxId) and an action hook (On Action) (action name: printHello)
- In Controller class, instead of import java.awt.event.ActionEvent, import javafx.event.ActionEvent
```java
public void printHello(ActionEvent){
	System.out.println("Hello");
}
```
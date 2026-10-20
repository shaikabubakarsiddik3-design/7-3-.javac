
import javafx.application.Application;
import javafx.geometry.Insets;
import javafx.geometry.Pos;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.control.Label;
import javafx.scene.control.TextField;
import javafx.scene.layout.GridPane;
import javafx.scene.layout.VBox;
import javafx.stage.Stage;

public class TipCalculator extends Application {

    @Override
    public void start(Stage stage) {
        Label title = new Label("Tip Calculator");

        Label billLabel = new Label("Bill Amount:");
        TextField billField = new TextField();
        billField.setPromptText("Enter bill amount");

        Label tipLabel = new Label("Tip Percentage:");
        TextField tipField = new TextField();
        tipField.setPromptText("Enter tip percentage");

        Button calculateButton = new Button("Calculate Tip");
        Label tipResult = new Label("Tip Amount: ₹0.00");
        Label totalResult = new Label("Total Amount: ₹0.00");
        Label message = new Label();

        calculateButton.setOnAction(event -> {
            try {
                double bill = Double.parseDouble(billField.getText());
                double tipPercent = Double.parseDouble(tipField.getText());

                if (bill < 0 || tipPercent < 0) {
                    message.setText("Enter non-negative values.");
                    return;
                }

                double tip = bill * tipPercent / 100;
                double total = bill + tip;

                tipResult.setText(String.format("Tip Amount: ₹%.2f", tip));
                totalResult.setText(String.format("Total Amount: ₹%.2f", total));
                message.setText("");

            } catch (NumberFormatException e) {
                message.setText("Please enter valid numbers.");
            }
        });

        GridPane grid = new GridPane();
        grid.setHgap(10);
        grid.setVgap(12);
        grid.setAlignment(Pos.CENTER);
        grid.add(billLabel, 0, 0);
        grid.add(billField, 1, 0);
        grid.add(tipLabel, 0, 1);
        grid.add(tipField, 1, 1);
        grid.add(calculateButton, 1, 2);

        VBox root = new VBox(18, title, grid, tipResult, totalResult, message);
        root.setPadding(new Insets(20));
        root.setAlignment(Pos.CENTER);

        Scene scene = new Scene(root, 400, 320);

        stage.setTitle("Tip Calculator App");
        stage.setScene(scene);
        stage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
}

import javafx.application.Application;
import javafx.stage.Stage;
import javafx.scene.Scene;
import javafx.scene.layout.VBox;
import javafx.scene.layout.HBox;
import javafx.geometry.Pos;
import javafx.geometry.Insets;
import javafx.scene.control.Label;
import javafx.scene.control.Button;
import javafx.scene.control.ComboBox;

/*

   Joe's Automotive offers the following maintenances:
   Oil Change - $35.00
   Lube Job   - $25.00
   Radiator Flush - $50.00
   Transmission Flush - $120.00
   Inspection - $35.00
   Muffler Replacement - $200.00
   Tire Rotation - $20.00
   Other Repairs (parts and labor) - $60.00/hr
   
*/

public class JoesAutomotive extends Application
{

   // Launch the application
   public static void main(String[] args)
   {
      launch(args);
   }
   
   @Override 
   public void start(Stage primaryStage)
   {
      // ComboBox dropdown with the selections for routine maintenances
      ComboBox<String> joesComboBox = new ComboBox<>();
      joesComboBox.getItems().addAll("Oil Change", 
                                     "Lube Job", 
                                     "Radiator Flush", 
                                     "Transmission Flush", 
                                     "Inspection", 
                                     "Muffler Replacement", 
                                     "Tire Rotation",
                                     "Repair Only (Must select repair hours)");
                                     
 // Store the main service label and dropdown in a VBox, then put the VBox in an HBox                                    
 Label joesLabel = new Label("Select Service");
 VBox vbox = new VBox(10, joesLabel, joesComboBox);
 HBox hbox = new HBox(10, vbox);
 
 // Dropdown to select the amount of quoted hours for repair
 ComboBox<String> joesRepairComboBox = new ComboBox<>();
 joesRepairComboBox.getItems().addAll("Maintenance Only",
                                      "1 hour",
                                      "2 hours",
                                      "3 hours",
                                      "4 hours",
                                      "5 hours",
                                      "6 hours",
                                      "7 hours",
                                      "8 hours");
                                      
 // Repair hours label, label and ComboBox arranged in a VBox                                
 Label joesRepairLabel = new Label("Select Repair Hours");
 VBox repairVBox = new VBox(10, joesRepairLabel, joesRepairComboBox);
 
 // Put the repair VBox in an HBox
 HBox repairHBox = new HBox(10, repairVBox);
 
 // Label for the cost and HBox for the cost
 Label costLabel = new Label("Cost in USD:");
 Label costDisplayLabel = new Label("0.00");
 HBox costHBox = new HBox(10, costLabel, costDisplayLabel);
 costHBox.setAlignment(Pos.CENTER);
 
 // Button that would return the total cost of the maintenances needed
 Button calculateButton = new Button("Calculate Total Cost");
 
 // Lambda expression for the cost calculation
 calculateButton.setOnAction(event -> 
 {
   double serviceCharge = 0.00;
   double hourlyCharge = 0.00;
   double totalCharge = 0.00;
   
/* 
   Oil Change - $35.00
   Lube Job   - $25.00
   Radiator Flush - $50.00
   Transmission flush - $120.00
   Inspection - $35.00
   Muffler Replacement - $200.00
   Tire Rotation - $20.00
   Other Repairs (parts and labor) - $60.00/hr
   
*/

   // Calculation for the cost of a routine maintenance service
   if (joesComboBox.getValue() != null)
   {  
      // If the user wants a maintenance and a repair, they would choose the maintenance here then choose repair hours.
      String service = joesComboBox.getValue();
      if (service.equals("Oil Change"))
         serviceCharge = 35.00;
       else if (service.equals("Lube Job"))
        serviceCharge = 25.00;
       else if (service.equals("Radiator Flush"))
         serviceCharge = 50.00;
       else if (service.equals("Transmission Flush"))
         serviceCharge = 120.00;
       else if (service.equals("Inspection"))
         serviceCharge = 35.00;
       else if (service.equals("Muffler Replacement"))
         serviceCharge = 200.00;
       else if (service.equals("Tire Rotation"))
         serviceCharge = 20.00;
       else if (service.equals("Repair (Must select repair hours)"))  // Repair is calculated using repair hourus
         serviceCharge = 0.00;
       else if (service.equals(""))    // If user does not select a service
         serviceCharge = 0.00;         // Leave the cost as 0.00 if the user selects no services
      } 
   
   // Calculation for the cost of a repair depending on the quoted hours
   if (joesRepairComboBox.getValue() != null)
   {
      String hours = joesRepairComboBox.getValue();
      if (hours.equals("Maintenance Only"))
         hourlyCharge = 0.00;
      else if (hours.equals("1 hour"))
         hourlyCharge = 60.00;
      else if (hours.equals("2 hours"))
         hourlyCharge = 120.00;
      else if (hours.equals("3 hours"))
         hourlyCharge = 180.00;
      else if (hours.equals("4 hours"))
         hourlyCharge = 240.00;
      else if (hours.equals("5 hours"))
         hourlyCharge = 300.00;
      else if (hours.equals("6 hours"))
         hourlyCharge = 360.00;
      else if (hours.equals("7 hours"))
         hourlyCharge = 420.00;
      else if (hours.equals("8 hours"))
         hourlyCharge = 480.00;
      else if (hours.equals(""))       
         hourlyCharge = 0.00;       // Leave cost as 0.00 if the user selects no services
   }
   
   // Total cost if the customer wants a maintenance service and a repair
   totalCharge = (serviceCharge + hourlyCharge);      
   costDisplayLabel.setText(String.format("%,.2f", totalCharge));       // Return cost w/ two decimal places
   });

   // Create a VBox that holds the hbox for the service label and dropdown, the repair and cost HBoxs, and the calculate button
   VBox mainVBox = new VBox(10, hbox, repairHBox, costHBox, calculateButton);
   mainVBox.setAlignment(Pos.CENTER);
   mainVBox.setPadding(new Insets(10));
   
   // Create a scene with the primary VBox   
   Scene scene = new Scene(mainVBox);
   
   // Display the scene
   primaryStage.setScene(scene);
   primaryStage.show();
   
   }
   
}

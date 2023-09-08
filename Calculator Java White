import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.text.DecimalFormat;

public class CalculatorApp {
    private JFrame frame;
    private JPanel panel;
    private JTextField textField;
    private String currentInput = "";

    public CalculatorApp() {
        frame = new JFrame("Calculator");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(400, 400);
        frame.setLayout(new BorderLayout());

        textField = new JTextField();
        textField.setFont(new Font("Arial", Font.PLAIN, 24));
        textField.setHorizontalAlignment(JTextField.RIGHT);
        textField.setEditable(false);

        panel = new JPanel();
        panel.setLayout(new GridLayout(5, 4));

        // Create buttons for digits and operators
        String[] buttonLabels = {
            "7", "8", "9", "+",
            "4", "5", "6", "-",
            "1", "2", "3", "*",
            "0", "C", "=", "/"
        };

        for (String label : buttonLabels) {
            JButton button = new JButton(label);
            button.setFont(new Font("Arial", Font.PLAIN, 24));
            button.addActionListener(new ActionListener() {
                public void actionPerformed(ActionEvent e) {
                    String buttonText = button.getText();
                    handleButtonClick(buttonText);
                }
            });
            panel.add(button);
        }

        frame.add(textField, BorderLayout.NORTH);
        frame.add(panel);
        frame.setVisible(true);
    }

    private void handleButtonClick(String buttonText) {
        if (buttonText.equals("C")) {
            currentInput = "";
            textField.setText("");
        } else if (buttonText.equals("=")) {
            try {
                // Evaluate the expression and display the result
                double result = evaluateExpression(currentInput);
                DecimalFormat decimalFormat = new DecimalFormat("#.##########"); // Adjust the number of decimal places as needed
                String resultText = decimalFormat.format(result);
                textField.setText(resultText);
                currentInput = resultText;
            } catch (Exception ex) {
                textField.setText("Error");
                currentInput = "";
            }
        } else {
            if (buttonText.equals("+") || buttonText.equals("-") || buttonText.equals("*") || buttonText.equals("/")) {
                // If the button clicked is an operator, add a space before and after it
                currentInput += " " + buttonText + " ";
            } else {
                currentInput += buttonText;
            }
            textField.setText(currentInput);
        }
    }

    private double evaluateExpression(String expression) {
        String[] tokens = expression.split(" ");

        if (tokens.length != 3) {
            throw new IllegalArgumentException("Invalid expression");
        }

        double num1 = Double.parseDouble(tokens[0]);
        double num2 = Double.parseDouble(tokens[2]);
        char operator = tokens[1].charAt(0);

        switch (operator) {
            case '+':
                return num1 + num2;
            case '-':
                return num1 - num2;
            case '*':
                return num1 * num2;
            case '/':
                if (num2 != 0) {
                    return num1 / num2;
                } else {
                    throw new ArithmeticException("Division by zero");
                }
            default:
                throw new IllegalArgumentException("Invalid operator");
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            public void run() {
                new CalculatorApp();
            }
        });
    }
}

# Agusah-Justice-Kodzo 
index number 1728043373

A. Emolument Class
public class Emolument {
    private double basic_salary; // Encapsulated
    private double tax_relief;   // Encapsulated

    // Constructor
    public Emolument(double basic_salary, double tax_relief) {
        this.basic_salary = basic_salary;
        this.tax_relief = tax_relief;
    }

    // Method to get basic salary
    public double getBasicSalary() {
        return basic_salary;
    }

    // Method to get tax relief
    public double getTaxRelief() {
        return tax_relief;
    }
    // Method to compute SSNIT contribution (3.5% of Basic Salary)
    public double SSNIT() {
        return 0.035 * basic_salary;
    }

    // Method to compute Taxable Income
    public double taxableIncome() {
        return basic_salary - (tax_relief + SSNIT());
    }
}


B. MyEmolument Class
public class MyEmolument extends Emolument {
    
    // Non-argument constructor with default values
    public MyEmolument() {
        super(0, 0); // Default values for basic salary and tax relief
    }

    // Constructor with specified values
    public MyEmolument(double basic_salary, double tax_relief) {
        super(basic_salary, tax_relief);
    }

    // Method to compute Income Tax
    public double incomeTax() {
        double taxableIncome = taxableIncome();
        double tax = 0;

        if (taxableIncome <= 500) {
            tax = taxableIncome * 0.05; // 5% for the first 500
        } else if (taxableIncome <= 1000) {
            tax = (500 * 0.05) + ((taxableIncome - 500) * 0.125); // 12.5% for the next 500
        } else {
            tax = (500 * 0.05) + (500 * 0.125) + ((taxableIncome - 1000) * 0.175); // 17.5% for the rest
        }
        return tax;
    }

    // Method to compute Total Deduction
    public double totalDeduction() {
        return SSNIT() + incomeTax(); // Total Deduction calculation
    }

    // Method to compute Net Salary
    public double netSalary() {
        return getBasicSalary() - totalDeduction(); // Net Salary calculation
    }
}


C. Test Program
import javax.swing.JOptionPane;

public class TestProgram {
    
    public static void main(String[] args) {
        // Accept input from the user using input dialog
        String salaryInput = JOptionPane.showInputDialog("Enter Basic Salary:");
        String reliefInput = JOptionPane.showInputDialog("Enter Tax Relief:");

        double basicSalary = Double.parseDouble(salaryInput);
        double taxRelief = Double.parseDouble(reliefInput);

        // Create MyEmolument object named Staff_Salary
        MyEmolument staffSalary = new MyEmolument(basicSalary, taxRelief);

        // Display the required outputs
        String output = "Basic Salary: " + staffSalary.getBasicSalary() + "\n" +
                        "Tax Relief: " + staffSalary.getTaxRelief() + "\n" +
                        "SSNIT Contribution: " + staffSalary.SSNIT() + "\n" +
                        "Taxable Income: " + staffSalary.taxableIncome() + "\n" +
                        "Income Tax: " + staffSalary.incomeTax() + "\n" +
                        "Total Deduction: " + staffSalary.totalDeduction() + "\n" +
                        "Net Salary: " + staffSalary.netSalary();

        JOptionPane.showMessageDialog(null, output);
    }
}

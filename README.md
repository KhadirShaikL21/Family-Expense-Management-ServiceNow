# Family Expense Management in ServiceNow

# 📊 Family Expense Management in ServiceNow  

## 📌 Project Overview  
The **Family Expense Management System** is a ServiceNow-based project designed to help families track, categorize, and manage their expenses efficiently.  
This system leverages ServiceNow’s **tables, relationships, business rules, and automation features** to provide a centralized solution for monitoring daily expenses and calculating overall family expenditure.  

---

## 🎯 Objectives  
- Enable tracking of **daily expenses** by family members.  
- Automate the calculation of **total daily/overall family expenses**.  
- Provide a **consolidated record** of expenses with detailed comments.  
- Ensure scalability for different family sizes and use cases.  
- Empower users with clear financial insights to support informed decision-making.  

---

## 🛠 Tools & Technologies  
- **ServiceNow PDI (Personal Developer Instance)** – Core platform for implementation.  
- **Update Sets** – For managing and migrating changes.  
- **Tables & Relationships** – For storing structured expense data.  
- **Business Rules (GlideRecord Scripting)** – For automated calculations.  
- **Form Designer** – To design and configure user-friendly forms.  
- **Number Maintenance** – To generate auto-incremented expense numbers.  

📖 References:  
- [ServiceNow Documentation](https://docs.servicenow.com/)  
- [GitHub Repository (Project Source & Screenshots)](https://github.com/KhadirShaikL21/Family-Expense-Management-ServiceNow)  

---

## 📂 Project Structure  
```plaintext
Family-Expense-Management-ServiceNow/
│
├── progress/                # Daily progress logs
│   ├── day1.md
│   ├── day2.md
│   └── day3.md
│
├── docs/                    # Project documentation
│   └── Project_Report.docx
│
├── screenshots/             # Screenshots of implementation
│   ├── FamilyExpensesTable.png
│   ├── DailyExpensesTable.png
│   ├── BusinessRule.png
│   ├── Result1.png
│   ├── Result2.png
│   └── Testing.png
│
├── update_sets/             # Exported ServiceNow update sets
│
└── README.md                # Project overview (this file)


📌 Implementation Steps
1. Setting up ServiceNow Instance

Signed up for a Developer Instance at developer.servicenow.com
.

Requested and configured a PDI instance.

2. Creating Update Set

Created a new update set:

Name: Family Expenses

Set as current update set for tracking.

3. Creating Tables
Family Expenses Table

Columns: Number, Date, Amount, Expense Details.

Number field configured with Auto Numbering via Number Maintenance (Prefix: MFE).

Daily Expenses Table

Columns: Number, Date, Expense, Family Member Name, Comments.

Number field configured with Auto Numbering.

4. Relationships

Created a relationship between Family Expenses and Daily Expenses.

Added Daily Expenses as a Related List under Family Expenses.

5. Business Rule

Automated calculation of daily expenses into the Family Expenses table.

(function executeRule(current, previous /*null when async*/) {
    var FamilyExpenses = new GlideRecord('u_family_expenses');
    FamilyExpenses.addQuery('u_date', current.u_date);
    FamilyExpenses.query();
    if (FamilyExpenses.next()) {
        FamilyExpenses.u_amount += current.u_expense;
        FamilyExpenses.u_expense_details += 
            " -> " + current.u_comments + ": Rs." + current.u_expense + "/-";
        FamilyExpenses.update();
    } else {
        var NewFamilyExpenses = new GlideRecord('u_family_expenses');
        NewFamilyExpenses.u_date = current.u_date;
        NewFamilyExpenses.u_amount = current.u_expense;
        NewFamilyExpenses.u_expense_details += 
            " -> " + current.u_comments + ": Rs." + current.u_expense + "/-";
        NewFamilyExpenses.insert();
    }
})(current, previous);


6. Testing

Added multiple Daily Expense records for the same date.

Verified that the Family Expenses table auto-updated with total sum and comments.

Results showed correct aggregation of expenses.

📸 Screenshots

(All screenshots available in Screenshots Folder
)

Family Expenses Table

Daily Expenses Table

Business Rule Configuration

Testing Results

✅ Results & Benefits

Successfully created a centralized expense tracking system.

Automated consolidation of daily expenses into a family-wide report.

Provided clear, user-friendly forms for expense entry.

Improved transparency and accountability in financial tracking.

System is scalable for different family setups.

🔮 Future Enhancements

Add budget alerts when expenses cross a predefined limit.

Build dashboards and charts for visual financial insights.

Enable multi-currency support for global families.

Integrate with mobile app for real-time expense tracking.

📚 References

ServiceNow Developer Documentation

ServiceNow Product Documentation

GitHub Repository (Source Code & Screenshots)

👨‍💻 Developed by: Khadir Shaik

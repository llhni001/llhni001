import csv
from datetime import datetime


class FinancialManagement:
    def __init__(self, file_path):
        self.file_path = file_path
        self.data = []

    def read_data_from_file(self):
        with open(self.file_path, 'r') as f:
            reader = csv.reader(f)
            for row in reader:
                self.data.append([row[0], float(row[1]), row[2], datetime.strptime(row[3], '%Y-%m-%d')])

    def add_income(self, amount, description, date):
        self.data.append(['income', amount, description, date])
        self.save_data_to_file()

    def add_expense(self, amount, description, date):
        self.data.append(['expense', amount, description, date])
        self.save_data_to_file()

    def add_credit_card_payment(self, amount, description, date):
        self.data.append(['credit_card_payment', amount, description, date])
        self.save_data_to_file()

    def get_total_income(self):
        total_income = 0
        for row in self.data:
            if row[0] == 'income':
                total_income += row[1]
        return total_income

    def get_total_expense(self):
        total_expense = 0
        for row in self.data:
            if row[0] == 'expense':
                total_expense += row[1]
        return total_expense

    def get_credit_card_payments(self):
        credit_card_payments = 0
        for row in self.data:
            if row[0] == 'credit_card_payment':
                credit_card_payments +=[]
        return credit_card_payments

    def get_balance(self):
        return self.get_total_income() - self.get_total_expense()

    def get_monthly_income(self, year, month):
        monthly_income = 0
        for row in self.data:
            if row[0] == 'income' and row[3].year == year and row[3].month == month:
                monthly_income += row[1]
        return monthly_income

    def get_monthly_expense(self, year, month):
        monthly_expense = 0
        for row in self.data:
            if row[0] == 'expense' and row[3].year == year and row[3].month == month:
                monthly_expense += row[1]
        return monthly_exp

    def get_monthly_credit_card_payments(self, year, month):
        monthly_credit_card_payments = 0
        for row in self.data:
            if row[0] == 'credit_card_payment' and row[3].year == year and row[3].month == month:
                monthly_credit_card_payments += row[1]
        return monthly_credit_card_payments

    def get_monthly_difference(self, year, month):
        return self.get_monthly_income(year, month) - (self.get_monthly_expense(year, month) + self.get_monthly_credit_card_payments(year, month))

    def save_data_to_file(self):
        with open(self.file_path, 'w', newline='') as f:
            writer = csv.writer(f)
            for row in self.data:
                writer.writerow([row[0], row[1], row[2], row[3].strftime('%Y-%m-%d')])

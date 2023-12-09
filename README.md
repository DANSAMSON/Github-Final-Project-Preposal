# Insulin Project-Final-Project-Proposal
What idea(s) do you have for your final project?
Insulin bolus calculator, recipe maker, workout planner.

If you plan to collaborate with one or two classmates, what are their names?
Daniel Samsonov and Jayden Millwood.

Do you have any questions of your own?
How or when do we get approval for our ideas?


# %%
import matplotlib.pyplot as plt

def insulin_calculator():
    while True:
        blood_sugar = float(input("Enter blood sugar level in (mg/dL): "))
        if blood_sugar < 70:
            blood_sugar = float(input("Blood glucose too low, enter another reading or treat your hypoglycemia."))
        else:
            break
    target_sugar = float(input("Enter target blood sugar level in (mg/dL): "))
    carb_intake = float(input("Enter carbohydrates to be consumed in (grams): "))
    carb_ratio_option = input("Do you know your carb ratio (y/n)?")
    if carb_ratio_option.lower() == 'y':
        carb_ratio = float(input("Enter insulin-to-carb ratio in (grams per unit of insulin): "))
    else:
        insulin_dose = float(input("Enter insulin dose for the carb intake: "))
        carb_ratio = insulin_dose / carb_intake
    correction_factor = float(input("Enter correction factor in (mg/dL per unit of insulin): "))

    # Insulin dosage formula
    carb_dose = round(carb_intake / carb_ratio, 2)
    correction_dose = round((blood_sugar - target_sugar) / correction_factor, 2)

    total_dosage = round(carb_dose + correction_dose, 2)

    # Check blood sugar level
    if blood_sugar > 180:
        print("Blood sugar level is too high")
    elif blood_sugar < 70:
        print("Blood sugar level is too low")
    else:
        print("Blood sugar level is OK")

    # Print statements
    print("\nInsulin Dosage Calculation:")
    print(f"Carbohydrate Dose: {carb_dose} units")
    print(f"Correction Dose: {correction_dose} units")
    print(f"Total Insulin Dosage: {total_dosage} units")

    return blood_sugar, total_dosage

if __name__ == "__main__":
    blood_sugar_values = []
    total_dosage_values = []

    while True:
        blood_sugar, total_dosage = insulin_calculator()
        blood_sugar_values.append(blood_sugar)
        total_dosage_values.append(total_dosage)

        another_sample = input("Do you want to input another sample? (yes/no): ")
        if another_sample.lower() != "yes":
            break

    # Bar graph
    plt.figure(figsize=(10, 6))
    plt.bar(range(len(blood_sugar_values)), total_dosage_values, color='blue')
    plt.xlabel('Sample')
    plt.ylabel('Total Dosage (units)')
    plt.title('Total Insulin Dosage for Blood Sugar Levels')
    plt.xticks(range(len(blood_sugar_values)), [f'Sample {i+1}' for i in range(len(blood_sugar_values))])
    plt.show()

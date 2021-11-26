renterName = (input('What is the customer’s name?'))
classification_Code = (input(' The customer classification code (B for budget, D for Daily, and W for weekly)'))
days_Rented = int(input('The number of days the vehicle was rented '))
Start_Reading = int(input('The vehicles odometer reading at the start of the rental period '))  # start odometer reading
End_Reading = int(input('The vehicles odometer reading at the end of the rental period '))   # Final odometer reading

# To calculate the number of kilometers driven, we subtract the End Reading from the Start reading.

kmDriven = End_Reading-Start_Reading

# CBased on the three available class codes, the following calculations were made:

if classification_Code == 'B':
    baseCharge = 40.00 * days_Rented
    kmCharge = 0.25 * kmDriven
    totalCharge = baseCharge + kmCharge
elif classification_Code == 'D':
    avgKmPerDay = kmDriven / days_Rented     # Calculation of average kilometres driven per day during rental period
    baseCharge = 60.00 * days_Rented
    if avgKmPerDay <= 100:
        kmCharge = 0.00
    else:
        kmCharge = 0.25 * (kmDriven - 100)     # - 100 to ensure calculation of only kilometres above 100 limit
    totalCharge = baseCharge + kmCharge
elif classification_Code == 'W':
    if days_Rented <= 7:
        weeksRented = 1
    else:
        weeksRented = (days_Rented // 7) + 1
    avgDrivenPerWeek = kmDriven / weeksRented
    baseCharge = 190.00 * weeksRented
    if avgDrivenPerWeek <= 900:
        kmCharge = 0.00
        addCharge = 0.00     # Additional charges
    elif avgDrivenPerWeek > 900 and avgDrivenPerWeek <= 1500:
        kmCharge = 0.00
        addCharge = 100.00 * weeksRented
    else:
        kmCharge = (0.25 * (avgDrivenPerWeek - 1500)) * weeksRented
        # - 1500 to  calculation only kilometres above 1500 kilometres per week limit:

        addCharge = 200.00 * weeksRented
    totalCharge = baseCharge + kmCharge + addCharge

# Code for entering wrong class code:

else:
    print('Sorry, the code you provided does not exist.')

# Show output statements

if classification_Code == 'B' or classification_Code == 'D' or classification_Code == 'W':
    print('\nSummary:')
    print()
    print('Name of vehicle renter: ', renterName)
    print('Number of days vehicle rented:', days_Rented)
    print('Initial odometer reading on rented vehicle: ', Start_Reading)
    print('Final odometer reading on rented vehicle: ', End_Reading)
    print('Number of kilometres driven during rental period:', kmDriven)
    print('\n Final billing cost: ', totalCharge)


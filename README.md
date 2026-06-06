# CIS567-integrated-lab-3
This repository is for practicing the GitHub Flow. CIS567-integrated-lab-3
def read_customer_data(filename):
    """Read and return data from filename as a list of lists (name, state, debt)"""
    names = []
    states = []
    debts = []

    with open(filename) as f:
        rows = f.readlines()
    for row in rows:
        row = row.split(",")
        names.append(row[0])
        states.append(row[1])
        debts.append(float(row[2].strip()))
    return names, states, debts


# Main portion of the program
if __name__ == "__main__":
    # number of rows to consider
    num_customers = int(input())
    debt_limit = int(input())
    search_phrase = input()
    state_abbr = input()

    names, states, debts = read_customer_data("CustomerData.csv")

    # U.S. Report
    highest_debt = debts[0]
    highest_name = names[0]
    starts_with_count = 0
    over_limit = 0
    debt_free = 0

    for i in range(num_customers):
        if debts[i] > highest_debt:
            highest_debt = debts[i]
            highest_name = names[i]

        if names[i].startswith(search_phrase):
            starts_with_count += 1

        if debts[i] > debt_limit:
            over_limit += 1

        if debts[i] == 0:
            debt_free += 1

    print("U.S. Report")
    print(f"Customers: {num_customers}")
    print(f"Highest debt: {highest_name}")
    print(f'Customer names that start with "{search_phrase}": {starts_with_count}')
    print(f"Customers with debt over ${debt_limit}: {over_limit}")
    print(f"Customers debt free: {debt_free}")
    print()

    # State Report
    state_customers = 0
    state_highest_debt = -1
    state_highest_name = ""
    state_starts_with = 0
    state_over_limit = 0
    state_debt_free = 0

    for i in range(num_customers):
        if states[i] == state_abbr:
            state_customers += 1

            if debts[i] > state_highest_debt:
                state_highest_debt = debts[i]
                state_highest_name = names[i]

            if names[i].startswith(search_phrase):
                state_starts_with += 1

            if debts[i] > debt_limit:
                state_over_limit += 1

            if debts[i] == 0:
                state_debt_free += 1

    print(f"{state_abbr} Report")
    print(f"Customers: {state_customers}")
    print(f"Highest debt: {state_highest_name}")
    print(f'Customer names that start with "{search_phrase}": {state_starts_with}')
    print(f"Customers with debt over ${debt_limit}: {state_over_limit}")
    print(f"Customers debt free: {state_debt_free}")

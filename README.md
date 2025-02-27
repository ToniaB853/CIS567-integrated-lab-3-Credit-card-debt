# CIS567-integrated-lab-3-Credit-card-debt
26.22 LAB*: Program: Credit card debt

def read_customer_data(filename):
    """Read and return data from filename as a list of lists (name, state, debt)"""
    names = []
    states = []
    debts = []

    with open(filename) as f:
        rows = f.readlines()
    for row in rows:
        row = row.split(',')
        names.append(row[0])
        states.append(row[1])
        debts.append(float(row[2].strip()))
    return names, states, debts

# Main portion of the program
if __name__ == '__main__':
    # number of rows to consider
    num_customers = int(input())

    names, states, debts = read_customer_data("CustomerData.csv")

    # Type your code here.
    
debt_limit = int(input())
search_phrase = input().strip()
state_abbr = input().strip()

max_debt = max(debts[:num_customers])
max_debt_index = debts.index(max_debt)
highest_debt_name = names[max_debt_index]

print("U.S. Report")
print(f"Customers: {num_customers}")
print(f"Highest debt: {highest_debt_name}")

count_names_with_phrase = sum(name.startswith(search_phrase) for name in names[:num_customers])
print(f"Customer names that start with \"{search_phrase}\": {count_names_with_phrase}")

count_debt_over_limit = sum(debt > debt_limit for debt in debts[:num_customers])
count_debt_free = sum(debt == 0 for debt in debts[:num_customers])

print(f"Customers with debt over ${debt_limit}: {count_debt_over_limit}")
print(f"Customers debt free: {count_debt_free}")

state_customers = [i for i in range(num_customers) if states[i] == state_abbr]
state_names = [names[i] for i in state_customers]
state_debts = [debts[i] for i in state_customers]

if state_customers:
    state_max_debt = max(state_debts)
    state_max_debt_index = state_debts.index(state_max_debt)
    state_highest_debt_name = state_names[state_max_debt_index]

count_state_names_with_phrase = sum(name.startswith(search_phrase) for name in state_names)
count_state_debt_over_limit = sum(debt > debt_limit for debt in state_debts)
count_state_debt_free = sum(debt == 0 for debt in state_debts)

print(f"\n{state_abbr} Report")
print(f"Customers: {len(state_customers)}")
print(f"Highest debt: {state_highest_debt_name}")
print(f"Customer names that start with \"{search_phrase}\": {count_state_names_with_phrase}")
print(f"Customers with debt over ${debt_limit}: {count_state_debt_over_limit}")
print(f"Customers debt free: {count_state_debt_free}")
    


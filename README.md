# CID567-integrated-lab-3
Credit Card 26.22 
def find_highest_debt(names, debts):
    max_debt = max(debts)
    index = debts.index(max_debt)
    return names[index]

def count_names_with_prefix(names, prefix):
    count = sum(name.startswith(prefix) for name in names)
    return count

def analyze_debts(names, debts, debt_limit):
    over_limit_count = sum(debt > debt_limit for debt in debts)
    debt_free_count = sum(debt == 0 for debt in debts)
    return over_limit_count, debt_free_count

def process_and_report(names, states, debts, num_customers, debt_limit, search_phrase, state_abbr):
    print("\nU.S. Report")
    print(f"Customers: {num_customers}")

    highest_debt_name = find_highest_debt(names, debts)
    print(f"Highest debt: {highest_debt_name}")

    prefix_count = count_names_with_prefix(names, search_phrase)
    print(f"Customer names that start with \"{search_phrase}\": {prefix_count}")

    over_limit_count, debt_free_count = analyze_debts(names, debts, debt_limit)
    print(f"Customers with debt over ${debt_limit}: {over_limit_count}")
    print(f"Customers debt free: {debt_free_count}")

    if state_abbr:
        print(f"\n{state_abbr} Report")
        state_customers = [i for i, state in enumerate(states) if state == state_abbr]

        state_debts = [debts[i] for i in state_customers]
        state_highest_debt_name = find_highest_debt([names[i] for i in state_customers], state_debts)
        print(f"Customers: {len(state_customers)}")
        print(f"Highest debt: {state_highest_debt_name}")

        state_prefix_count = count_names_with_prefix([names[i] for i in state_customers], search_phrase)
        print(f"Customer names that start with \"{search_phrase}\": {state_prefix_count}")

        state_over_limit_count, state_debt_free_count = analyze_debts([names[i] for i in state_customers],
                                                                      state_debts, debt_limit)
        print(f"Customers with debt over ${debt_limit}: {state_over_limit_count}")
        print(f"Customers debt free: {state_debt_free_count}")

if __name__ == '__main__':
    num_customers = int(input())
    names, states, debts = read_customer_data("CustomerData.csv")

debt_limit = int(input())
search_phrase = input().strip()
state_abbr = input().strip()

process_and_report(names, states, debts, num_customers, debt_limit, search_phrase, state_abbr)
    

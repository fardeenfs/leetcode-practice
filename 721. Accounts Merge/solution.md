Here is my solution for the problem: [721. Accounts Merge](https://leetcode.com/problems/accounts-merge/)


## My Solution

```python
class Solution:
    def accountsMerge(self, accounts: List[List[str]]) -> List[List[str]]:
        emails = {} # {"232@gmail":1}
        merged_accounts = {} # {1: ["name", "232@gmail"]}

        for i, account in enumerate(accounts):
            account_emails = [account[0]]
            for email in account[1:]:
                if email not in emails.keys(): 
                    emails[email] = i # Email -> Account Index
                    account_emails.append(email) # Account -> Email

                elif email in emails.keys() and emails[email] != i:
                    # If email was seen previously with another account,
                    # we merge the accounts
                    prev_account = merged_accounts[emails[email]]
                    merged_accounts.pop(emails[email])

                    # For all the emails in the earlier account,
                    # we update the pointer to the new account
                    for email in prev_account[1:]:
                        emails[email] = i
                    # Add the other emails seen in the previous account 
                    # to this account
                    account_emails += prev_account[1:]
            # Insert the account number and emails to the dictionary
            merged_accounts[i] = account_emails
        
        result = []
        for key, value in merged_accounts.items():
            result.append([value[0]]+sorted(value[1:]))

        return result


```

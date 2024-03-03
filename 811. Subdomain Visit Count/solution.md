Here is my solution for the problem: [811. Subdomain Visit Count](https://leetcode.com/problems/subdomain-visit-count/)


## My Solution

```python
class Solution:
    def subdomainVisits(self, cpdomains: List[str]) -> List[str]:
        counts = {}
        for cpdomain in cpdomains:
            to_insert = []
            cpdomain = cpdomain.split()

            # Split each value by the whitespace to get the domain and count
            count = cpdomain[0]
            domain = cpdomain[1]

            # This full domain needs to be inserted into the dictionary
            to_insert.append(domain)

            # Divide the domain into parts separated by .
            split_domain = domain.split('.')

            # If there are three parts, we will add both the last part and the joined 2nd and 3rd part of the domain.
            # If two parts, we will only add the last part.
            if len(split_domain) == 3:
                to_insert += [split_domain[1] + '.' + split_domain[2], split_domain[2]]
            elif len(split_domain) == 2:
                to_insert.append(split_domain[-1])

            # Insert into the counts dictionary to keep a track of the sum of repetitive parts accross iterations.
            for insertion in to_insert:
                if insertion in counts.keys():
                    counts[insertion] += int(cpdomain[0])
                else:
                    counts[insertion] = int(cpdomain[0])

        result = []
        for key, value in counts.items():
            result.append(str(value) + ' ' + key)
        
        return result
```

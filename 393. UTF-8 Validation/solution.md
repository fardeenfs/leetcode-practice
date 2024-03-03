Here is my solution for the problem: [393. UTF-8 Validation](https://leetcode.com/problems/utf-8-validation/)


## My Solution

```python
class Solution:
    def validUtf8(self, data: List[int]) -> bool:
        for i in range(len(data)):
            data[i] = str("{0:08b}".format(data[i]))

        n = 0
        while n < len(data):
            num_bytes = 0
            index = 0
            last_char = data[n][index]

            # Counts the number of 1s in the byte (Considered as the first byte of the sequence). Consider this the parent byte.
            while last_char != '0':
                index += 1 
                last_char = data[n][index]
                num_bytes += 1
                if num_bytes > 4:
                    return False

            # There is no sequence that stats with 10xxxx so it is invalid. Valid sequences start with 0, 110, 1110, 11110
            if num_bytes == 1:
                return False

            index = 1
            n += 1
            # Check the next bytes in the sequence until the number of bytes is reached as indicated by the parent byte.
            while index < num_bytes:

                # If there are no more bytes to check, then the sequence is invalid. We haven't reached the number of bytes indicated by the parent byte but we have run out of bytes.
                if n >= len(data): 
                    return False

                # If the next byte does not start with 10, then the sequence is invalid.
                if data[n][:2] != '10':
                    return False
                n += 1
                index += 1

        return True
```


## Optimal Solution - Same time complexity but simpler code

```python
class Solution:
    def validUtf8(self, data: List[int]) -> bool:
        # Initialize a counter variable
        count = 0
        
        # Iterate through each integer in the input data list
        for num in data:
            # If the count is 0, check how many leading 1's there are in the current integer
            if count == 0:
                if (num >> 5) == 0b110:
                    count = 1
                elif (num >> 4) == 0b1110:
                    count = 2
                elif (num >> 3) == 0b11110:
                    count = 3
                elif (num >> 7) != 0:
                    return False
            # If the count is not 0, check if the current integer is a continuation byte
            else:
                if (num >> 6) != 0b10:
                    return False
                count -= 1
        
        # If the count is still not 0 after iterating through all the integers, it is invalid
        return count == 0

```


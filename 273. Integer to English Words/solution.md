Here is my solution for the problem: [273. Integer to English Words](https://leetcode.com/problems/integer-to-english-words/)


## My Solution

```python

class Solution:
    num_words = {
            1: 'One',
            2: 'Two',
            3: 'Three',
            4: 'Four',
            5: 'Five',
            6: 'Six',
            7: 'Seven',
            8: 'Eight',
            9: 'Nine',
            10: 'Ten',
            11: 'Eleven',
            12: 'Twelve',
            13: 'Thirteen',
            14: 'Fourteen',
            15: 'Fifteen',
            16: 'Sixteen',
            17: 'Seventeen',
            18: 'Eighteen',
            19: 'Nineteen',
            20: 'Twenty',
            30: 'Thirty',
            40: 'Forty',
            50: 'Fifty',
            60: 'Sixty',
            70: 'Seventy',
            80: 'Eighty',
            90: 'Ninety',
        }

    def two_digit_in_words(self, num):
        if num in self.num_words:
            return ' ' + self.num_words[num]
        response = ""
        tens = (num // 10) * 10
        ones = num % 10
        if tens > 0:
            response += ' ' + self.num_words[tens]
        if ones > 0:
            response += ' ' + self.num_words[ones]
        return response

    def three_digit_in_words(self, num):
        response = ""
        hundreds = num // 100
        num = num % 100
        if hundreds > 0:
            response += ' ' + self.num_words[hundreds] + ' Hundred'
        if num > 0:
             response += self.two_digit_in_words(num)
        return response

    def higherOrderMapper(self, base, basename):
        response = ""
        if len(str(base)) == 3:
            response += self.three_digit_in_words(base) + ' ' + basename
        elif len(str(base)) == 2:
            response += self.two_digit_in_words(base) + ' ' + basename
        elif base > 0:
            response += ' ' + self.num_words[base] + ' ' + basename
        return response

    def numberToWords(self, num: int) -> str:
        if num == 0:
            return "Zero"
        result = ""
        billions = num // 1000000000
        num = num % 1000000000
        
        result += self.higherOrderMapper(billions, 'Billion')

        millions = num // 1000000
        num = num % 1000000

        result += self.higherOrderMapper(millions, 'Million')

        thousands = num // 1000
        num = num % 1000

        result += self.higherOrderMapper(thousands, 'Thousand')

        result += self.three_digit_in_words(num)

        return result.strip()
       

```

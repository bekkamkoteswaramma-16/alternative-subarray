# alternative-subarray
class Solution:
    def maxAlternatingSum(self, nums: List[int]) -> int:
        NEG = -10**18
        plus = NEG # ends with +, p=1, no deletion
        minus = NEG # ends with -, p=0, no deletion
        dplus = NEG # ends with +, deletion used
        dminus = NEG # ends with -, deletion used
        ans = NEG

        for x in nums:
            # no deletion
            n_plus = x
            if minus!= NEG:
                n_plus = max(n_plus, minus + x)
            n_minus = plus - x if plus!= NEG else NEG

            # with deletion
            # dplus (next should be +): can come from minus + x (using del), dminus + x, or plus (delete current)
            best_dplus = x
            if minus!= NEG:
                best_dplus = max(best_dplus, minus + x) # entry: delete between
            if dminus!= NEG:
                best_dplus = max(best_dplus, dminus + x)
            if plus!= NEG:
                best_dplus = max(best_dplus, plus) # delete current x

            # dminus: from plus - x (entry), dplus - x, minus (delete current)
            best_dminus = NEG
            if plus!= NEG:
                best_dminus = max(best_dminus, plus - x)
            if dplus!= NEG:
                best_dminus = max(best_dminus, dplus - x)
            if minus!= NEG:
                best_dminus = max(best_dminus, minus)

            plus, minus, dplus, dminus = n_plus, n_minus, best_dplus, best_dminus
            ans = max(ans, plus, minus, dplus, dminus)

        return ans

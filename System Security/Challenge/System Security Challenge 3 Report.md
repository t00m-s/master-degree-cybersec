## Soncin Tommaso -  890558@stud.unive.it

# Introduction
In this third challenge we're asked to recover a plain-text PIN having the following data available to us:
- Encrypted PIN block: e0cbc26e7c292e25 
- Offset:                         5493 
- Decimalization table: 0123456789012345
*But how can we do that?*
# Decimalization Attack
The idea behind is simple:
- We first change all the occurrences of one digit at a time in the decimalization table by offsetting the value (e.g. we change all the 0 to 1). This step must be done for one digit at a time, we can't change for example all the 0 to 1 and all the 5 to 7.
- We check if something changed in the pin verification process API (e.g if the pin is now incorrect), if that happens (again, as an example if the pin is wrong) we know that the original digit in the decimalization table is present in the PIN.
	- We then need to find the position of that digit, it should be technically possible to find first all the digits and then attempt a brute-force attack with all the permutations... *boring.* A faster (**and smarter**) way is to modify the offset to "counterbalance" the decimalization table modifications. This is done by, for example, subtracting one to a digit and checking if the API now accepts our values.
	  If that happens we know both the digit (from the decimalization table) and the position (from the index of the offset).
		  - **But what if i can't find the index?**
		    It means that the digit appears is more than one position and we have to find which offset digits to modify.
# Exploit script
The following script reproduces the idea behind the decimalization attack, a few things have to be mentioned:
- The utility function could have been "prettified" with various castings from string to int and viceversa
- I originally thought (after being stuck for two days because the API returns "CORRECT" instead of "CORRECT!" .. *yup*) that i had to guess all the possible combination 1X and X1 where $X \in [1,9]$ but luckily the first combination was enough so i cleaned up the temporary script. 
```python
import subprocess


def utility(digit: str, is_sum: bool = False) -> str:
    """
    Utility function for sum and subtract operation.
    """
    if digit == "0":
        return "1" if is_sum else "9"
    if digit == "9":
        return "0" if is_sum else "8"
    return chr(ord(digit) + 1) if is_sum else chr(ord(digit) - 1)


def verify(encrypted_pin: str, offset: str, dec_tab: str) -> bool:
    """
    Runs the program and checks if the values trigger the pin correctness.
    """
    payload = f"sudo docker run --rm secunive/seclab:hsm {encrypted_pin} {offset} {dec_tab}".split()
    return subprocess.check_output(payload) == b"CORRECT\n"


def main() -> None:
    """
    Decimalization attack logic.
    """
    encrypted_pin: str = "e0cbc26e7c292e25"
    offset: str = "5493"
    dec_tab: str = "0123456789012345"
    pin = [-1, -1, -1, -1] # Placeholder for real pin.
    # Trying to "jiggle" both the decimalization table and offset
    # First we check if a change in the value triggers the wrong pin message
    # If that doesn't happen we know that digit can be freely changed and is
    # Not present on the original PIN.
    # Instead, if something happens (verify == false) we try to guess
    # The index of the digit that we changed in the decimalization table
    # by modifying the offset one by one (spoiler, or more...)
    # Once verify == true we know the original digit and position
    # We then iterate to find all the digits.
    for i in range(len(dec_tab)):
        new_dectab = dec_tab.replace(dec_tab[i], utility(dec_tab[i], True))
        if not verify(encrypted_pin, offset, new_dectab):
            print(f"{dec_tab[i]} in pin, position checked: {i}")
            for digit in range(len(offset)):
                new_offset = offset.replace(offset[digit], utility(offset[digit]))
                if verify(encrypted_pin, new_offset, new_dectab):
                    print(f"{dec_tab[i]} in PIN, PIN: position {digit}")
                    pin[digit] = int(dec_tab[i])
                    break

    # "Proper" proof for missing index 1 and 2
    # This was supposed to implement the "change multiple offset digits"
    # part but i guess i can't make it work rn.
    # tmp_offset = [5, 4, 9, 3]
    # dectab_tmp = "0223456789022345"
    # for i in range(1, len(tmp_offset) + 1):
    #     values = [
    #         (value - 1 if idx < i else value) for idx, value in enumerate(tmp_offset)
    #     ]
    #     print(values, i)
    #     offset_tmp = "".join(map(str, values))
    #     if verify(encrypted_pin, offset_tmp, dectab_tmp):
    #         pin[1 : i + 1] = [1] * i
    #         break

    # Original guess knowing that 1 appeared in the pin, without the
    # index known
    pin[1] = 1
    pin[2] = 1
    # Part 2, obtaining the original PN.
    offset_as_list = [5, 4, 9, 3]
    original_pin = []
    for x, y in zip(pin, offset_as_list):
        original_pin.append((x + y) % 10)
    print(original_pin)

if __name__ == "__main__":
    main()
```
Here's the original pin: `3508` 
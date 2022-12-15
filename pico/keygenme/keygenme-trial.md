# Keygenme  PICOCTF 2021
## AUTHOR: SYREAL

Keygenme is a Reverse Engineering challenge that asks us to find the program's licence key.

i order to do that we need to find the piece of code that validates the licence key which is:

```python
def check_key(key, username_trial):

    global key_full_template_trial

    if len(key) != len(key_full_template_trial):
        return False
    else:
        # Check static base key part --v
        i = 0
        for c in key_part_static1_trial:
            if key[i] != c:
                return False

            i += 1

        # TODO : test performance on toolbox container
        # Check dynamic part --v
        if key[i] != hashlib.sha256(username_trial).hexdigest()[4]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[5]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[3]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[6]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[2]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[7]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[1]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[8]:
            return False



        return True
```

at the top of the source code we can see that there are 3 variables that together construct a pico flag and the code is validating a part of it;
so the licence key is the flag we are looking for.
in order to get the whole flag we need to reverse the above code which is easy:

```python
import hashlib

value = b'GOUGH'
pico = "picoCTF{1n_7h3_|<3y_of_"



hashed_value = hashlib.sha256(value)

pico += hashed_value.hexdigest()[4]
pico += hashed_value.hexdigest()[5]
pico += hashed_value.hexdigest()[3]
pico += hashed_value.hexdigest()[6]
pico += hashed_value.hexdigest()[2]
pico += hashed_value.hexdigest()[7]
pico += hashed_value.hexdigest()[1]
pico += hashed_value.hexdigest()[8]
pico += '}'

print(pico)

```
The above code will print our flag.



from sympy import mod_inverse

def is_prime(num):
    if num > 1:
        for i in range(2, num):
            if (num % i) == 0:
                return False
        return True
    else:
        return False

def generate_rsa_keys(p, q):
    if not (is_prime(p) and is_prime(q)):
        return "Оба числа должны быть простыми."
    elif p == q:
        return "Числа p и q должны быть различными."

    n = p * q
    phi_n = (p - 1) * (q - 1)

    # Выберите e
    e = int(input("Введите e, взаимно простое с φ(n): "))
    
    # Вычислите d
    d = mod_inverse(e, phi_n)

    public_key = (e, n)
    private_key = (d, p, q, phi_n)

    return public_key, private_key

p = int(input("Введите простое число p: "))
q = int(input("Введите простое число q: "))

public_key, private_key = generate_rsa_keys(p, q)

print('Открытые ключи (e, n):', public_key)
print('Закрытые ключи (d, p, q, φ(n)):', private_key)


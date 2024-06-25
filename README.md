from sympy.ntheory import isprime

def check_prime(num):
    if num > 1:
        if isprime(num):
            return True
        else:
            print(f"Число {num} не является простым. Пожалуйста, введите простое число.")
            return False
    else:
        print("Число должно быть больше 1.")
        return False

def diffie_hellman():
    p = int(input("Введите общее простое число (p): "))
    if not check_prime(p):
        return

    g = int(input("Введите общее основание (g): "))
    if not check_prime(g):
        return

    a = int(input("Введите закрытый ключ Алисы (a): "))
    b = int(input("Введите закрытый ключ Боба (b): "))

    A = pow(g, a, p)
    B = pow(g, b, p)

    print(f"Открытый ключ Алисы (A): {A}")
    print(f"Открытый ключ Боба (B): {B}")

    secretA = pow(B, a, p)
    secretB = pow(A, b, p)

    print(f"Секретный ключ Алисы: {secretA}")
    print(f"Секретный ключ Боба: {secretB}")

    if secretA == secretB:
        print("Общий секретный ключ успешно вычислен.")
    else:
        print("Ошибка: секретные ключи не совпадают.")

if __name__ == "__main__":
    diffie_hellman()


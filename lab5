from math import factorial
from timeit import timeit
from decimal import Decimal, getcontext
import matplotlib.pyplot as plt

getcontext().prec = 120  # т��чность можно увеличить

rec_times = []
iter_times = []


def paf(n: int) -> Decimal:
    if n == 1:
        return Decimal(2)
    if n == 2:
        return Decimal(4)
    sign = Decimal(-1) if (n % 2) else Decimal(1)
    return sign * (paf(n - 1) - paf(n - 2) / Decimal(factorial(3 * n)))


def pav(n: int) -> Decimal:
    if n == 1:
        return Decimal(2)
    if n == 2:
        return Decimal(4)

    f_nm2 = Decimal(2)  # F(1)
    f_nm1 = Decimal(4)  # F(2)

    for k in range(3, n + 1):
        sign = Decimal(-1) if (k % 2) else Decimal(1)
        f_n = sign * (f_nm1 - f_nm2 / Decimal(factorial(3 * k)))
        f_nm2, f_nm1 = f_nm1, f_n

    return f_nm1


if __name__ == "__main__":
    n_big = 1000

    try:
        print(f"При вводе {n_big} для функции, вычисляемой рекурсивно:")
        print(paf(n_big))
    except Exception as e:
        print(f"Рекурсивная ошибка: {type(e).__name__}: {e}")

    print()

    try:
        print(f"При вводе {n_big} для функции, вычисляемой итеративно, получаем значение:")
        print(pav(n_big))
    except Exception as e:
        print(f"Итеративная ошибка: {type(e).__name__}: {e}")

    print()
    print("№ | Рекурсивно (сек) | Итеративно (сек)")

    x = list(range(1, 11))
    for i in x:
        t_rec = timeit(lambda: paf(i), number=2000)
        t_it = timeit(lambda: pav(i), number=2000)
        rec_times.append(t_rec)
        iter_times.append(t_it)
        print(f"{i} | {t_rec:.10f} | {t_it:.10f}")

    plt.figure(figsize=(9, 5))
    plt.plot(x, rec_times, marker="o", label="Рекурсивно")
    plt.plot(x, iter_times, marker="o", label="Итеративно")
    plt.xlabel("n")
    plt.ylabel("Время вычисления (сек)")
    plt.title("Вариант 28")
    plt.grid(True, alpha=0.3)
    plt.legend()
    plt.tight_layout()
    plt.show()

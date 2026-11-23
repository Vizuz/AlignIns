Оригинальный код: github.com/JiiahaoXU/AlignIns 
Эксперименты выполнялись на macOS с использованием MPS.
Для этого были внесены изменения в оригинальный код, которые не затронули логику самого алгоритма:
-В agent.py и utils.py параметр non_blocking=True заменён на non_blocking=False ( тк при первоначальном запуске были очень низкие loss и точность, а при вычислении TDA появлялись NaN)
Также:
-Добавлен аргумент --seed для управления случайными генераторами. По умолчанию используется seed=0.
-Для CIFAR-10 раньше --rounds принудительно устанавливалось 100, теперь можно указывать свое значение 
Эксперименты: 
Общие параметры: CIFAR-10, 150 раундов, 4 вредоносных клиента, доля отравленных данных 0.3.
python federated.py --device mps --rounds 150 --poison_frac 0.3 --num_corrupt 4 --aggr alignins --data cifar10 --attack badnet
python federated.py --device mps --rounds 150 --poison_frac 0.3 --num_corrupt 4 --aggr avg --data cifar10 --attack badnet

python federated.py --device mps --rounds 150 --poison_frac 0.3 --num_corrupt 4 --aggr alignins --data cifar10 --attack badnet --non_iid --beta 0.5
python federated.py --device mps --rounds 150 --poison_frac 0.3 --num_corrupt 4 --aggr avg --data cifar10 --attack badnet --non_iid --beta 0.5

python federated.py --device mps --rounds 150 --poison_frac 0.3 --num_corrupt 4 --aggr alignins --data cifar10 --attack DBA
python federated.py --device mps --rounds 150 --poison_frac 0.3 --num_corrupt 4 --aggr avg --data cifar10 --attack DBA

python federated.py --device mps --rounds 150 --poison_frac 0.3 --num_corrupt 4 --aggr alignins --data cifar10 --attack neurotoxin

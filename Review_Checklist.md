### 1. Review Checklist

| Category | Result | Defect |
| :--- | :--- | :--- |
| **1. Initialization** | **Issue** | Uninitialized variable `sum` in `averageAttack`. |
| **2. Pointers** | **Issue** | Null pointer dereference in `attackMonster`, use-after-free in `defeatMonster`, memory leak (`bonus` in `main`), incorrect `delete` instead of `delete[]` in `readBoss`. |
| **3. Arrays / Buffers** | **Issue** | Array bounds overflow in `spawnMonster` (called 6 times for array of size 5), buffer overflow vulnerability with `std::cin >> name`. |
| **4. Loops** | **Issue** | Off-by-one error `i <= monsterCount` in `totalMonsterHealth` leads to out-of-bounds access. |
| **5. Arithmetic** | **Issue** | Signed/unsigned mismatch in `attackMonster` causes incorrect arithmetic logic; potential division by zero in `averageAttack`. |
| **6. Control Flow** | **Issue** | Assignment operator `=` used instead of equality `==` in `findMonster`; missing default return path in `playerRank`. |
| **7. Function calls** | **Issue** | Returning a reference to a local variable `label` in `getMonsterLabel`. |
| **8. Classes** | **Issue** | Rule of Three violation (missing copy constructor/assignment operator) causes shallow copy and double-free in `main`; `defeatMonster` causes double-free upon `Game` destruction. |

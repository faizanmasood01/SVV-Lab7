### 2. Code Review Report

| Line(s) | Defect Type | Why it is a problem | Proposed Fix | Severity |
| :--- | :--- | :--- | :--- | :--- |
| **35-38** | Array Bounds | No bounds checking before inserting into `monsters` array. Line 104 adds a 6th monster to a size 5 array, corrupting memory. | Add `if (monsterCount >= MAX_MONSTERS) return;` | High |
| **42** | Logic Error | `if (monsters[i]->id = id)` assigns `id` to the monster's `id` and evaluates to true (if `id != 0`), always returning the first monster. | Change to `if (monsters[i]->id == id)` | High |
| **48-52** | Null Dereference | `findMonster` returns `nullptr` if ID is not found. `m->health` immediately dereferences it, causing a segmentation fault. | Add `if (m == nullptr) return -1;` before accessing `m->health`. | High |
| **50** | Type Conversion | `m->health - dmg` promotes the result to `unsigned int`. Unsigned values are never `< 0`, breaking the health check. | Use `int dmg = damage;` instead of `unsigned int dmg`. | Medium |
| **57** | Loop Bounds | `for (i = 0; i <= monsterCount; i++)` reads past the end of the initialized objects, causing undefined behavior. | Change condition to `i < monsterCount`. | High |
| **62-65** | Dangling Reference | `getMonsterLabel` returns a reference to a local `std::string`. The object is destroyed when the function exits. | Change return type to `std::string` (pass by value). | High |
| **67-68** | Uninitialized Var | `double sum;` is not initialized. Adding to it results in garbage values. | Initialize `double sum = 0.0;` | Medium |
| **70** | Division by Zero | If `monsterCount` is 0, `sum / monsterCount` causes a division by zero crash. | Add `if (monsterCount == 0) return 0;` | Medium |
| **74-75** | Use After Free | `defeatMonster` deletes `m`, then accesses `m->name` on the next line. | Print the name before calling `delete m;`. | High |
| **74** | Memory / Classes | `defeatMonster` deletes the pointer but leaves it in the array. The `~Game()` destructor will delete it again (double-free). | Nullify the array index or shift remaining elements, decrement `monsterCount`. | High |
| **84-88** | Control Flow | `playerRank` lacks a return statement if `score <= 100`, resulting in undefined behavior. | Add `return 3;` or similar at the end of the function. | Medium |
| **93** | Buffer Overflow | `std::cin >> name;` reads unbounded input into a 10-char array. | Use `std::string name` or `std::setw(10)`. | High |
| **96** | Memory / Pointers | `delete name;` used on an array allocated with `new char[10]`. | Use `delete[] name;` (or avoid by using `std::string`). | Medium |
| **107** | Memory Leak | `Monster* bonus = new Monster(...)` is allocated but never deleted. | Add `delete bonus;` at the end of `main`. | Low |
| **118** | Classes (Rule of 3) | `Game copy = game;` uses compiler-generated shallow copy. Both `game` and `copy` destructors will `delete` the same pointers. | Implement a custom copy constructor (deep copy) or disable copying. | High |

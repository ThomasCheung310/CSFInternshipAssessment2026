# Architectural Proposal

## Problem
Animal count in each paddock is maintained manually in several different places such as in POST /animals, PUT /animals/:id, and DELETE /animals/:id etc. This data is multi-step and it can cause error as shown with one of the bug fixes where the decrement of the animal count is incorrect. The data is also redundant since the animal count in each paddock can just be calculated with another method. 

## How to fix
The animal_count column should be removed from the paddocks table schema in the db.js, and all the manual UPDATE paddocks SET animal_count statements should be deleted from animals.js. The animal count in each paddock can be calculated by counting the number of animals that has a certain paddock id:

```sql
SELECT p.*, COUNT(a.id) as animal_count
FROM paddocks p
LEFT JOIN animals a ON a.paddock_id = p.id
GROUP BY p.id
```

This method calculates the animal_count accurately from the live data without having to manually keep track of a separate parameter. The frontend would stay the exact same as the response shape stays unchanged.

## Why leave it for later
This fix is out of the scope of the assessment as the most important parts are fixing the critical bugs and adding the weight logging feature. This fix would also touch on multiple different files which would require more testings and its own focused PR.
This proposal is detailed enough so that other engineers can complete it without asking extra questions.
# Retrospective

## Trade-offs
1. I initially decremented old paddock count first before checking if the new paddock was full. If the new paddock was full, the old paddock count could be permanently wrong. I caught this error early and fixed it. The capacity check is now done first which eliminates the chance of an error happening to the old paddock count.

2. I fixed the immediate bugs regarding to the animal_count instead of removing the underlying issue of having a redundant separate variable. 

3. I fetched the full paddock list on every page refresh to build a name look-up map for the paddock names. A better solution would be to JOIN the paddock name in the API response on the server side. However, that would change the API contract.

## What I would do differently
1. I would add a weight graph in the frontend to visualize trends that might be beneficial for some sickness diagnosis.

2. I would add better error messages when API calls fail since it is hard to debug currently.

3. I would completely remove the redundant animal_count column in the paddocks and replace it with calculation shown in ARCH_PROPOSAL.md

## Deliberately left alone
1. I left the N+1 query in the GET /animals since it is more of a performance issue rather than an immediate break to the application.

2. I left the frontend error handling alone because fixing it consistently across all forms would require restructuring app.js which was out of scope
#Code Audit for FarmTracker App

##Problems Found
1. In PUT/:id in animals.js, the animal count of the old paddock does not decrease after updating the animal count of the new paddock.

2. Before updating the animal count of the new paddock, the capacity is not checked. Which means animal count can increase even if the capacity is reached.

3. When creating paddocks, there is no capacity validation beforehand. The capacity can be a negative number and a paddock can still be created.

4. The pagination that shows the animals is wrong. With a page limit of 5, the second page should start with animal tag 6 instead of animal tag 2.

5. In the POST/ in animals.js, the event returns 200 (default) instead of 201. 201 is the standard convention for creation in the REST API.

6. The paddock name for each animal is shown as ID instead of the paddock name in the frontend.

##Priority:
Issue 1 would be fixed first since it could affect the other functionalities such as the capacity check and error in the displayed count.

Issue 2 and 3 would be fixed second since the capacity of the paddock is related to the physical limitation of the paddock. With a faulty capacity check, more animals than the actual capacity would be accepted which the physical paddock could not handle.

##Leave for later
Issue 4,5, and 6 can be fixed later since those are just display problems which don't corrupt the data or disrupt core functionalities. Those issues can be addressed later after the critical fixes.

A performance issue that a N+1 query pattern in GET/ in animals.js. The pattern fetches the latest health event separately for each animal. This is not data corrupting and can be addressed after the other bug fixes.
```json
{
 "Statuses": [
   { "name": "Status: Abandoned", "color": "#000000" },
   { "name": "Status: Accepted", "color": "#009800" },
   { "name": "Status: Blocked", "color": "#e11d21" },
   { "name": "Status: Completed", "color": "#006b75" },
   { "name": "Status: In Progress", "color": "#cccccc" },
   { "name": "Status: On Hold", "color": "#e11d21" },
   { "name": "Status: Pending", "color": "#fef2c0" },
   { "name": "Status: Review Needed", "color": "#fbca04" }
 ],



 "Priorities":[
   { "name": "Priority: Low", "color": "#009800" },
   { "name": "Priority: Medium", "color": "#ff9900" },
   { "name": "Priority: High", "color": "#eb6420" },
   { "name": "Priority: Critical", "color": "#e11d21" }
 ],

 "Types":[
   { "name": "Type: Bug", "color": "#e11d21" },
   { "name": "Type: Maintenance", "color": "#fbca04" }, // Refactoring, optimization...
   { "name": "Type: Enhancement", "color": "#84b6eb" }, // Iterations on existing features or infrastructure. Generally these update speed, or improve the quality of results. Adding a new “Owner” field to an existing “Calendar” model in the API, for example.
   { "name": "Type: Feature", "color": "#9ecbfc" }, // Brand new functionality. New pages, workflows, endpoints, etc.
   { "name": "Type: Question", "color": "#cc317c" } // Requires further conversation to figure out the action steps. Most feature ideas start here.
 ],

 "Subjects":[
   { "name": "Subject: Security", "color": "#e11d21" },
   { "name": "Subject: Optimization", "color": "#84b6eb" },
   { "name": "Subject: Documentation", "color": "#fbca04" },
   { "name": "Subject: User Experience", "color": "#ec008c" } // Affect user's comprehension, or overall enjoyment of the product. These can be both opportunities and `UX bugs`.

 ],

 "Severity":[
   { "name": "Severity: CRITICAL/OSL1", "color": "#e11d21"}, // Total loss of service, inappropriate or invalid content regarding Veepee image or performance.
   { "name": "Severity: HIGH/OSL2", "color": "#ff9900"}, // Partial loss of service, inappropriate or invalid content regarding Veepee's partners (brands) image or performance.
   { "name": "Severity: MEDIUM/OSL3", "color": "#fbca04"}, // Inappropriate or invalid content regarding Veepee's providers image or performance. 
   { "name": "Severity: INVALID/OSL4", "color": "#84b6eb"} // Applications that bring comfort to workers, clients, partners, etc.

 ]
}
```

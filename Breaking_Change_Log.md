<a name="2016-10-19"></a>
#Release Date: 2016-10-19

###Change Summary
Team based security is being introduced into the DezrezCore to provide branch managers with greater controls around data security.

###What are the changes?
Every Team owned data contract returned from the DezrezCore API will now contain the below additional information outlining some security details: 

* **long** Id { get; set; }
* **long** OwningTeamId { get; set; }
* **long** BranchId { get; set; }
* **string** Name { get; set; }
* **string** TeamAccessType { get; set; } - [FullAccess,Restricted]

When a member of a team requests data to which is does not have access, the above 5 properties will be all that is returned inside the resulting Data Contract. This information can be used to identify the Owning Team for occassions where access to the required data need to be requested.

###Will you be affected?
All developers will see the additional properties included in the returned data contracts, however the ability to control access at a team level is a feature that will be enabled for each Agency by request. Only when an Agency who is a client of yours enables this feature will the above data contract restrictions be enforced.




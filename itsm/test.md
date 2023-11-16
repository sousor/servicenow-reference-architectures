```mermaid
C4Context
title Incident Management System - Context Diagram

Person(User, "User", "A user reporting or affected by an incident")
Person(Incident Manager, "User", "An employee who is responsible for the overall health and performance of a service")
Person(Support Group, "User", "An employee who is responsible for investigating and resolving incidents")


System_Boundary(SN, "ServiceNow Platform") {

Container(IM, "Incident Management", "Manages and resolves reported incidents")

Container_Boundary(IM1, "Incident Management") {
Component(IMM, "Incident Process Flow")
Container_Boundary(IPF, "Incident Process Flow"){
Component(IForm, "Incident Form","Form layout")
Component(ClientScr, "Client Script","Allows the system to run JavaScript on the client")
Component(UI, "UI Policy","Dynamically change the behavior of information on a form")
Component(BR, "Business Rules","Server-side logic that executes when database records are queried/updated/inserted or deleted")
Component(SI, "Script Include","Reusable server-side script logic")
Component(GR, "GlideRecord","JavaScript API")


Rel(IMM, IForm, "Contains", "Uses")
Rel(IForm, ClientScr, "Triggers")
Rel(IForm, UI, "Consumes")
Rel(IForm, BR, "Triggers")
Rel(IForm, UI, "Triggers")
Rel(SI, BR, "Uses")
Rel(BR, SI, "Uses")
Rel(SI, GR, "Consumes")
Rel(BR, GR, "Consumes")

 


}
}
}
System(CMDB, "Configuration Management Database", "Stores configuration and incident related data")
System(ES, "External Systems", "External systems and APIs interacting with Incident Management")

Rel(User, IM, "Reports incidents", "Uses")
Rel(Incident Manager, IM, "Reports incidents", "Uses")
Rel(Support Group, IM, "Reports incidents", "Uses")
Rel(IM, CMDB, "Queries and updates incident data")
Rel(IM, ES, "Integrates with")
Rel(BR,CMDB,"Reads/Updates")
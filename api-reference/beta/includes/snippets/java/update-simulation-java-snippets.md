---
description: "Automatically generated file. DO NOT MODIFY"
---

```java

GraphServiceClient graphClient = GraphServiceClient.builder().authenticationProvider( authProvider ).buildClient();

Simulation simulation = new Simulation();
simulation.id = "2f5548d1-0dd8-4cc8-9de0-e0d6ec7ea3dc";
simulation.displayName = "Graph Simulation";
simulation.description = "Test simulation created using postman";
simulation.payloadDeliveryPlatform = PayloadDeliveryPlatform.EMAIL;
simulation.additionalDataManager().put("payload@odata.bind", new JsonPrimitive("https://graph.microsoft.com/beta/security/attacksimulation/payloads/12345678-9abc-def0-123456789a"));
simulation.durationInDays = 7;
simulation.attackTechnique = SimulationAttackTechnique.CREDENTIAL_HARVESTING;
simulation.attackType = SimulationAttackType.SOCIAL;
simulation.status = SimulationStatus.SCHEDULED;
simulation.completionDateTime = OffsetDateTimeSerializer.deserialize("2022-09-16T06:13:08.4297612Z");
simulation.launchDateTime = OffsetDateTimeSerializer.deserialize("2022-09-05T06:13:08.4297612Z");
AddressBookAccountTargetContent includedAccountTarget = new AddressBookAccountTargetContent();
includedAccountTarget.type = AccountTargetContentType.ADDRESS_BOOK;
LinkedList<String> accountTargetEmailsList = new LinkedList<String>();
accountTargetEmailsList.add("faiza@contoso.com");
includedAccountTarget.accountTargetEmails = accountTargetEmailsList;
simulation.includedAccountTarget = includedAccountTarget;
AddressBookAccountTargetContent excludedAccountTarget = new AddressBookAccountTargetContent();
excludedAccountTarget.type = AccountTargetContentType.ADDRESS_BOOK;
LinkedList<String> accountTargetEmailsList1 = new LinkedList<String>();
accountTargetEmailsList1.add("sam@contoso.com");
excludedAccountTarget.accountTargetEmails = accountTargetEmailsList1;
simulation.excludedAccountTarget = excludedAccountTarget;

graphClient.security().attackSimulation().simulations("2f5548d1-0dd8-4cc8-9de0-e0d6ec7ea3dc")
	.buildRequest()
	.patch(simulation);

```
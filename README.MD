Modules::
Authorization-Microservice :
This module is used for doing the Authentication and Authorization part of our project. This microsevice provides the endpoints for authentication and authorization

--Endpoints :
Method	Endpoint Path	Returns
POST	/authenticate	ResponseEntity
POST	/authorize	boolean
POST	/authorize-role	boolean
--Dependencies on Other microsevices : None
--Application Properties Toggle :
spring.application.name=Authorizatiion-Microservice
server.port=8400
server.servlet.context-path=/auth
User Database : H2(In-Memory)

InsuranceClaim-Microservice :
This module is used for doing the Insurance Claim part after the registration of a patient. This microsevice provides the endpoints for getting the Insurance related details and storing insurer details.

--Endpoints :
Method	Endpoint Path	Returns
GET	/getAllInsurerDetail	List of "InsurerDetail"
GET	/getInsurerByPackageName/{packageName}	"InsurerDetail"
POST	/initiateClaim	double
--Dependencies on Other microsevices : Authorization-Microservice, IPTreatment-MicroService
--Application Properties Toggle :
spring.application.name=InsuranceClaim
server.port=8300
server.servlet.context-path=/insure
auth.URL=http://localhost:8400/auth
iptreatment.URL=http://localhost:8200/ipTreatment
User Database : H2(In-Memory)

IPTreatmentOffering-Microservice :
This module is used for doing the IPTreatmentOffering services. This microsevice provides the endpoints for viewing and modifying the treatment packages and the specialists.

--Endpoints :
Method	Endpoint Path	Returns
GET	/ipTreatmentPackages	List of "IPTreatmentPackage"
GET	/ipTreatmentPackageByName/{ailment}/{packageName}	List of "IPTreatmentPackage"
GET	/specialists	List of "SpecialistDetail"
POST	/addSpecialist	ResponseEntity of String type
DELETE	/deleteSpecialist/{specialistId}	ResponseEntity of String
PUT	/updatePackage/{pid}/{treatmentPackageName}	ResponseEntity of String
GET	/countPid/{pid}	boolean
--Dependencies on Other microsevices : Authorization-Microservice
--Application Properties Toggle :
spring.application.name=IPTreatmentOffering-service
server.port=8100
server.servlet.context-path=/ipTreatmentOffering
User Database : H2(In-Memory)

IPTreatment-Microservice :
This module is used for doing the Treatment Plan details of our project. This microsevice provides the endpoints for formulating timetable , getting treatment plans & updating the status.

--Endpoints :
Method	Endpoint Path	Returns
POST	/formulateTimetable	TreatmentPlan
GET	/getAllTreatmentPlan	List of "TreatmentPlan"
POST	/updateTreatmentPlan	TreatmentPlan
GET	/health-check	ResponseEntity
--Dependencies on Other microsevices : Authorization-Microservice, IPTreatmentOffering-Microservice
--Application Properties Toggle :
spring.application.name=IPTreatment-service
server.port=8200
server.servlet.context-path=/ipTreatment
User Database : H2(In-Memory)

Portal-Microservice :
This module is used for simulating the project through the User Interface. This microsevice provides the endpoints for Login. This is the UI-Microservice for our Project.

--Endpoints :
Method	Endpoint Path	Returns
GET	/login	View
--Dependencies on Other microsevices : Authorization-Microservice, IPTreatmentOffering-Microservice, IPTreatment-MicroService, InsuranceClaim-Microservice
--Application Properties Toggle :
auth.URL=http://localhost:8400/auth
ipoffering.URL=http://localhost:8100/ipTreatmentOffering
iptreatment.URL=http://localhost:8200/ipTreatment
insure.URL=http://localhost:8300/insure

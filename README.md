![Arma Server Monitor](picture/ASMCapture.PNG)

#Arma Server Monitor#

"Arma Server Monitor" is a spin-off of my "arma engine performance research".

Propertys:

	- monitors up to 4 server (or headless client) instances simultaneous 
	- introduces a performance value CPS for FSM processing analysis
	- very simple, compact and solid design
	- almost no influence to cpu load
	- easy to use, just bind one FSM in your mission and launch it from init.sqf file	

Currently able to monitor the following values:

	- FPS (on a server this means simulation frames per second)
	- CPS (Condition-evaluation Per Second)
	- PL# (Number of alive player units)
	- AI# (Number of alive local AI units)
	- PID (process ID of the server instance)
	- Name of the currently played mission (missionName)

**Arma Server Monitor** consists of 3 components:

	ASM.fsm 				- Collects and reports some internal performance states from arma server (or HC)
	ASMdll.dll 				- Interfaces to ArmaServerMonitor.exe via MMF (Memory Mapped File)
	ArmaServerMonitor.exe 	- The Monitor itself reads from MMF and displays the values


Alongside to the well known FPS (frames per second), an very interesting new value **CPS** is introdused here.    
**CPS** is expressed by **condition** **evalations** per **second** and measured from an reference condition in `ASM.fsm`.   

You can realize this **CPS** value as something like the current "response time" of AI in the running mission.    
Especially COOP missions running with low **CPS** are really no pleasure. AI seems to be "stupid".   

Two examples to illustrate this value:   
Lets say we have an CPS value of 10.0, then our AI has an average response delay of ca. 100ms here (1000ms/10.0).
That means everything runs well here.         
In a second scenario we have a CPS value of 0.3, what means AI response time is larger the 3 seconds !!!    
(If the second scenario occurs together with normal FPS values, I'd recommend to have a talk with the mission developer,    
because this behavior is very likely caused by excessively use of execVM, spawn etc.)    


**How to use ASM:**

Copy `ASMdll.dll` to your arma directory (where arma3server.exe resists)   
Copy `ASM.FSM` to your extracted mission folder and add a start line to `init.sqf` (see example)
Pack your mission to a `.pbo` again and copy it in your `MPMission` folder.

Run `ArmaServerMonitor.exe` to monitor all your server (or HC) instances with prepared missions.


*ENJOY :)*
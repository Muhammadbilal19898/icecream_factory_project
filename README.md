# INTRODUCTION

Our project simulates the working of an ice cream factory that gets multiple orders from customers demanding multiple ice cream cones. The process of creating/making an ice cream is complex and can be carried out at different speed depending upon the number of machines of various types. The procedure of making an ice cream cone is:

1.Boiling the milk.
2.Adding sugar.
3.Adding flavor.
4.Putting it into the cone.
5.Freezing.
6.Wrapping the cone.

Each of the above instruction takes time depending upon the complexity of the instruction. For example, the boiling of milk and freezing take more time than adding sugar etc.
	There are also different numbers of machines for each action. In our simulation, there are 3 boilers and freezers and the count of other machines is 2.
		 In the simulation, only one of the waiting customers can be entertained as there is only one counter. But multiple ice creams can be made of the same customers at a time. Once customer’s order is processed the customer can leave and one of the other waiting customers can check in to the counter.
	**Our project integrates a built-in system call into the kernel that simulates this behavior.**


# IMPLEMENTATION
	The project is implemented as a system call into the kernel (Linux). It can be executed just as we usually call any other built in command by its ID.The underlying principles of the project are semaphores and thread creation. There is a main system call function that initializes the semaphores to their respective values and prints the details of the orders.																								After that individual threads for each of the customers are created.Each of the customer thread that waits for the waiting line semaphore and requests for the entering the counter through ‘orderCounter’ semaphore. As this semaphore is a binary semaphore so only one customer thread can enter at a time. A single customer thread enters the counter and all the other customer threads wait for its completion. 
	The order of the customer on the counter is received and the manufacturing process is started. Threads for each of the ice cream that is requested by the customer are created. Each ice cream threads waits for the semaphores of machines in a pre-defined order. If all the machines are occupied, then the ice cream thread(s) wait till the machines are free.
	Once all the ice cream threads have completed their manufacturing process, the customer can leave the counter. Other waiting customers can request for the counter once this customer leaves. One of the other waiting customers is given entry to the counter. 
The program finishes once the orders of all the customers have been processed.

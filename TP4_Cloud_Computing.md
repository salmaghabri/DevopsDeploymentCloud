Work done by: Sandra Mourali, Mohamed Aziz Bellaaj, Louay Badri & Salma Ghabri
---

# Task 1: Azure traffic manager profile
## 1
a. b.
![](Capture%20d'écran%202024-12-02%20134143.png)
c. ![](Capture%20d'écran%202024-12-02%20160821.png)d. 
![](Capture%20d'écran%202024-12-02%20161209.png)
e.
![](TP4_Cloud_Computing-2.png)
![](TP4_Cloud_Computing-1.png)

## 2. 

- **Primary Traffic Manager**:
    - **Routing Method:** Performance.
    - Directs users to the closest region:
        - UK South (via a nested Traffic Manager).
        - North Europe (direct external endpoint).
- **UK South Traffic Manager**:
    - **Routing Method:** Priority.
    - Ensures high availability by routing:
        - Primarily to **UK South VM1**.
        - Fails over to **UK South VM2** if the primary is unavailable.
This setup achieves **geo-proximity-based routing** for users and ensures **redundancy** within UK South.

![](TP4_Cloud_Computing-3.png)

# Task 2: Azure front door

1. 
![](TP4_Cloud_Computing-6.png)
![](TP4_Cloud_Computing-7.png)

![](TP4_Cloud_Computing-8.png)

# Task 3: Azure Firewall
1. ![](TP4_Cloud_Computing-10.png)

2. ![](TP4_Cloud_Computing-11.png)
3. ![](TP4_Cloud_Computing-12.png)
4. ![](TP4_Cloud_Computing-13.png)
5. ![](TP4_Cloud_Computing-14.png)

6. ![](TP4_Cloud_Computing-15.png)
7. ![](TP4_Cloud_Computing-17.png)
	![](TP4_Cloud_Computing-16.png)
8. ![](TP4_Cloud_Computing-18.png)
9. 10 
	![](TP4_Cloud_Computing-20.png)
	 ![](TP4_Cloud_Computing-21.png)

#### 11
![](TP4_Cloud_Computing-22.png)
![](TP4_Cloud_Computing-23.png)
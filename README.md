<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)



<h2>Deployment and Configuration Steps</h2>

DC-1 has to have a static Private IP Address, Client one will connect to DC-1 and we should also try to ping DC-1. We have to enable ICMPv4 on the firewall on DC-1 in order for the ping to work now, since it previously was not working.

![image](https://github.com/MatthewTulloch/configure-ad/assets/165750459/9443cda2-afd2-400c-a577-7cdf53021820)

![image](https://github.com/MatthewTulloch/configure-ad/assets/165750459/be578eac-9b2c-4e44-bcc6-758186405de4)


Now we install Active Directory Users and Computers, Promote the VM to DC, setup a forest as "mydomain.com" afterwards restart then log back into DC-1 as user: "mydomain.com\labuser". It should look like this. 

![image](https://github.com/MatthewTulloch/configure-ad/assets/165750459/644bf6f6-92b2-4a5b-85ac-a6e7ea04c357)

I made _EMPLOYEES and _ADMINS too to place some of the users

![image](https://github.com/MatthewTulloch/configure-ad/assets/165750459/d8558c15-2313-4adf-8c4e-29780ef4a307)

I made Jane Doe, and made her a domain admin + user in order for this account to do various things on the computer. From now on we are using Jane_admin as the main account. 




Now we will join Client-1 to the domain (mydomain.com) using the azure portal. We change client-1's DNS settings to the DC's Private IP address. Then we restart the VM from within the portal. 

![image](https://github.com/MatthewTulloch/configure-ad/assets/165750459/6381d6ce-2301-4562-9575-145683f6243a)

Now we must join Client-1 to the domain. Go to system settings and go to about, then off to the right select rename this PC (advanced). From there select to "change the domain". Enter "mydomain.com", then enter your credentials from mydomain.com\labuser. The PC will restart automatically, and then client-1 will be a part of mydomain.com 

![image](https://github.com/MatthewTulloch/configure-ad/assets/165750459/35e555b8-ee7a-4454-a050-957f5ca98526)

 Client-1 is now apart of the domain. We will set up remote desktop for normal users on Client-1. Log into Client-1 as an admin and open system properties. Navigate to "Remote Desktop", allow "domain users" access to remote desktop. Now standard users can just login now.

 ![image](https://github.com/MatthewTulloch/configure-ad/assets/165750459/c75d6948-372a-4a96-a784-1c37807abfd0)

 In order to make sure this actually works, we will create users and then login into Client-1 with one of them. We use code that generates many users to do this

![image](https://github.com/MatthewTulloch/configure-ad/assets/165750459/bd78e3b1-bdc7-43ea-b925-b65a259603e1)

![image](https://github.com/MatthewTulloch/configure-ad/assets/165750459/1ece4c86-0d49-471b-a1a6-6b508117cb13)

![image](https://github.com/MatthewTulloch/configure-ad/assets/165750459/e31f2fd9-c632-40e8-a39e-57215adc29cf)

I used the user fav.jaxe and it worked as shown above!




</p>
<br />

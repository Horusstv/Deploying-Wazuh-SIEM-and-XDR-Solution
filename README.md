# Deploying-Wazuh-SIEM-and-XDR-Solution

## Part 1 Installation

Wazuh is a (SIEM) solution that provides monitoring, detection, and alerting of security events and incidents. 

In this exercise we are going to install Wazuh in the cloud on a Google Cloud Machine running Ubuntu 20.04, afer that we are going to install two agents, one in a local computer running Windows 11, and another one in an Azure Cloud Machine running Windows Enterprise, both are going to report to our server already installed in the Google Cloud machine so we can see the data reported and understand how a SIEM like Wazuh works.

**Note: Installation and configuration of the Machines in the cloud will NOT be covered in this exercise.**

To start we are going to go to [wazuh.com](https://wazuh.com/)

Click on "Install Wazuh" at the top right.

There are some minimum requirements that should be met in order to install Wazuh, do not try to install it without the minimum requirements since the installation can encounter errors and/or not install at all.

![minimum](https://imgur.com/8uWJEeZ.png)

Installation is pretty straight forward, just follow the instructions on the webpage starting in "Download and run the Wazuh installation assistant".

Connect to your machine via SSH
Install Wazuh in the Google Cloud Machine: curl -sO https://packages.wazuh.com/4.11/wazuh-install.sh && sudo bash ./wazuh-install.sh -a

![install](https://imgur.com/QZ0oCsn.png)

Installation will take a while so get yourself a coffe or do something else after typing the command above, just let the machine work and monitor the installation while you do something else.

After the installation is complete you should receive a message with your Wazuh credentials, (admin and password) copy and paste those credentials in a notepad.

![installfinish](https://imgur.com/PaapEIV.png)

## Part 2 Log in

You can also see in the iamge above that there is a message on how to connect to the Wazuh Dashboard: "You can access the web interface https//< wazuh-dashboard-ip >:443

This means you will have to replace the < wazuh-dashboard-ip > with the IP address of your own machine, in my case it is 34.170.189.234 on port 443 so mine will look like this: https//34.170.189.234:443

![login](https://imgur.com/1HMUJa7.png)

You will get some messages about certificates "not trusted", you can ignore the warnings and just accept everything and log in.

After you type in your username and password (the one you saved in a notepad before) you will see some quick check ups that Wazuh will do.

![checks](https://imgur.com/4Wbi0d6.png)

And then here we are, finally at the Wazuh dashboard.

![dash](https://imgur.com/EU1l6mi.png)

## Part 3 Deploying Agents

Now we need to deploy some agents so the Wazuh server can get some information to work with and the dashboard can show you data.

Click on "Deploy Agent"

![deploy](https://imgur.com/6NpOkPM.png)

Select the platform of the machine where you want to deplo the agent.

![deploy2](https://imgur.com/Cqqpt7h.png)

Follow the steps in the configuration, assign a name to the agent and configure the IP address to where the agent is going to connect (this is the IP address of the main server that you just installed before) in my case it was 34.170.189.234 after that you will get a script.

![deply3](https://imgur.com/2NW67uO.png)

You will need to copy and paste this script and run it via Linux terminal or Power Shell depending on what O.S is installed in the machine where you want to deploy the agent, keep in mind you will need amininstrator priviledges to run this commands or they won't work.

![script](https://imgur.com/E7WibQQ.png)

![powershell](https://imgur.com/xPtxZjV.png)

Do not forget to also run any other command after the script, it is different depending if you are running it on windows or linux.

## Part 4 Investigating Alers

Now give it a couple of minutes and soon the agents will start to report online in the Dashboard.
If you installed Wazuh in the cloud you may need to do additional firewall configuration for the server to start getting data.
![agentonline](https://imgur.com/7L7DmtV.png)

If you click on the agents you can see more information about them such as O.S, the node and the IP address.

![agentinfo](https://imgur.com/ROXcAdw.png)

The Dashboard will start to get information about the agents the longer they are running, you can then start investigating alerts, if your machines are exposed to the internet you will probably start to get information about strange activity such as login attemps with non existing users among others.

![failure](https://imgur.com/CVydUEz.png)

If you click on the detailed view in any of those alerts you can see even more information of the attackers such as country of origin, IP, etc.

![moreinfo](https://imgur.com/pMbUvyO.png)

Yet again it depends if your machine is exposed to the internet you may be able to get a lot of attacks and alerts that you can investigate using the software.

![failure2](https://imgur.com/SQOEkys.png)

## Conclusion

As you can see Wazuh is an amazing software that can help you manage and investigate threats to your network, by running this lab I was able to get practice in a SIEM enviroment getting real data of machines being attacked in real time.

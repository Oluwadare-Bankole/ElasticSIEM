#Elastic SIEM configuration

<h2>Description</h2>
This is a Lab environment where we configured an Elastic SIEM and pushed telemetry traffic and security events from a Kali linux Virtual Machine which serves as an elastic agent. We gp through the process of configuring a SIEM, a visualization within the SIEM and also simulating a security alert on this SIEM.

<h2>Pre-requisites </h2>

Virtual box downloaded: https://www.virtualbox.org/wiki/Downloads
Kali linux downloaded : https://www.kali.org/get-kali/#kali-platforms
Ensure that your kali linux VM is up and running and can access the internet.
When configuring the network for your Kali linux VM make sure that you choose NAT or bridged adapter to ensure it does not get placed on an isolated network

<h2>Network Topology</h2>

![Elastic SIEM drawio](https://github.com/user-attachments/assets/a3156578-463f-4ede-a455-026429fbaff3)


<h2> Set up Elastic SIEM</h2>

Sign up for elastic account by going to the following link: https://cloud.elastic.co/registration

![image](https://github.com/user-attachments/assets/529e8e0a-d937-4d74-afa6-0e0216d530f5)

Enter your name and company( You can enter home for your company)

![image](https://github.com/user-attachments/assets/5560380e-6fb7-4f1f-8602-d4b3b2e0544e)

Select your elastic skill level:

![image](https://github.com/user-attachments/assets/64688296-defc-4b60-bab6-9c343551296e)

Select your primary goal

![image](https://github.com/user-attachments/assets/081f4089-1070-41ea-b64e-4614fd669b63)

Select your use case

![image](https://github.com/user-attachments/assets/6e6f7b91-e74f-48f0-8aeb-b34165da3808)

Choose where you want our data stored( I chose Google Cloud and Northern Virginia)

![image](https://github.com/user-attachments/assets/73d365f1-b378-4a80-9fe7-c926e2baed5d)

Wait for your environment to be set up

![image](https://github.com/user-attachments/assets/9f23e36a-dff5-4602-9708-39f180188696)

Choose the "I'd like to explore on my own" option

![image](https://github.com/user-attachments/assets/b00eae91-27a5-400c-b15a-56ed3b011934)

You should end up at a page that looks like this

![image](https://github.com/user-attachments/assets/f681a51f-df1a-4381-a339-c7e3562aa9df)

<h2>Let's integrate our Elastic SIEM with our Elastic Agent</h2>

Select the hamburger menu then select 'Add integrations"

![image](https://github.com/user-attachments/assets/21d9fd8c-4e34-41a4-988a-898746b4d387)

Select the Elastic Defend

![image](https://github.com/user-attachments/assets/949bde82-22a6-47ac-bda0-39c4a70f1df8)

Select the "Add Elastic Defend"

![image](https://github.com/user-attachments/assets/13ce66ec-3261-48e1-85ab-52886cc825d6)

You should see this page:

![image](https://github.com/user-attachments/assets/f775177f-bbdd-4a9c-a7fc-304cb786674c)

Select the Add integration only *Do not select the "Install Elastic Agent". This will install it on your local machine and not the kali linux VM)

![image](https://github.com/user-attachments/assets/33ebb889-777e-4576-b52d-9cbd161a7e3b)

Configure arbitrary name and description

![image](https://github.com/user-attachments/assets/e5b5365d-1809-4754-b130-8c10b5560e28)

Select the complete EDR option

![image](https://github.com/user-attachments/assets/6252c2a3-131a-4a35-a107-e24510a30b54)

The Agent Policy name can be arbitrary

![image](https://github.com/user-attachments/assets/7910b390-9125-4feb-89ad-6fef31ca2b8d)

Select the save and Continue

![image](https://github.com/user-attachments/assets/15d9464d-29fc-4ae7-8f1f-e56033f7977a)

<h2>Lets add the elastic agent to our Kali Linux VM</h2>

This pop-up should appear, select the "Add elastic agent to your hosts'

![image](https://github.com/user-attachments/assets/16a8d222-6ccf-49c0-9af9-b24e7052a879)

The Following side panel should appear with your information *(I've blocked out my Enrollment token)*

![image](https://github.com/user-attachments/assets/aa085c14-c5a6-45f7-805e-326f88baedcd)

Ensure the Linux tar is selected and that you select the copy clipboard icon

![image](https://github.com/user-attachments/assets/5ebf58fe-596e-4c4f-8e3a-9f622847dd71)

I copy and pasted this into my kali linux terminal

![image](https://github.com/user-attachments/assets/9f6e824d-a8f5-41ac-9ea7-2d8d09475d8f)

An installation should commence, during the installation it may prompt for your kali password

![image](https://github.com/user-attachments/assets/007fd582-19a5-44b6-ae05-f21de5185e96)

The Following warning may also come up, you can enter Y to proceed

![image](https://github.com/user-attachments/assets/10287c16-04d2-4f10-9c44-e434c7bfe40b)

You should See the following Success message indicating that elastic agent has been installed.

*The Download may fail, attempt the download again if it does*

![image](https://github.com/user-attachments/assets/66dafc96-6341-41b9-8942-f90c2eddf39e)

Running the command "sudo systemctl elastic-agent" should provide you with the status 

![image](https://github.com/user-attachments/assets/3fa4ccb8-6ba6-4c0a-9d49-38caf72a2555)

<h3>Let's generate some traffic</h3>

I'm going to run an nmap scan against the kali box itself

![image](https://github.com/user-attachments/assets/662dd975-d39c-4ca8-9fa4-f827b597f3ab)

![image](https://github.com/user-attachments/assets/06f719a3-99b2-481c-bda4-fbb17c561682)

Lets verify the logs that we generated. Go back to the Elastic UI. Select the Hamburger menu -> Observability -> logs

![image](https://github.com/user-attachments/assets/6af3165e-53bd-489c-9bc1-c5dd190bfb30)

Upon selecting that, you should see a large number of events within the log explorer

![image](https://github.com/user-attachments/assets/f9a176eb-d375-45df-bb40-a0fd235a5c80)

To search for the nmap scan we can do a process.args: nmap. Upon doing this we can see a nmberof events

![image](https://github.com/user-attachments/assets/cc9e08f7-e553-40f1-b554-a23842a028da)

Select the expansive arrows and a details pane should pop up on the left side of the screen

![image](https://github.com/user-attachments/assets/6cdec737-373d-4aed-a7c8-ed06a261f337)

Select the "Table" option in the Log details panel that pops up on the left hand side 

![image](https://github.com/user-attachments/assets/dddaa38a-a9d6-41a5-af40-9e744ce623c3)

Scrolling down the table I can see the executed command

![image](https://github.com/user-attachments/assets/ed0984e4-0c96-4e74-9e34-1b5c78e11c13)

<h2>Lets create a dashboard to visualize an event</h2>


Select the Hamburger menu -> Analytics -> Dashboards

![image](https://github.com/user-attachments/assets/c8282b6b-8e19-4f0b-8e44-e81031cf8bc3)

Select the "Create Dashboard"

![image](https://github.com/user-attachments/assets/fc3d74cb-8f58-4cd5-b33d-212845f5717c)

Selct the Create Visualization

![image](https://github.com/user-attachments/assets/90f25bd7-3db2-4214-9990-d1194b24e937)

You should be at a page that looks like this

![image](https://github.com/user-attachments/assets/ef9701b5-ed82-4389-a84a-0016f75cd08a)

Select the visualization type to be Area

![image](https://github.com/user-attachments/assets/78bb8836-5240-42ec-b006-453ba193d2d3)

On the vertical axis, change it to count of records and on the horizontal axis change it to timestamp

![image](https://github.com/user-attachments/assets/59b05f5a-1bcb-4c98-8086-a50d42e72f39)

Select the Save and return to save the visualization

![image](https://github.com/user-attachments/assets/38079bc3-3ab9-493c-8aa9-f482ae031166)

Select the elipses for your visualization to give it a name, select edit visualization

![image](https://github.com/user-attachments/assets/88e250fb-efa6-4523-b526-f61e029e7b9c)

![image](https://github.com/user-attachments/assets/1f7194cf-5491-45cb-9039-84e9f2b2ac84)

Select the title and provide a name that you would like. I chose 'First ElasticSearch query. Ater choosing a title, select Apply

![image](https://github.com/user-attachments/assets/be1054b0-3638-4b4b-a598-a3a343afff94)

After clicking apply, click save in the top right corner and it should prompt for a title

![image](https://github.com/user-attachments/assets/9decae58-7164-4f34-a33e-adbab80831e6)

Lets create a second vizualiztion just to look at the data differently. I ceated a Bar vertical that has time stamp on the horizontal axis and the count on the vertical axis

![image](https://github.com/user-attachments/assets/8e687e91-8102-4254-ba3a-7129ddf8a7e7)

![image](https://github.com/user-attachments/assets/f627218c-3cc8-424e-b190-961a72b820ae)

Generating more traffic to further populate the SIEM

![image](https://github.com/user-attachments/assets/03179628-55e3-4e6d-aa40-8d7123a71aef)

<h2>Lets configure alerts</h2>

Select the Hamburger Icon -> Security -> Alerts

![image](https://github.com/user-attachments/assets/7dae93f0-d4a5-4526-9f22-b5d2d6622e22)

You should be at a page that looks like this:

![image](https://github.com/user-attachments/assets/ee6af9e9-a0a5-4342-99ca-175ded1433bd)

On this page: Select Manage Rules

![image](https://github.com/user-attachments/assets/30883139-233b-41d6-9db7-9f2edb1346ad)

On the following page, select Create New Rule

![image](https://github.com/user-attachments/assets/09e016be-1bca-47e4-a1d2-a04ddd68e624)

Ensure custom query is selected:

![image](https://github.com/user-attachments/assets/928032be-f0dc-445f-b40b-98c1e836067c)


We want the KQL query to be process.name: nmap as shown in the picture

![image](https://github.com/user-attachments/assets/031d679d-766f-4736-9237-74a82838fd75)


Select Continue and go to the About rule section. Apply a name and description and choose the severity

![image](https://github.com/user-attachments/assets/a4d37c51-2a5b-4505-b48f-a778c30bd384)


Click continue on  the Schedule rule section

![image](https://github.com/user-attachments/assets/a606b678-36a4-46ef-9179-14e290d607ec)


Choose the Action you want to take when the conditions for the rule are met. I'm making use of email

![image](https://github.com/user-attachments/assets/db149906-356e-4648-81ab-0ff496567403)


![image](https://github.com/user-attachments/assets/f875c418-5a53-4fd7-977b-715e524fbd6c)


Select the "Create & enable rule button in the bottom right corner

![image](https://github.com/user-attachments/assets/a7d5ee51-fedf-4ff4-8304-1438796490f7)


Doing an Nmap scan from kali linux, I can see that an alert comes in

![image](https://github.com/user-attachments/assets/1dfcbcee-0a0f-4449-bb2b-f9599bb75ed3)


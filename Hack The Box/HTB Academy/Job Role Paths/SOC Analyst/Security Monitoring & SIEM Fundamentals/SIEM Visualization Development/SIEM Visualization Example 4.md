- In this SIEM visualization example, we aim to create a visualization to monitor user additions or removals from the local "Administrators" group from March 5th 2023 to date.
- Our visualization will be based on the following Windows event logs.
	- [4732: A member was added to a security-enabled local group](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4732)
	- [4733: A member was removed from a security-enabled local group](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4733)
- Navigate to the bottom of this section and click on `Click here to spawn the target system!`.
- Navigate to `http://[Target IP]:5601`, click on the side navigation toggle, and click on "Dashboard".
- A prebaked dashboard should be visible. Let's click on the "pencil"/edit icon.
![Visualization 16](https://academy.hackthebox.com/storage/modules/211/visualization16.png)
- Now, to initiate the creation of our first visualization, we simply have to click on the "Create visualization" button.
- Upon initiating the creation of our first visualization, the following new window will appear with various options and settings.
![Visualization 1](https://academy.hackthebox.com/storage/modules/211/visualization1.png)
- There are five things for us to notice on this window:

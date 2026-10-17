🖥️ Windows Server 2025 Lab: Building an Enterprise File Server from Scratch (SMB + NTFS + GPO + ABE)

In my latest lab, I documented the end-to-end process of building a secure, role-based file server. It's one thing to read about NTFS permissions; it's another to build the whole stack and test it from a domain-joined client.

Here is the architecture I built in the video:

1️⃣ SMB File Sharing (The Foundation)
Created the physical folders and published them to the network.
Key takeaway: Share Permissions are the "front door" (I set them to Authenticated Users: Full Control), while NTFS Permissions are the actual locks inside.

2️⃣ NTFS Permissions & AD Groups (The Security)
Locked down the folders using Active Directory Security Groups.
Key takeaway: Never assign individual users to folder ACLs. I removed inherited permissions and restricted access solely to the department groups (e.g., IT-Share, HR-Share).

3️⃣ Access-Based Enumeration (The UX)
Enabled ABE on the Server Manager shares.
Key takeaway: Without ABE, users see every department share but get "Access Denied" when they click. With ABE, the server dynamically hides folders the user doesn't have NTFS rights to. Clean and secure.

4️⃣ GPO Drive Mapping (The Convenience)
Automated the drive mapping using Group Policy Preferences and Item-Level Targeting.
Key takeaway: A mapped drive is convenience, not security. Using Item-Level Targeting ensures only users in the specific AD group get the specific drive letter mapped at login.

The Result:
When a user logs in, they only see the shares and drive letters they are authorized to access. It's automated, secure, and scales perfectly.

I also learned a hard lesson about UAC filtered tokens during testing—even Domain Admins get "Access Denied" in standard File Explorer unless they elevate!

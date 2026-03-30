## **Challenge Overview**

**Name:** H an M Part 2
**Category:** OSINT  
**Difficulty:** Medium
**Points**: 450
###### Challenge Description

A **voice**. An old man. A **war** that shaped a nation.  
That's all you get.  
The Voice: [https://drive.google.com/file/d/1gJEFVDMrNOrwxyKlKFjOvUKYk6YlW7n6/view?usp=sharing](https://drive.google.com/file/d/1gJEFVDMrNOrwxyKlKFjOvUKYk6YlW7n6/view?usp=sharing)  
  
Flag Format: MythX{fullname_age_regiment_commandingofficer_award}  
e.g: MythX{JohnDoe_0_InfantryTown_JaneSmith_ExampleAward}

---
Extract the text from the  voice given:

![](attachments/H%20an%20M%20Part%202.png)

This leads directly to a video:

- **Title:** _Lt. Col. Hari Ram Janu's Aamne Samne Interview_

This confirms the identity of the speaker.
 [Lt. Col. Hari Ram Janu's Aamne Samne Interview](https://www.youtube.com/watch?v=YNatk67GziA)

![](attachments/H%20an%20M%20Part%202-1.png)
In this interview of part2 get the exect voice and commandingofficer and 

Also from Google
The authoritative military history books on the 1965 war (such as _Monsoon War_ and _The Fateful 72 Hours_) record the Commanding Officer of the 4th Grenadiers specifically as **Lt. Col. Farhat Bhatti**


Found a pdf 
https://www.scribd.com/document/845645848/1965-Stories-From-the-Second-Indo-Pakistan-War

![](attachments/H%20an%20M%20Part%202-2.png)

on trying multiple attempt of current age or age that time Find the final Flag
flag: 
```
MythX{HariRamJanu_83_4Grenadiers_FarhatBhatti_SenaMedal}
```
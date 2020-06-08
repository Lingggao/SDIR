# Software Defect Investigation Report

## I. Introduction

[**中文版本报告 (Chinese Version Report)**](https://github.com/Lingggao/SDIR/blob/master/README_ZH_CN.md#%E7%BC%BA-%E9%99%B7-%E8%B0%83-%E6%9F%A5-%E6%8A%A5-%E5%91%8A)

> From: Ling G.  
> Title: Microsoft Windows Insider  
>
> To: Kayo M.  
> Title: Microsoft Engineer  
>
> Date: June 5, 2020

## II. Description

In the use of the Microsoft Pinyin Input Method Editor (IME), the candidate window closes unexpectedly and automatically when some specific Pinyin characters are typed. Users cannot select a candidate character with the cursor or numeric keyboard after the candidate window is closed. If users continue to type one or more Pinyin characters, the candidate window may reappear, and they can proceed to type Chinese characters.

**In one of my Windows 10 devices (running Windows 10 Build 19640.1 currently), the problem is 100% reproducible. The IME candidate window disappears whenever some Pinyin combinations are typed. This problem can be reproduced successfully anywhere in the Windows 10 system, but not just in certain Apps. Also, the candidate window only closes when some pinyin combinations are typed, while most pinyin characters can be entered normally. The problem cannot be solved temporarily or permanently by rebooting the device.**

Up to now (June 5, 2020), I have found a total of 9 Pinyin combinations that may reproduce the problem:

1. shi ' fou ' an ' zhuan（是否安装）
2. zhi ' nen（稚嫩）
3. zong ' xian（总线）
4. suo ' pin（锁频）
5. ci ' pang（祠旁）
6. nin ' jin（您今）
7. jin ' nian（今年）
8. liu'  chan（流产）
9. long ' ming（龙鸣）

**In Build 19640, the latest Windows Insider Preview, not all of the above 9 Pinyin combinations, will cause the IME candidate window to disappear. The problem only resurfaces when the last 4 Pinyin combinations are typed, while the first 5 Pinyin combinations will not produce any problems during the test.**

**At the same time, this problem cannot be reproduced successfully in all devices running Windows 10 Insider Preview. As far as I know, it strikes only in a minimal number of devices and should be considered as a rare problem. Please refer to Chapter III. Testing for more information.**

## III. Testing

To carry out a comprehensive investigation and analysis of this problem, I used three Windows 10 devices for testing, namely Xiaomi Game Laptop 2019, Dell Inspiron 7560, and Microsoft Surface Go. Among them, the first two devices run the Windows 10 Build 19640 system, while Surface Go runs Windows 10 Build 18363.

1. I tested and found that the problem that the IME candidate window disappeared could be reproduced **successfully** in my daily used Xiaomi Game Laptop 2019 device, **which had many third-party applications installed and ran the latest Windows 10 Insider Preview**. The details are described as follows:

|        Pinyin combinations         |  Xiaomi Game Laptop 2019 (Build 19640)   |
| :--------------------------------: | :--------------------------------------: |
| shi ' fou ' an ' zhuan（是否安装） |                  Normal                  |
|         zhi ' nen（稚嫩）          |                  Normal                  |
|        zong ' xian（总线）         |                  Normal                  |
|         suo ' pin（锁频）          |                  Normal                  |
|         ci ' pang（祠旁）          |                  Normal                  |
|         nin ' jin（您今）          | **The IME candidate window disappears.** |
|         jin ' nian（今年）         | **The IME candidate window disappears.** |
|         liu'  chan（流产）         | **The IME candidate window disappears.** |
|        long ' ming（龙鸣）         | **The IME candidate window disappears.** |

2. **However, the problem was irreproducible in Dell Inspiron 7560 that also ran Windows 10 Insider Preview Build 19640, which was an immaculate device without any third-party applications. The IME candidate window did not close whenever pinyin words were typed:**

|        Pinyin combinations         | Dell Inspiron 7560 (Build 19640) |
| :--------------------------------: | :------------------------------: |
| shi ' fou ' an ' zhuan（是否安装） |              Normal              |
|         zhi ' nen（稚嫩）          |              Normal              |
|        zong ' xian（总线）         |              Normal              |
|         suo ' pin（锁频）          |              Normal              |
|         ci ' pang（祠旁）          |              Normal              |
|         nin ' jin（您今）          |              Normal              |
|         jin ' nian（今年）         |              Normal              |
|         liu'  chan（流产）         |              Normal              |
|        long ' ming（龙鸣）         |              Normal              |

3. The problem was also tested and confirmed to be irreproducible in Microsoft Surface Go running the official version of Windows 10 **Build 18363**. **The Microsoft Pinyin IME worked normally.**

4. I executed “[**Clean Boot**](https://support.microsoft.com/en-us/help/929135/how-to-perform-a-clean-boot-in-windows)” in Xiaomi Game Laptop 2019 that could successfully reproduce the problem to determine whether the problem was caused by the interference of third-party applications installed on the device. After testing and confirmation, the IME candidate window still disappeared unexpectedly in the “Clean Boot” state. Thus, **the problem could be reproduced successfully.**

5. I deleted the Microsoft Pinyin IME via Settings > Time and Language > Language > Preferred Language in Xiaomi Game Laptop 2019, I added the IME again. The problem was tested and confirmed to be still reproducible.

6. I scanned the system components using the commands “Dism /Online /Cleanup-Image /ScanHealth” and “SFC /SCANNOW” in Xiaomi Game Laptop 2019 exception was detected.

7. I created a local administrator account in Xiaomi Game Laptop 2019 and logged in the system with the new account for testing. Upon testing and confirmation, the problem did **not** arise under the new account, and the Microsoft Pinyin IME could operate normally. **The problem was eventually solved.**

## IV. Conclusion

According to the test, I can believe that the problem that “the candidate window suddenly disappears when some Pinyin characters are typed in the use of Microsoft Pinyin IME” is caused by the **damage to the local account on my device**. The problem can be solved satisfactorily by creating a new local account. However, I have recently received reports from other users (about three people) about this issue. 

**In this context, I suspect that the Microsoft Pinyin IME may also have certain defects. In summary, I hope that Microsoft can continue to track this defect and verify whether the Microsoft Pinyin IME and its components may directly damage the local account of the system.**

As the test is completed satisfactorily, I hope that the defect investigation report I prepared may help Microsoft engineers to carry out troubleshooting. I sincerely thank Microsoft engineers for their hard work over the years, and wish everyone a happy life and good health!
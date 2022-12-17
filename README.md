# SPCN-011
ขั้นตอนการใช้งานของสร้าง vm and ct on Proxmox cluster

1) Create master vm [ ubuntu-22.04 ]
   - สร้าง master vm มา 1 ตัว แล้วทำการ set ค่าพื้นฐานต่างๆ
   - เช็คเวลาด้วย dateและset update time ด้วยคำสั่ง sudo timedatectl set-timezone Asia/Bangkok
   - ทำการเปิดใช้งาน ip qemu ด้วยคำสั่ง
       - sudo -i
       - apt update
       - apt install qemu-guest-agent
       - systemctl enable qemu-guest-agent
       - และทำการตั้งค่าที่ option ให้เปิดใช้งานตัว Qemu guest agent เป็น Enable 
       ![image](https://user-images.githubusercontent.com/119097836/208231806-5129324d-d311-436a-9524-d692b3f763e6.png)
       - reboot เพื่อรีระบบ
   1.1) clone from template 2 vm
   - Click ที่ vm(master) > Convert to template
   -  หลังจาก vm(master) กลายเป็นtemplate ให้ Click vm แล้วเลือก Clone เป็นตัวvmใหม่2ตัว
   
      ![image](https://user-images.githubusercontent.com/119097836/208231956-14524eff-e116-4604-8b81-7d97f0af8b32.png)   
   - ทำการsetระบบโดย
        - date เพื่อเช็ค timezone
    
          ![image](https://user-images.githubusercontent.com/119097836/208232376-56184cbe-9e34-43c5-98b5-032604885797.png) 
        - ทำการเปลี่ยนipของระบบเพื่อไม่ให้ipซ้ำกันโดย
            - sudo -i
            - rm /var/lib/dbus/machine-id
            - nano /etc/machine-id เพื่อลบ id เก่าออก
            - ln -s /etc/machine-id /var/lib/dbus/machine-id เพื่อ link เชื่อมต่อกับ machine-id
            - reboot เพื่อรี ip ใหม่
            - หลังเปลี่ยน ip clone1
              ![image](https://user-images.githubusercontent.com/119097836/208232581-d23ef48a-1372-455a-bf8d-3e233a1f86e3.png)
            - หลังเปลี่ยน ip clone2
              ![image](https://user-images.githubusercontent.com/119097836/208232616-37057b73-ae44-4fae-bc6d-e59b2a058c35.png)
 
2) create vm from other os
   - Create VM จากนั้นทำการตั้งค่าที่กำหนดโดยระบบปฏิบัติการที่เลือกใช้คือ Linux Mint
      - Summary ของ Linux Mint
        ![image](https://user-images.githubusercontent.com/119097836/208232705-a59b5485-2944-4519-a331-415aca64aaae.png)
      - หน้า console screen
        ![image](https://user-images.githubusercontent.com/119097836/208232727-2e0b8a8c-56ba-4d6c-be89-31b349ffe4be.png)  

3) create container template 
   - Click create container template เพื่อสร้าง CT
      - Summary 
        ![image](https://user-images.githubusercontent.com/119097836/208232763-9f4f58ff-a806-4b3d-8260-9e34a58989bb.png)
      - console screen 
        ![image](https://user-images.githubusercontent.com/119097836/208232982-a995092b-eb07-4c6d-b6a3-85ffe7938e4e.png)

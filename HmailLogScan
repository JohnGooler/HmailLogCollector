from time import gmtime, strftime
import os

NowTime = strftime("%Y-%m-%d", gmtime())
print(NowTime)

with open("whitelist.txt", "r") as wl:
    IpWl = wl.readlines()
    

with open(f"hmailserver_{NowTime}.log", 'r') as log:
# with open("hmailserver_2023-09-09.log", 'r') as log:
    AllLogs = log.readlines()
    for line in AllLogs:
        line = line.split("\t")
        if str(line[0]) == '"SMTPD"':
            # print(line)
            if line[5] == '"SENT: 550 Unknown user"\n':
                ip = str(line[4].replace('"', ''))+"\n"
                with open("tempIPs.txt", "a") as f:
                    if ip in IpWl or ip.strip("\n") in IpWl:
                        pass
                    else:
                        f.write(ip)


#remove Dubpicated ips
with open("tempIPs.txt", 'r') as f:
    List_Of_IPS = f.readlines()
    No_duplicate = list(set(List_Of_IPS))
    with open("AttachersIPs.txt", 'a') as attckers:
        # No_duplicate = str(No_duplicate)
        for i in No_duplicate:
            attckers.write(i)

with open("AttachersIPs.txt", "r") as f:
    IPS = f.readlines()
    No_Dup_IP = list(set(IPS))
    with open("Final_IP_List.txt", "w") as final:
        for i in No_Dup_IP:
            final.write(i)

if os.path.exists("tempIPs.txt"):
    print("remove Temp file")
    os.remove("tempIPs.txt")
else:
    print("tempIPs.txt Not exist")

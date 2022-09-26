# docker-ilo-workloader
* Notes




# Part 1
* You can populate the pce.yaml by running workloader pce-add or copy the following template (Make sure to create your own PCE service account API key and PCE info)

* Note: Make sure you are root in that directory

```
root@6bee01ea21ce:/var/workloader/linux/linux-v8.24.6# ls -l
total 16212
drwxr-xr-x 2 root root      197 Aug 11 00:24 illumio-templates
-rw-r--r-- 1 root root     1136 Aug 26 13:55 pce.yaml
-rw-r--r-- 1 root root     3877 Aug 11 00:24 workload-identifier-default.csv
-rwxr-xr-x 1 root root 16592380 Aug 11 00:24 workloader
-rw-r--r-- 1 root root        0 Aug 26 13:55 workloader.log
```


* To populate multi-line text file from shell, use printf

```
printf "
debug: false
default_pce_name: pce-illumio-com
max_entries_for_stdout: 100
no_prompt: false
output_format: both
pce-illumio-com:
    disabletlschecking: false
    fqdn: pce.illumio.com
    key: 4e7ce63a4329890a9afacb9accd8821
    org: 1
    port: 443
    user: api_126220928cc25f
    userhref: /users/1
target_pce: pce-illumio-com
update_pce: false
verbose: false

" >> pce.yaml
```


*Quick test for workloader (if you have some workloads in idle to run the following to print in console the output via stdout)
```
./workloader compatibility -i --out stdout
```

Expected output should look like this (depends on your workloads for sure)

```
testuser@6bee01ea21ce:/var/workloader/linux/linux-v8.24.6$ ./workloader compatibility -i --out stdout
2022/08/26 14:02:17 open workloader.log: permission denied
testuser@6bee01ea21ce:/var/workloader/linux/linux-v8.24.6$ sudo ./workloader compatibility -i --out stdout
2022-08-26 14:02:22  [INFO] - reviewed compatibility report 9 of 9 (100%).
+---------------------------------------------------+--------------------------------------------------------+--------+
|                     HOSTNAME                      |                          HREF                          | STATUS |
+---------------------------------------------------+--------------------------------------------------------+--------+
| venx2-external-vsphere.docker.illumio.consulting  | /orgs/1/workloads/1f7534a2-15a2-4c44-abca-20de1bcfa43e | yellow |
+---------------------------------------------------+--------------------------------------------------------+--------+
| ven5-ubuntu-docker.illumio.consulting             | /orgs/1/workloads/2f99dce0-e996-4a89-9cc7-af8ceba72eca | yellow |
+---------------------------------------------------+--------------------------------------------------------+--------+
| B0-B3-ubuntu-server-2004                          | /orgs/1/workloads/23151cd2-2df3-4e59-851f-66a681d4c3f3 | yellow |
+---------------------------------------------------+--------------------------------------------------------+--------+
| B0-B2-ubuntu-server-2004.hamra.services           | /orgs/1/workloads/17a30f65-5f8d-4dcb-b0fc-bde0974b4a57 | yellow |
+---------------------------------------------------+--------------------------------------------------------+--------+
| venx1-external-vsphere.regular.illumio.consulting | /orgs/1/workloads/b66d6644-3f84-406d-bd46-89dff3069337 | yellow |
+---------------------------------------------------+--------------------------------------------------------+--------+
| venx5-external-vsphere.regular.illumio.consulting | /orgs/1/workloads/7f6a3a44-6c13-47c3-a77e-5585568f3ed1 | yellow |
+---------------------------------------------------+--------------------------------------------------------+--------+
2022-08-26 14:02:22  [INFO] - 6 compatibility reports exported.
2022-08-26 14:02:22  [INFO] - compatibility completed
```


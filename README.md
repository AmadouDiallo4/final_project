# Clone the master branch on your computer:
Copy the master branch on your computer, in the directory you choose.

`git clone https://github.com/schneiderana/final_project.git -b master`

# Create ssh-key:
Create a ssh-key named **part1_rsa** with the following command, inside the directoruy **part1**.

`cd part1`
`ssh-keygen -f part1_rsa`

# Start the servers:
You will have a machine **control** to have a linux environment (if you work on a linux environment, you don't need it !) plus the 5 servers for wordpress:
s0.infra = DNSmasq + HAPROXY
s1.infra = where is running wordpress (Apache2 + PHP7)
s2.infra = where is also running wordpress (Apache2 + PHP7)
s3.infra = database server (MariaDB)
s4.infra = NFS server (share /home/data)

To start your machines, do:
`vagrant up && vagrant provision`

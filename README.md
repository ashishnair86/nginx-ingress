
# nginx-ingress

                      Internet User
                             |
                 http://ec2-xx-xx-xx.compute.amazonaws.com/web
                             |
                +----------------------------------+
                |  AWS Security Group (opens 30737)|
                +----------------------------------+
                             |
                       EC2 Public IP
                             |
                     +----------------+
                     |   NodePort 30737|
                     +----------------+
                             |
                 [k3s Node - EC2 Instance]
                             |
        +----------------------------------------+
        |    ingress-nginx-controller (Pod)      |
        |  (listens on :30737 external, :80/443 inside)  |
        +----------------------------------------+
                             |
               Ingress Rule: Host + Path (/web)
                             |
                             v
                 +-----------------------+
                 |  Service: nginx-service|
                 |   (ClusterIP: 10.43.x.x|
                 |    Port 80)            |
                 +-----------------------+
                             |
                             v
                    +------------------+
                    | Pod: nginx        |
                    | (serves content at|
                    | path "/")          |
                    +------------------+

# Ingress Traffic Diagram



```
API   <------------   NGINX CONTROLLER          HOST PORT / LB <
                            |                                  |
                            |                                  |
                            |                                  |
CHEDDAR                     |                            BROWSER HTTP;Cheddar
CHEDDAR  <------------------- 
CHEDDAR
CHEDDAR
CHEDDAR

    The NGINX is storing IP of the Cheddars and
    updating itself as things change dynamically 
    so proxy can update itself. WOW!

```
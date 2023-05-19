# Deployment Visual Walkthrough

## 19.000 words
- they say a picture is worth one thousands words
- the following 19 slides show what really happens when we run:

`kubectl run web --image=nginx --replicas=3`

https://kubernetes.io/docs/concepts/workloads/controllers/deployment/







Check video

```

                            Deployment DB (ETC)
                                    |
                                    |
                                    |

    DEVOPS      <---------->    API SERVER    <-----------> kubelet 
                                |       |
                                |       |
                        scheduler       Controller
                                        Manager

                            CONTROL PLANE               WORKER NODES
```



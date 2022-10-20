# Creating an Application with Helm

0. Init a helm chart

    `$` `helm create parrot`
    
0. Tree it

    `$` `tree parrot`
    
0. Edit the values.yaml to use another simple service

    ```diff
      image:
    -    repository: nginx
         pullPolicy: IfNotPresent
         # Overrides the image tag whose default is the chart appVersion.
    -    tag: ""
      image:
    +    repository: ealen/echo-server
         pullPolicy: IfNotPresent
         # Overrides the image tag whose default is the chart appVersion.
    +    tag: "0.7.0"
    ```
    
0. Also, edit values.yaml to use ingress.

    ```diff
      ingress:
    -   enabled: false
    +   enabled: true
        className: ""
        annotations: {}
    -     # kubernetes.io/ingress.class: nginx
    -     # kubernetes.io/tls-acme: "true"
    +     alb.ingress.kubernetes.io/group.name: k8-internal
    +     alb.ingress.kubernetes.io/healthcheck-path: /namespaces
    +     alb.ingress.kubernetes.io/listen-ports: '[{"HTTPS": 443}]'
    +     alb.ingress.kubernetes.io/scheme: internal
    +     alb.ingress.kubernetes.io/target-type: ip
    +     kubernetes.io/ingress.class: alb
      hosts:
    -    - host: chart-example.local
    +    - host: parrot.<domain>
           paths:
             - path: /
               pathType: ImplementationSpecific
    ```
   
0. Install the chart

    `$` `helm install parrot parrot/`
    
0. Get pod, deploy, svc, ing

0. Port-forward

0. Set up your load balancer

0. Try it out! Go to `https://parrot.<domain>` in your browser.

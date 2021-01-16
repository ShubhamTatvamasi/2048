# game-2048

deploy game-2048:
```bash
kubectl create deployment game-2048 --image=blackicebird/2048
kubectl expose deployment game-2048 --port=80 --name=game-2048
```
> user: `admin` pass: `admin`

delete everything:
```bash
kubectl delete deploy/game-2048 svc/game-2048 ing/game-2048
```

create ingress value:
```bash
kubectl apply -f - << EOF
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: game-2048
spec:
  tls:
    - hosts:
      - 2048.k8s.shubhamtatvamasi.com
      secretName: letsencrypt
  rules:
    - host: 2048.k8s.shubhamtatvamasi.com
      http:
        paths:
        - path: /
          backend:
            serviceName: game-2048
            servicePort: 80
EOF
```

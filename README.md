# CKAD
Préparation Certification CKAD 


Listes d'exercices pour la préparation de la certification CKAD : 
 
 
 
- Exercices CKAD par catégorie (réponses , commande et tout 28q) : https://grok.com/c/db6198a5-84b0-4b64-b025-bac78b8a8aaa?rid=2cc27c3e-9df7-4dcc-a1a6-0587ca790f4d
- Exercices CKAD page entière (all catégories 23q) : https://grok.com/c/0bc13f71-cfe0-4b60-83ba-6ba6ef62e12f?rid=61e56fcc-9267-435f-bfdd-9aabeaf01cc5
- Réponses aux Exercices CKAD Page entière ( + comparaison avec site stéphane robert ce qu'il manque)  : https://grok.com/c/c2d7c41d-65e0-4a14-965b-108d86c9dfc6?rid=f2deecd7-cb8c-4110-87de-b9f4289092ed
- Exercices de troubleshooting CKAD (26q) : https://grok.com/c/cb21f07e-e3cd-4d56-9c3a-8dfba4f1f1f7?rid=7ba18847-0701-4b54-bfc3-97a8e9c0c896
- Exercices de préparations Application Environment, Configuration and Security (25%) : https://grok.com/project/3fb55066-bfb1-4ea6-9d0f-0d8ade34b89c?chat=acd84529-ecba-4662-8ef6-1c1594eb6498&rid=c98de82a-0c2b-44c9-beb5-bc6723359196
- Exercices de préparations Application Deployment (20%) : https://grok.com/project/3fb55066-bfb1-4ea6-9d0f-0d8ade34b89c?chat=d133d434-96ab-433c-984f-86b9fae8ca3d&rid=bbb974ef-fcab-4f40-9afd-4af7ad8bf3f4
- Exercices de préparations Application Design and Build (20%) : https://grok.com/project/3fb55066-bfb1-4ea6-9d0f-0d8ade34b89c?chat=5f9d54df-6c97-4b86-9794-a9c9edee7524&rid=c9343baf-2417-4b2c-b3d4-47d404c8f212
- Exercices de préparations Services and Networking (20%) :   https://grok.com/project/3fb55066-bfb1-4ea6-9d0f-0d8ade34b89c?chat=f86c202c-380b-4c64-a008-4ae1183be57e&rid=008e7350-d5c0-49d7-8c8a-998bdc3309dc
- Exercices de préparations Application Observability and Maintenance (15%) : https://grok.com/project/3fb55066-bfb1-4ea6-9d0f-0d8ade34b89c?chat=1a711d8d-ba9f-45d8-b9e4-f33a86e24c73&rid=c296e3e4-25a2-44db-a2c3-944341025d13
 
 
 
- Toutes les commandes kubectl et par catégorie d'exam CKAD : https://grok.com/c/1d4e7603-515b-4374-a133-08c5fc233a53?rid=36fa0995-bc17-4de6-9717-b13073826d07
- différentes commandes pour modifier le contenu d'un déploiment : https://grok.com/c/f4417882-9b69-4f89-a20c-06beeec11e14?rid=b0e71565-eb02-4f5e-8050-291fe5325af4
- différentes commandes avec shortname : https://grok.com/project/3fb55066-bfb1-4ea6-9d0f-0d8ade34b89c?chat=3c40b6ae-94a8-4bbc-a0a5-bec92c647eb2&rid=3c87c5c0-e19c-49fa-9128-4b6b2132e71a
 
 
 
- page avec question sur stratégie de déploiment : https://grok.com/project/3fb55066-bfb1-4ea6-9d0f-0d8ade34b89c?chat=c02ad12e-9e65-42cc-bc98-aba95b1183c4&rid=4d071c21-ebde-44b3-a5aa-2e2586409c20
- page avec questions sur namespace : https://grok.com/project/3fb55066-bfb1-4ea6-9d0f-0d8ade34b89c?chat=7fb9e6b5-2120-42e8-b335-7f6fe667ac0e&rid=ce765130-e810-4390-9d55-32a1068f74f5
- page avec objets sous-objets et champs minimum à connaître pour la CKAD : https://grok.com/project/3fb55066-bfb1-4ea6-9d0f-0d8ade34b89c?chat=dc276563-dac0-4ce2-b151-146c7934bfe2&rid=2c999ae4-7bd7-4f71-b750-977d90657f04



3. Application Observability and Maintenance (15%) 

1. Application Design and Build (20%)

Objets principaux : Pod, Deployment, DaemonSet, StatefulSet, Job, CronJob, PersistentVolume, PersistentVolumeClaim, StorageClass.
Champs racine communs à tous les workloads :

apiVersion (v1, apps/v1, batch/v1)
kind
metadata.name
metadata.labels (très important pour selector)
metadata.annotations (parfois pour Helm/Kustomize)

Deployment / DaemonSet / StatefulSet :

spec.selector.matchLabels
spec.template.metadata.labels (doit matcher le selector)
spec.replicas (Deployment/StatefulSet)
spec.service (StatefulSet – headless service)

Job :
spec.template (pod template)

spec.completions  !!!!!!!!!!!!!!
spec.parallelism  !!!!!!!!!!!!!
spec.backoffLimit !!!!!!!!!!!!
spec.activeDeadlineSeconds !!!!!!!!!!!!!!!!!!!!!!
spec.template.spec.restartPolicy → OnFailure ou Never (jamais Always) !!!!!!!!!!!!!!!!!!!!!

CronJob :

spec.schedule (format cron)  !!!!!!!!!
spec.jobTemplate.spec.template (le pod template du Job)

volumes[] (ephemeral + persistent)
name
emptyDir (sizeLimit, medium: Memory)
persistentVolumeClaim (claimName)
configMap / secret (pour plus tard)

volumeMounts[] dans chaque container
name, mountPath, subPath, readOnly

2. Application Deployment (20%)
Objets principaux : Deployment, (parfois StatefulSet pour stratégie), Helm, Kustomize.
Champs racine spécifiques Deployment :

spec.strategy.type → RollingUpdate (défaut) ou Recreate
spec.strategy.rollingUpdate
maxUnavailable (ex: 25% ou 1)
maxSurge (ex: 25% ou 1)

spec.minReadySeconds
spec.progressDeadlineSeconds (pour savoir quand un rollout échoue)

Blue/Green & Canary (primitives Kubernetes) :

Deux Deployments + service selector qui change (ou labels temporaires)
Ou Deployment avec maxUnavailable: 0 + maxSurge: 100% pour canary manuel

PodSpec (peu de nouveauté ici, mais tu réutilises tout le template du point 1)
Helm & Kustomize : pas de champs YAML spécifiques dans le manifest, mais tu dois savoir :

helm install/upgrade --set / --values
kustomization.yaml → resources:, patchesStrategicMerge:, configMapGenerator, secretGenerator


3. Application Observability and Maintenance (15%)
Objets principaux : Deployment, Pod, (kubectl commands).
PodSpec / spec.template.spec (cette section est très lourde) :
Dans containers[] uniquement :

livenessProbe
readinessProbe
startupProbe
Types : httpGet, tcpSocket, exec
Champs communs : initialDelaySeconds, periodSeconds, timeoutSeconds, successThreshold, failureThreshold, terminationGracePeriodSeconds

lifecycle (hooks)
preStop
postStart
(exec ou httpGet)


Autres champs utiles pour debugging :

terminationGracePeriodSeconds (pod level)
stdin, tty (parfois pour debug)

4. Application Environment, Configuration and Security (25%) – le plus lourd
Objets principaux : ConfigMap, Secret, Deployment/Pod, ServiceAccount, ResourceQuota, LimitRange, CRD/Operator (découverte seulement), SecurityContext.
Champs racine :

metadata.labels / metadata.annotations
spec.serviceAccountName (dans pod spec)
automountServiceAccountToken: false (sécurité)

PodSpec / spec.template.spec (très important) :
Ressources (dans chaque container) :
YAMLresources:
  requests:
    cpu: "250m"
    memory: "256Mi"
    ephemeral-storage: "1Gi"
  limits:
    cpu: "500m"
    memory: "512Mi"
    ephemeral-storage: "2Gi"
Config & Secrets (plusieurs façons) :

env[]
value
valueFrom.configMapKeyRef
valueFrom.secretKeyRef
valueFrom.fieldRef (metadata.name, status.podIP, etc.)

envFrom[]
configMapRef
secretRef

volumeMounts + volumes.configMap / volumes.secret

Security :
Pod level (spec.securityContext) :

runAsUser, runAsGroup, fsGroup
supplementalGroups
sysctls[]

Container level (containers[].securityContext) :

runAsNonRoot: true
readOnlyRootFilesystem: true
allowPrivilegeEscalation: false
capabilities
add / drop (ex: NET_ADMIN, SYS_TIME, ALL)

privileged: false
seccompProfile.type (RuntimeDefault, Localhost, Unconfined)

Autres :

imagePullSecrets[] (pod level)

CRD / Operators : tu dois juste savoir les lister (kubectl get crd) et les utiliser comme n’importe quel objet (pas de création de CRD à l’examen).


. Services and Networking (20%)
Objets principaux : Service, Ingress, NetworkPolicy (pas de champs dans le pod spec ici, mais labels très importants).
Service :

spec.selector (doit matcher les labels du pod template)
spec.ports[] (port, targetPort, nodePort, protocol)
spec.type (ClusterIP, NodePort, LoadBalancer)

Ingress (networking.k8s.io/v1) :

spec.rules[]
host
http.paths[]
path, pathType (Prefix, Exact, ImplementationSpecific)
backend.service.name + backend.service.port.number



NetworkPolicy :

spec.podSelector.matchLabels
spec.policyTypes (Ingress, Egress)
spec.ingress[] / spec.egress[]
from / to (podSelector, namespaceSelector, ipBlock)
ports (port + protocol)


Dans le PodSpec (indirect) :

Les labels du spec.template.metadata.labels sont critiques (sélection par Service et NetworkPolicy).



niveau pod donc pod security context = 
runAsUser / runAsGroup ; fsGroup ; seccompProfile.type au niveau du container toutes les valeurs auf fsGroup : 
runAsNonRoot ; readOnlyRootFilesystem ; allowPrivilegeEscalation ; privileged ; capabilities.drop/add ; runAsUser / runAsGroup ; seccompProfile.type
























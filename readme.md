# SIT737 - 9.1P

1. Apply all the yaml files

```
kubectl apply -f createHeadlessService.yaml
kubectl apply -f createConfigMap.yaml
kubectl apply -f createMongoDbSecret.yaml
kubectl apply -f createStatefulSet.yaml
```

2. You can view all your pod in your kubernetes dashboard

3. Check all the pods working correctly
```
kubectl get svc
kubectl get configmap
kubectl get statefulset
```

4. Start mongo
```
kubectl exec -it mongo-0 /bin/bash
```

5. Enter the following commands to enter the pods
```
> mongo
> use admin
```

6. Enter db commands
```
db.<collection>.find()
# To retrive all the data

db.<collection>.insertOne({"name":"Adi","age":20})
# To add data

db.<collection>.updateOne({"name":"Adi"},{$set:{"age":20}})
# To update the data

db.<collection>.deleteOne({"name":"Adi"})
# To delete the data
```

7. Change to secondary pod
```
kubectl exec -it mongo-1 /bin/bash
```

8. It only has read-only access, to see the database
```
rs.slaveOk()
```

9. See the data
```
db.<collection>.find()
```
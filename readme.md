# SIT737 - 9.1P

## Setup Mongodb

1. Update xcode (mac - ARM64)
```
xcode-select --install
```

2. Apply homebrew formula for mongodb
```
brew tap mongodb/brew
```

3. Update Homebrew and all existing formulae
```
brew update
```

4. Install mongodb into your mac
```
brew install mongodb-community@6.0
```

5. Check mongodb in terminal
```
mongod --version
```

## Steps to add mongodb into kubernetes
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

6. Insert one data
```
db.<collection>.insertOne({"name":"Adi","age":20})
# To add data
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

In secondary, you can't change or add the record. To change or add you need to

10. Change to primary
```
kubectl exec -it mongo-0 /bin/bash
```

11. Performing CRUD
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

Reference:
https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-os-x/
https://www.mongodb.com/docs/manual/reference/method/js-collection/
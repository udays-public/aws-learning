1. Set up local dynamo db https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DynamoDBLocal.DownloadingAndRunning.html

wget https://s3.ap-south-1.amazonaws.com/dynamodb-local-mumbai/dynamodb_local_latest.tar.gz

java -D"java.library.path=./DynamoDBLocal_lib" -jar DynamoDBLocal.jar -sharedDb
aws dynamodb list-tables --endpoint-url http://localhost:8000

aws dynamodb create-table     --table-name Music     --attribute-definitions         AttributeName=Artist,AttributeType=S         AttributeName=SongTitle,AttributeType=S     --key-schema AttributeName=Artist,KeyType=HASH AttributeName=SongTitle,KeyType=RANGE     --provisioned-throughput ReadCapacityUnits=1,WriteCapacityUnits=1  --endpoint-url http://localhost:8000

aws dynamodb put-item --table-name Music  --item     '{"Artist": {"S": "No One You Know"}, "SongTitle": {"S": "Call Me Today"}, "AlbumTitle": {"S": "Somewhat Famous"}}' --return-consumed-capacity TOTAL  --endpoint-url http://localhost:8000

aws dynamodb put-item  --table-name Music --item '{ "Artist": {"S": "Uday Shanbhag"}, "SongTitle": {"S": "Dum maaro Dum"}, "AlbumTitle": {"S": "Songs About DUm"},"CreatedBy": {"S": "Uday"} }' --return-consumed-capacity TOTAL --endpoint-url http://localhost:8000

aws dynamodb query --table-name Music --key-conditions file://query.json --endpoint-url http://localhost:8000


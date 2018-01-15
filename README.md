# app-market
It is the application market setting group of the home application.

## Create OData
The procedure for creating OData for storing application market data with curl command is as follows. 

1. Create OData called applist under the box. (Example: under main)  

		curl "https://{UnitFQDN}/{CellName}/__/applist" -X MKCOL -i -H 'Authorization: Bearer {AccessToken}' -H 'Accept: application/json' -d '<?xml version="1.0" encoding="utf-8"?><D:mkcol xmlns:D="DAV:" xmlns:p="urn:x-personium:xmlns"><D:set><D:prop><D:resourcetype><D:collection/><p:odata/></D:resourcetype></D:prop></D:set></D:mkcol>'

1. Create an EntityType in the created applist. (EntityType name: Apps)

		curl "https://{UnitFQDN}/{CellName}/__/applist/\$metadata/EntityType" -X POST -i -H 'Authorization: Bearer {AccessToken}' -H 'Accept: application/json' -d '{ "Name": "Apps" }'

1. Register Property in Apps.

		BarUrl
		curl "https://{UnitFQDN}/{CellName}/__/applist/\$metadata/Property" -X POST -i -H 'Authorization: Bearer {AccessToken}' -H 'Accept: application/json' -d '{"Name": "BarUrl","_EntityType.Name": "Apps","Type": "Edm.String","Nullable": false}'

		SchemaUrl
		curl "https://{UnitFQDN}/{CellName}/__/applist/\$metadata/Property" -X POST -i -H 'Authorization: Bearer {AccessToken}' -H 'Accept: application/json' -d '{"Name": "SchemaUrl","_EntityType.Name": "Apps","Type": "Edm.String","Nullable": false,"IsKey":true}'

		BoxName
		curl "https://{UnitFQDN}/{CellName}/__/applist/\$metadata/Property" -X POST -i -H 'Authorization: Bearer {AccessToken}' -H 'Accept: application/json' -d '{"Name": "BoxName","_EntityType.Name": "Apps","Type": "Edm.String","Nullable": false}'

		Type
		curl "https://{UnitFQDN}/{CellName}/__/applist/\$metadata/Property" -X POST -i -H 'Authorization: Bearer {AccessToken}' -H 'Accept: application/json' -d '{"Name": "Type","_EntityType.Name": "Apps","Type": "Edm.String"}'

1. Create an Entity (data) in the created Apps.

		curl "https://{UnitFQDN}/{CellName}/__/applist/Apps" -X POST -i -H 'Authorization: Bearer {AccessToken}' -H 'Accept: application/json' -d '{"BarUrl": "{BoxName}/{BarFileName}","SchemaUrl": "{SchemaUrl}","BoxName": "{BoxInstallBoxName}","Type": "{CellType}"}'
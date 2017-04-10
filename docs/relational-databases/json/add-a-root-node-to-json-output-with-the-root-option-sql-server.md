---
title: "Agregar un nodo ra&#237;z a la salida JSON con la opci&#243;n ROOT (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ROOT (PARA JSON)"
ms.assetid: b9afa74a-f59f-483e-a178-42be2e9882c9
caps.latest.revision: 16
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 15
---
# Agregar un nodo ra&#237;z a la salida JSON con la opci&#243;n ROOT (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Para agregar un solo elemento de nivel superior a la salida JSON de la cláusula **FOR JSON**, especifique la opción **ROOT**.  
  
 Si no especifica la opción **ROOT** , la salida JSON no incluye un elemento raíz.  
  
## Ejemplos  
 En la tabla siguiente se muestra la salida de la cláusula **FOR JSON** con y sin la opción **ROOT** .  
  
 En los ejemplos de la tabla siguiente se asume que el argumento *RootName* opcional está vacío. Si proporciona un nombre para el elemento raíz, este valor reemplaza el valor **root** en los ejemplos.  
  
 Sin la opción **ROOT**  
  
```json  
{  
   <<json properties>>  
}  
```  
  
```json  
[  
   <<json array elements>>  
]  
```  
  
 Con la opción **ROOT**  
  
```json  
{   
  "root": {  
   <<json properties>>  
 }  
}  
```  
  
```json  
{   
  "root": [  
   << json array elements >>  
  ]  
}  
```  
  
 Este es otro ejemplo de una cláusula **FOR JSON** con la opción **ROOT** . En este ejemplo se especifica un valor para el argumento *RootName* opcional.  
  
 **Query**  
  
```tsql  
SELECT TOP 5   
      BusinessEntityID As Id,  
      FirstName, LastName,  
      Title As 'Info.Title',  
      MiddleName As 'Info.MiddleName'  
  FROM Person.Person  
  FOR JSON PATH, ROOT('info')  
```  
  
 **Resultado**  
  
```json  
{  
  "info": [  
    {"Id":1,"FirstName":"Ken","LastName":"Sánchez","Info":{"MiddleName":"J"}},  
    {"Id":2,"FirstName":"Terri","LastName":"Duffy","Info":{"MiddleName":"Lee"}},  
    {"Id":3,"FirstName":"Roberto","LastName":"Tamburello"},  
    {"Id":4,"FirstName":"Rob","LastName":"Walters"},  
    {"Id":5,"FirstName":"Gail","LastName":"Erickson","Info":{"Title":"Ms.","MiddleName":"A"}}  
  ]  
}  
  
```  
  
 **Resultado (sin raíz)**  
  
```json  
[  
  {"Id":1,"FirstName":"Ken","LastName":"Sánchez","Info":{"MiddleName":"J"}},  
  {"Id":2,"FirstName":"Terri","LastName":"Duffy","Info":{"MiddleName":"Lee"}},  
  {"Id":3,"FirstName":"Roberto","LastName":"Tamburello"},  
  {"Id":4,"FirstName":"Rob","LastName":"Walters"},  
  {"Id":5,"FirstName":"Gail","LastName":"Erickson","Info":{"Title":"Ms.","MiddleName":"A"}}  
]  
  
```  
  
## Vea también  
 [Cláusula FOR &#40;Transact-SQL&#41;](../Topic/FOR%20Clause%20\(Transact-SQL\).md)  
  
  
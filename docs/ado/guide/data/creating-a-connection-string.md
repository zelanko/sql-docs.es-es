---
title: "Crear una cadena de conexión | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connections [ADO]
- connection strings [ADO]
ms.assetid: 14eae122-2d1e-40c8-b88e-b7cb8dfbc93b
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 90105b448604f3b99fefc2598fa375677f0bbdb4
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="creating-a-connection-string"></a>Creación de una cadena de conexión
Una cadena de conexión consta de una lista de pares de valor del argumento (es decir, los parámetros), separada por punto y coma. Por ejemplo:  
  
```  
"arg1=val1; arg2=val2; ... argN=valN;"  
```  
  
 Todos los parámetros se deben reconocer ADO o el proveedor especificado.  
  
 ADO reconoce los siguientes cinco argumentos en una cadena de conexión.  
  
|Argumento|Description|  
|--------------|-----------------|  
|*Proveedor*|Especifica el nombre de un proveedor que se usará para la conexión.|  
|*Nombre de archivo*|Especifica el nombre de un archivo específico del proveedor (por ejemplo, un objeto de origen de datos almacenados) que contiene información de conexión predefinida.|  
|*Dirección URL*|Especifica la cadena de conexión como una dirección URL absoluta que identifica un recurso, como un archivo o directorio.|  
|*Proveedor remoto*|Especifica el nombre de un proveedor que se usará al abrir una conexión de cliente. (Solo servicio de datos remotos).|  
|*Servidor remoto*|Especifica el nombre de ruta de acceso del servidor que se usará al abrir una conexión de cliente. (Solo servicio de datos remotos).|  
  
 Otros argumentos se pasan al proveedor con el nombre de la *proveedor* argumento, sin ningún procesamiento mediante ADO.  
  
 La aplicación HelloData en [HelloData: una aplicación ADO sencilla](../../../ado/guide/data/hellodata-a-simple-ado-application.md) usa la cadena de conexión siguiente:  
  
```  
m_sConnStr = "Provider=SQLOLEDB;Data Source=MySqlServer;" & _  
             "Initial Catalog=Northwind;Integrated Security='SSPI';"  
```  
  
 En esta cadena de conexión ADO sólo reconoce el `"Provider=SQLOLEDB"` parámetro, que especifica el proveedor Microsoft OLE DB para SQL Server como el origen de datos de ADO. El resto de los pares de valor del argumento, `"Data Source=MySqlServer; Initial Catalog=Northwind;Integrated Security='SSPI';"`, se pasan literalmente a este proveedor. El tipo y la validez de estos parámetros son específicas del proveedor. Para obtener información acerca de los parámetros válidos que se pueden pasar en la cadena de conexión, consulte la documentación del proveedor individual.  
  
 Según el proveedor OLE DB para la documentación de SQL Server, puede sustituir "Server" para el *origen de datos* parámetro y "Base de datos" para la *Initial Catalog* parámetro. Por lo tanto, la cadena de conexión siguiente generaría resultados idénticos al anterior:  
  
```  
m_sConnStr = "Provider=SQLOLEDB;Server=MySqlServer;" & _  
             "Database=Northwind;Integrated Security='SSPI';"  
```


---
title: Secuencias de comandos | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- command streams [ADO]
- streams [ADO], command
ms.assetid: 0ac09dbe-2665-411e-8fbb-d1efe6c777be
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1be2cc9528e62e548feb242b06686ad50a1753c8
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="command-streams"></a>Secuencias de comandos
ADO siempre ha sido compatible proporcionados por el comando en formato de cadena especificado por el **CommandText** propiedad. Como alternativa, con ADO 2.7 o posterior, también puede utilizar una secuencia de información para la entrada de comando mediante la asignación de la secuencia a la **CommandStream** propiedad. Puede asignar un ADO **flujo** objeto o cualquier objeto que admita el modelo COM **IStream** interfaz.  
  
 El contenido de la secuencia de comandos se pasa simplemente desde ADO al proveedor, por lo que el proveedor debe admitir la entrada de comando de flujo para que funcione esta característica. Por ejemplo, SQL Server admite las consultas en forma de plantillas XML o extensiones de OpenXML a Transact-SQL.  
  
 Dado que los detalles de la secuencia deben interpretarse por el proveedor, debe especificar el lenguaje de comandos estableciendo el **dialecto** propiedad. El valor de **dialecto** es una cadena que contiene un GUID, que es definido por el proveedor. Para obtener información acerca de los valores válidos para **dialecto** compatible con el proveedor, consulte la documentación del proveedor.  
  
## <a name="xml-template-query-example"></a>Ejemplo de consulta de plantilla XML  
 En el siguiente ejemplo se escribe en VBScript en la base de datos Northwind.  
  
 En primer lugar, inicializar y abrir el **flujo** objeto que se usará para contener la secuencia de consulta:  
  
```  
Dim adoStreamQuery  
Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
adoStreamQuery.Open  
```  
  
 El contenido de la secuencia de la consulta será una consulta de la plantilla XML.  
  
 La consulta de plantilla requiere una referencia al espacio de nombres XML identificado por la instrucción sql: prefijo de la \<SQL: > etiqueta. Una instrucción SELECT de SQL se incluye como el contenido de la plantilla XML y se asigna a una variable de cadena, como se indica a continuación:  
  
```  
sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME </sql:query>  
</ROOT>"  
```  
  
 A continuación, escribir la cadena en la secuencia:  
  
```  
adoStreamQuery.WriteText sQuery, adWriteChar  
adoStreamQuery.Position = 0  
```  
  
 Asignar adoStreamQuery a la **CommandStream** propiedad de ADO **comando** objeto:  
  
```  
Dim adoCmd  
Set adoCmd  = Server.CreateObject("ADODB.Command"")  
adoCmd.CommandStream = adoStreamQuery  
```  
  
 Especificar el lenguaje de comandos **dialecto**, lo que indica cómo el proveedor OLE DB de SQL Server debe interpretar la secuencia de comandos. El dialecto especificado por un GUID específico del proveedor:  
  
```  
adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
```  
  
 Por último, ejecutar la consulta y devolver los resultados a un **Recordset** objeto:  
  
```  
Set objRS = adoCmd.Execute  
```


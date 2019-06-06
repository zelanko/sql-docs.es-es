---
title: Secuencias de comandos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- command streams [ADO]
- streams [ADO], command
ms.assetid: 0ac09dbe-2665-411e-8fbb-d1efe6c777be
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9d1322d872d5e05de4c7f142804fe2f1390b9859
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700882"
---
# <a name="command-streams"></a>Secuencias de comandos
ADO siempre ha admitido la entrada del comando en el formato de cadena especificado por el **CommandText** propiedad. Como alternativa, con ADO 2.7 o posterior, también puede usar una secuencia de información para la entrada de comando mediante la asignación de la secuencia de la **CommandStream** propiedad. Puede asignar un ADO **Stream** objeto, o cualquier objeto que admite el COM **IStream** interfaz.  
  
 El contenido de la secuencia de comandos se pasa simplemente de ADO a su proveedor, por lo que el proveedor debe admitir la entrada de comando de secuencia para esta característica funcione. Por ejemplo, SQL Server admite las consultas en forma de plantillas XML o OpenXML extensiones a Transact-SQL.  
  
 Dado que los detalles de la secuencia deben interpretarse el proveedor, debe especificar el dialecto del comando estableciendo el **dialecto** propiedad. El valor de **dialecto** es una cadena que contiene un GUID, que se define por el proveedor. Para obtener información acerca de los valores válidos para **dialecto** admitida por el proveedor, consulte la documentación del proveedor.  
  
## <a name="xml-template-query-example"></a>Ejemplo de consulta de plantilla XML  
 En el ejemplo siguiente se escribe en VBScript en la base de datos Northwind.  
  
 En primer lugar, inicializar y abrir el **Stream** objeto que se usará para contener la secuencia de la consulta:  
  
```  
Dim adoStreamQuery  
Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
adoStreamQuery.Open  
```  
  
 El contenido de la secuencia de la consulta será una consulta de la plantilla XML.  
  
 La consulta de la plantilla requiere una referencia al espacio de nombres XML identificado por la instrucción sql: prefijo de la \<SQL: > etiqueta. Una instrucción SELECT de SQL se incluye como el contenido de la plantilla XML y asigna a una variable de cadena del siguiente modo:  
  
```  
sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME </sql:query>  
</ROOT>"  
```  
  
 A continuación, escriba la cadena en la secuencia:  
  
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
  
 Por último, ejecute la consulta y devolver los resultados a un **Recordset** objeto:  
  
```  
Set objRS = adoCmd.Execute  
```

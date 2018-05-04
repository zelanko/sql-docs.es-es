---
title: Más información acerca de la persistencia de Recordset | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: a9b287f5-04b0-4514-8143-f67879ca9842
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a5c0d8bda0d3d881dfcb1dfd99706b28e5fb733
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="more-about-recordset-persistence"></a>Más información acerca de la persistencia de conjunto de registros
El objeto de conjunto de registros ADO admite almacenar el contenido de un **Recordset** objeto en un archivo mediante su [guardar](../../../ado/reference/ado-api/save-method.md) método. El archivo almacenado persistentemente exista en una variable local de unidad, server, o como una dirección URL en un servidor Web del sitio. Más adelante, se puede restaurar el archivo con cualquiera el [abiertos](../../../ado/reference/ado-api/open-method-ado-recordset.md) método de la **Recordset** objeto o la [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) método de la [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
 Además, el [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) método convierte un **Recordset** objeto a un formulario en el que las columnas y filas se delimitan con los caracteres especificados.  
  
 Para conservar un **Recordset**, conviértalo primero a un formulario que se pueden almacenar en un archivo. **Conjunto de registros** objetos pueden almacenarse en el formato de datos ADTG (Advanced TableGram) propietario o el formato de lenguaje de marcado Extensible (XML) abierto. En la sección siguiente se muestran ejemplos ADTG. Para obtener más información acerca de la persistencia de XML, vea [almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).  
  
 Guarde los cambios pendientes en el archivo persistente. Esto le permite emitir una consulta que devuelve un **Recordset** (objeto), ediciones el **conjunto de registros**, guarda junto con los cambios pendientes, restaure posteriormente el **conjunto de registros**y, a continuación, actualiza el origen de datos con el guardado los cambios pendientes.  
  
 Para obtener información acerca del almacenamiento persistente **flujo** los objetos, vea [secuencias y persistencia](../../../ado/guide/data/streams-and-persistence.md).  
  
 Para obtener un ejemplo de **Recordset** persistencia, consulte el escenario de persistencia del conjunto de registros de XML.  
  
## <a name="example"></a>Ejemplo  
  
### <a name="save-a-recordset"></a>Guardar un conjunto de registros:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Save "c:\yourFile.adtg", adPersistADTG  
```  
  
### <a name="open-a-persisted-file-with-recordsetopen"></a>Abrir un archivo almacenado con Recordset.Open:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg", "Provider=MSPersist",,,adCmdFile  
```  
  
 Opcionalmente, si la **Recordset** does no tiene una conexión activa, puede aceptar todos los valores predeterminados y cree el siguiente código:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg"  
```  
  
### <a name="open-a-persisted-file-with-connectionexecute"></a>Abrir un archivo almacenado con Connection.Execute:  
  
```  
Dim conn as New ADODB.Connection  
Dim rs as ADODB.Recordset  
conn.Open "Provider=MSPersist"  
Set rs = conn.execute("c:\yourFile.adtg")  
```  
  
### <a name="open-a-persisted-file-with-rdsdatacontrol"></a>Abrir un archivo almacenado con RDS. DataControl:  
 En este caso, el **Server** no tiene ningún valor.  
  
```  
Dim dc as New RDS.DataControl  
dc.Connection = "Provider=MSPersist"  
dc.SQL = "c:\yourFile.adtg"  
dc.Refresh  
```  
  
## <a name="see-also"></a>Vea también  
 [GetString (método) (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)   
 [Proveedor de persistencia de Microsoft OLE DB (proveedor de servicios ADO)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Secuencias y persistencia](../../../ado/guide/data/streams-and-persistence.md)

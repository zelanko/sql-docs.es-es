---
title: Más información acerca de la persistencia de conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: a9b287f5-04b0-4514-8143-f67879ca9842
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 88fcf471b2f853a5e1a874c29d2192c17d23b113
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701943"
---
# <a name="more-about-recordset-persistence"></a>Más información acerca de la persistencia de conjunto de registros
El objeto de conjunto de registros ADO admite almacenar el contenido de un **Recordset** objeto en un archivo mediante el uso de su [guardar](../../../ado/reference/ado-api/save-method.md) método. El archivo de forma persistente almacenado existan en una variable local de unidad, servidor, o como una dirección URL en un servidor Web de sitio. Más adelante, se puede restaurar el archivo con cualquiera el [abierto](../../../ado/reference/ado-api/open-method-ado-recordset.md) método de la **Recordset** objeto o la [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) método de la [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
 Además, el [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) método convierte un **Recordset** objeto a un formulario en el que las columnas y filas se delimitan con los caracteres especificados.  
  
 Para conservar un **Recordset**, conviértalo primero a un formulario que se puede almacenar en un archivo. **Conjunto de registros** objetos se pueden almacenar en el formato Advanced Data TableGram (ADTG) propietario o el formato abierto de Extensible Markup Language (XML). En la sección siguiente se muestran ejemplos ADTG. Para obtener más información acerca de la persistencia de XML, vea [almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).  
  
 Guardar los cambios pendientes en el archivo almacenado. Esto permite emitir una consulta que devuelve un **Recordset** (objeto), las modificaciones la **Recordset**, guarda y los cambios pendientes, más adelante restaura el **Recordset**y, a continuación, actualiza el origen de datos con el guardado los cambios pendientes.  
  
 Para obtener información acerca del almacenamiento persistente **Stream** objetos, vea [secuencias y persistencia](../../../ado/guide/data/streams-and-persistence.md).  
  
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
  
 Opcionalmente, si la **Recordset** does no tiene una conexión activa, puede aceptar todos los valores predeterminados y el siguiente código:  
  
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
  
### <a name="open-a-persisted-file-with-rdsdatacontrol"></a>Abrir un archivo almacenado con RDS. Control de datos:  
 En este caso, el **Server** no se establece la propiedad.  
  
```  
Dim dc as New RDS.DataControl  
dc.Connection = "Provider=MSPersist"  
dc.SQL = "c:\yourFile.adtg"  
dc.Refresh  
```  
  
## <a name="see-also"></a>Vea también  
 [GetString (método) (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)   
 [Proveedor de persistencia OLE DB de Microsoft (proveedor de servicios de ADO)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Secuencias y persistencia](../../../ado/guide/data/streams-and-persistence.md)

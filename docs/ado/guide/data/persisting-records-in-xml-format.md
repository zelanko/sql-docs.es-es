---
title: Almacenar registros en formato XML | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
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
- XML persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: f3113ec4-ae31-428f-89c6-bc1024f128ea
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 64041d559dcc680cc72f44f082013c65ef738c27
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272434"
---
# <a name="persisting-records-in-xml-format"></a>Almacenar registros en formato XML
Al igual que con formato ADTG, **Recordset** persistencia en formato XML se implementa con el proveedor de persistencia de Microsoft OLE DB. Este proveedor genera un conjunto de filas de solo avance y solo lectura desde un archivo XML o una secuencia que contiene la información de esquema generada por ADO guardado. De forma similar, puede tardar un ADO **Recordset**, generar XML y guardarlo en un archivo o cualquier objeto que implementa el modelo COM **IStream** interfaz. (De hecho, un archivo es otro ejemplo de un objeto que admite **IStream**.) En las versiones 2.5 y versiones posteriores, ADO se basa en Microsoft XML Parser (MSXML) para cargar el XML en el **Recordset**; por lo tanto, MSXML se requiere.  
  
> [!NOTE]
>  Existen algunas limitaciones cuando se guarda jerárquica **conjuntos de registros** (formas de datos) en formato XML. No se puede guardar en XML si el jerárquica **Recordset** contiene las actualizaciones pendientes, y no se puede guardar un con parámetros jerárquicos **conjunto de registros**. Para obtener más información, consulte [conservar filtradas y conjuntos de registros jerárquicos](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md).  
  
 La manera más fácil para conservar datos en XML y cargarlo de nuevo del nuevo a través de ADO es con el **guardar** y **abiertos** métodos, respectivamente. El siguiente ejemplo de código ADO muestra cómo guardar los datos en el **títulos** tabla a un archivo que se denomina titles.sav.  
  
```  
Dim rs as new Recordset  
Dim rs2 as new Recordset  
Dim c as new Connection  
Dim s as new Stream  
  
' Query the Titles table.  
c.Open "provider=sqloledb;data source=MySQLServer;initial catalog=pubs;Integrated Security='SSPI'"  
rs.cursorlocation = adUseClient  
rs.Open "select * from titles", c, adOpenStatic  
  
' Save to the file in the XML format. Note that if you don't specify   
' adPersistXML, a binary format (ADTG) will be used by default.  
rs.Save "titles.sav", adPersistXML  
  
' Save the recordset into the ADO Stream object.  
rs.save s, adPersistXML  
rs.Close  
c.Close  
  
set rs = nothing  
  
' Reopen the file.  
rs.Open "titles.sav",,,,adCmdFile  
' Open the Stream back into a Recordset.  
rs2.open s  
```  
  
 ADO siempre conserva toda la **Recordset** objeto. Si desea conservar un subconjunto de filas de la **Recordset** objeto, utilice la **filtro** método para restringir las filas o cambie la cláusula de selección. Sin embargo, debe abrir una **Recordset** objeto con un cursor de cliente (**CursorLocation** = **adUseClient**) para usar el **filtrar** método para guardar un subconjunto de filas. Por ejemplo, para recuperar títulos que empiecen por la letra "b", puede aplicar un filtro a un formato de archivo **Recordset** objeto:  
  
```  
rs.Filter "title_id like 'B*'"  
rs.Save "btitles.sav", adPersistXML  
```  
  
 ADO siempre utiliza el conjunto de filas del motor de Cursor de cliente para generar un desplazable admite marcadores **Recordset** objeto encima de los datos de solo avance generados por el proveedor de persistencia.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Formato de persistencia de XML](../../../ado/guide/data/xml-persistence-format.md)  
  
-   [Espacios de nombres](../../../ado/guide/data/namespaces.md)  
  
-   [Sección de esquema](../../../ado/guide/data/schema-section.md)  
  
-   [Sección de datos](../../../ado/guide/data/data-section.md)  
  
-   [Conjuntos de registros jerárquicos en XML](../../../ado/guide/data/hierarchical-recordsets-in-xml.md)  
  
-   [Propiedades del conjunto de registros dinámicos en XML](../../../ado/guide/data/recordset-dynamic-properties-in-xml.md)  
  
-   [Transformaciones XSLT](../../../ado/guide/data/xslt-transformations.md)  
  
-   [Guardar datos en el objeto de DOM de XML](../../../ado/guide/data/saving-to-the-xml-dom-object.md)  
  
-   [Consideraciones de seguridad XML](../../../ado/guide/data/xml-security-considerations.md)  
  
-   [Escenario de persistencia del conjunto de registros XML](../../../ado/guide/data/xml-recordset-persistence-scenario.md)

---
title: Formato de persistencia XML | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- XML persistence [ADO], persistence format
ms.assetid: 6e146738-ac4d-47bb-b6cd-d87b2260aead
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e477478ca6f5ef416086fc9ae1b91c8c2e5cf124
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="xml-persistence-format"></a>Formato de persistencia de XML
ADO utiliza la codificación UTF-8 para la secuencia XML que se conserva.  
  
 El formato XML de ADO se divide en dos secciones, una sección de esquema seguida de la sección de datos. El siguiente es un archivo XML de ejemplo para la tabla Shippers de la base de datos Northwind. Distintas partes del código XML se analizan el ejemplo siguiente.  
  
## <a name="remarks"></a>Comentarios  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"   
xmlns:dt="uuid:C2F41010-65B3-11d1-A29F-00AA00C14882"   
xmlns:rs="urn:schemas-microsoft-com:rowset"   
xmlns:z="#RowsetSchema">   
  <s:Schema id="RowsetSchema">   
    <s:ElementType name="row" content="eltOnly" rs:updatable="true">   
      <s:AttributeType name="ShipperID" rs:number="1"   
        rs:basetable="shippers" rs:basecolumn="ShipperID"  
        rs:keycolumn="true">   
        <s:datatype dt:type="int" dt:maxLength="4" rs:precision="10"   
          rs:fixedlength="true" rs:maybenull="false"/>   
      </s:AttributeType>   
      <s:AttributeType name="CompanyName" rs:number="2"   
        rs:nullable="true" rs:write="true" rs:basetable="shippers"   
        rs:basecolumn="CompanyName">   
        <s:datatype dt:type="string" dt:maxLength="40" />   
      </s:AttributeType>   
      <s:AttributeType name="Phone" rs:number="3" rs:nullable="true"   
        rs:write="true" rs:basetable="shippers"   
        rs:basecolumn="Phone">   
        <s:datatype dt:type="string" dt:maxLength="24"/>   
      </s:AttributeType>   
      <s:extends type="rs:rowbase"/>   
    </s:ElementType>   
  </s:Schema>   
  
  <rs:data>   
    <z:row ShipperID="1" CompanyName="Speedy Express"   
      Phone="(503) 555-9831"/>   
    <z:row ShipperID="2" CompanyName="United Package"   
      Phone="(503) 555-3199"/>   
    <z:row ShipperID="3" CompanyName="Federal Shipping"   
      Phone="(503) 555-9931"/>   
  </rs:data>   
</xml>  
```  
  
 El esquema muestra las declaraciones de espacios de nombres, la sección de esquema y la sección de datos. La sección de esquema contiene definiciones para fila, ShipperID, CompanyName y Phone.  
  
 Definiciones de esquema se ajustan a la [especificación de datos XML de W3C](http://www.w3.org/TR/1998/NOTE-XML-data/) y se pueden validar totalmente (aunque la validación no se producirá en Internet Explorer 5). XML-Data es actualmente el formato de esquemas admitidas solo para la persistencia de conjunto de registros.  
  
 La sección de datos tiene tres filas que contienen información acerca de expedidores. Para un conjunto de filas vacío, la sección de datos puede estar vacía, pero la \<rs: data > etiquetas deben estar presentes. Sin datos, podría escribir la etiqueta de forma abreviada como simplemente \<rs: data / >. Cualquier etiqueta el prefijo "rs" indica que se encuentra en el espacio de nombres definido por urn: schemas-microsoft-Rowset.  
  
## <a name="see-also"></a>Vea también  
 [Almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)

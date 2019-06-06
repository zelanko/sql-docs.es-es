---
title: Formato de persistencia XML | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML persistence [ADO], persistence format
ms.assetid: 6e146738-ac4d-47bb-b6cd-d87b2260aead
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 49a3c276aa17d8f2bd7f48296eeecb69ad91d04d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718368"
---
# <a name="xml-persistence-format"></a>Formato de persistencia de XML
ADO utiliza la codificación UTF-8 para la secuencia XML que almacena.  
  
 El formato XML de ADO se divide en dos secciones, una sección de esquema seguida de la sección de datos. El siguiente es un archivo XML de ejemplo para la tabla Shippers de la base de datos Northwind. Se tratan distintas partes del código XML del ejemplo siguiente.  
  
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
  
 El esquema muestra las declaraciones de espacios de nombres, la sección de esquema y la sección de datos. La sección de esquema contiene definiciones de fila, ShipperID, CompanyName y teléfono.  
  
 Definiciones de esquema se ajustan a la [especificación W3C XML-Data](http://www.w3.org/TR/1998/NOTE-XML-data/) y se pueden validar totalmente (aunque no se producirá la validación en Internet Explorer 5). Datos XML está actualmente en el formato de esquema admitidas solo para la persistencia de conjunto de registros.  
  
 La sección de datos tiene tres filas que contienen información acerca de distribuidores. Para un conjunto de filas vacío, la sección de datos puede estar vacía, pero la \<rs: data > etiquetas deben estar presentes. Sin datos, podría escribir la etiqueta de forma abreviada como simplemente \<rs: data / >. Cualquier etiqueta el prefijo "rs" indica que está en el espacio de nombres definido por el urn: schemas-microsoft-Rowset.  
  
## <a name="see-also"></a>Vea también  
 [Almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)

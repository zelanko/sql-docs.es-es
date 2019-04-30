---
title: Conjuntos de registros jerárquicos en XML | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO], in XML
ms.assetid: 5d4b11c4-c94f-4910-b99b-5b9abc50d791
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 860732a8d694ee59dae05f76eb9cabe49ebc8c96
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161572"
---
# <a name="hierarchical-recordsets-in-xml"></a>Conjuntos de registros jerárquicos en XML
ADO permite la persistencia de los objetos de conjunto de registros jerárquicos en XML. Con objetos de conjunto de registros jerárquicos, el valor de un campo en el conjunto de registros principal es otro conjunto de registros. Estos campos se representan como elementos secundarios en la secuencia XML en lugar de un atributo.  
  
## <a name="remarks"></a>Comentarios  
 El ejemplo siguiente muestra este caso:  
  
```  
Rs.Open "SHAPE {select stor_id, stor_name, state from stores} APPEND ({select stor_id, ord_num, ord_date, qty from sales} AS rsSales RELATE stor_id TO stor_id)", "Provider=MSDataShape;DSN=pubs;Integrated Security=SSPI;"  
```  
  
 Este es el formato XML del conjunto de registros persistentes:  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"     xmlns:dt="uuid:C2F41010-65B3-11d1-A29F-00AA00C14882"     xmlns:rs="urn:schemas-microsoft-com:rowset"   
    xmlns:z="#RowsetSchema">   
  <s:Schema id="RowsetSchema">   
    <s:ElementType name="row" content="eltOnly" rs:updatable="true">   
      <s:AttributeType name="stor_id" rs:number="1"   
        rs:writeunknown="true">   
        <s:datatype dt:type="string" dt:maxLength="4"   
          rs:fixedlength="true" rs:maybenull="false"/>   
      </s:AttributeType>   
      <s:AttributeType name="stor_name" rs:number="2" rs:nullable="true"   
        rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="40"/>   
      </s:AttributeType>   
      <s:AttributeType name="state" rs:number="3" rs:nullable="true"   
        rs:writeunknown="true">   
        <s:datatype dt:type="string" dt:maxLength="2"   
          rs:fixedlength="true"/>   
      </s:AttributeType>   
      <s:ElementType name="rsSales" content="eltOnly"   
        rs:updatable="true" rs:relation="010000000100000000000000">   
        <s:AttributeType name="stor_id" rs:number="1"   
          rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="4"   
            rs:fixedlength="true" rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="ord_num" rs:number="2"   
          rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="20"   
            rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="ord_date" rs:number="3"   
          rs:writeunknown="true">   
            <s:datatype dt:type="dateTime" dt:maxLength="16"   
              rs:scale="3" rs:precision="23" rs:fixedlength="true"   
              rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="qty" rs:number="4" rs:writeunknown="true">   
          <s:datatype dt:type="i2" dt:maxLength="2" rs:precision="5"   
            rs:fixedlength="true" rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:extends type="rs:rowbase"/>   
      </s:ElementType>   
      <s:extends type="rs:rowbase"/>   
    </s:ElementType>   
  </s:Schema>   
  <rs:data>   
    <z:row stor_id="6380" stor_name="Eric the Read Books" state="WA">   
      <rsSales stor_id="6380" ord_num="6871"   
        ord_date="1994-09-14T00:00:00" qty="5"/>   
      <rsSales stor_id="6380" ord_num="722a"   
        ord_date="1994-09-13T00:00:00" qty="3"/>   
    </z:row>   
    <z:row stor_id="7066" stor_name="Barnum's" state="CA">   
      <rsSales stor_id="7066" ord_num="A2976"   
        ord_date="1993-05-24T00:00:00" qty="50"/>   
      <rsSales stor_id="7066" ord_num="QA7442.3"   
        ord_date="1994-09-13T00:00:00" qty="75"/>   
    </z:row>   
    <z:row stor_id="7067" stor_name="News & Brews" state="CA">   
      <rsSales stor_id="7067" ord_num="D4482"   
        ord_date="1994-09-14T00:00:00" qty="10"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="40"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="20"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="20"/>   
    </z:row>   
  </rs:data>   
</xml>   
```  
  
 El orden exacto de las columnas de conjunto de registros principal no es evidente cuando se conserva de esta manera. Cualquier campo en el elemento primario puede contener a un conjunto de registros secundarios. El proveedor de persistencia conserva todas las columnas escalares como atributos y luego todas las "columnas" Recordset secundarias como elementos secundarios de la fila primaria. La posición ordinal del campo en el elemento primario puede obtenerse Recordset echando un vistazo a la definición de esquema del conjunto de registros. Cada campo tiene una propiedad de OLE DB, rs: number, definida en el espacio de nombres del esquema de conjunto de registros que contiene el número ordinal para ese campo.  
  
 Los nombres de todos los campos del conjunto de registros secundario se concatenan con el nombre del campo en el conjunto de registros que contiene a este elemento secundario del primario. Esto es para asegurarse de que no hay ninguna colisión de nombre en casos donde primarios y secundarios de conjuntos de registros de ambas contienen un campo que se obtiene de dos tablas diferentes pero con nombre singular.  
  
 Al guardar los conjuntos de registros jerárquicos en XML, debe tener en cuenta las restricciones siguientes en ADO:  
  
-   No se pueden conservar un conjunto de registros jerárquico con actualizaciones pendientes en XML.  
  
-   Un conjunto de registros jerárquico creado con un comando de forma con parámetros no puede conservarse (en formato XML o ADTG).  
  
-   Actualmente, ADO guarda la relación entre el elemento primario y secundario conjuntos de registros como un objeto binario grande (BLOB). Etiquetas XML para describir esta relación aún no se han definido en el espacio de nombres del esquema de conjunto de filas.  
  
-   Cuando se guarda un conjunto de registros jerárquico, secundarios de todos los conjuntos de registros se guardan con él. Si el conjunto de registros actual es un elemento secundario de otro conjunto de registros, no se guarda su elemento primario. Todos los secundarios se guardan los conjuntos de registros que componen el subárbol del conjunto de registros actual.  
  
 Cuando un conjunto de registros jerárquico se vuelve a abrir desde su formato XML persistente, debe tener en cuenta las siguientes limitaciones:  
  
-   Si el registro secundario contiene registros para el que no hay ningún registro primario correspondiente, estas filas no se escriben en la representación XML del conjunto de registros jerárquicos. Por lo tanto, estas filas se perderán cuando se vuelve a abrir el conjunto de registros desde su ubicación persistente.  
  
-   Si un registro secundario tiene referencias a más de un registro primario, en el conjunto de registros, volver a abrir el conjunto de registros secundarios pueden contener los registros duplicados. Sin embargo, estos duplicados solo será visibles si el usuario trabaja directamente con el conjunto de filas secundario subyacente. Si un capítulo se usa para navegar por el elemento secundario de conjunto de registros (es decir, la única forma de navegar a través de ADO), los duplicados no son visibles.  
  
## <a name="see-also"></a>Vea también  
 [Almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)

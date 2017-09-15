---
title: "Conjuntos de registros jerárquicos en XML | Documentos de Microsoft"
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
- hierarchical Recordsets [ADO], in XML
ms.assetid: 5d4b11c4-c94f-4910-b99b-5b9abc50d791
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c5d4a03801d4f126185ba63fe3fb6409947219bf
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="hierarchical-recordsets-in-xml"></a>Conjuntos de registros jerárquicos en XML
ADO permite la persistencia de los objetos de conjunto de registros jerárquicos en XML. Con objetos de conjunto de registros jerárquicos, el valor de un campo en el conjunto de registros principal es otro conjunto de registros. Estos campos se representan como elementos secundarios en la secuencia XML en lugar de un atributo.  
  
## <a name="remarks"></a>Comentarios  
 En el ejemplo siguiente se muestra este caso:  
  
```  
Rs.Open "SHAPE {select stor_id, stor_name, state from stores} APPEND ({select stor_id, ord_num, ord_date, qty from sales} AS rsSales RELATE stor_id TO stor_id)", "Provider=MSDataShape;DSN=pubs;Integrated Security=SSPI;"  
```  
  
 Éste es el formato XML del conjunto de registros persistente:  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"     xmlns:dt="uuid:C2F41010-65B3-11d1-A29F-00AA00C14882"     xmlns:rs="urn:schemas-microsoft-com:rowset"   
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
  
 El orden exacto de las columnas en el conjunto de registros principal no es obvio cuando se conservan de esta manera. Cualquier campo en el elemento primario puede contener a un conjunto de registros secundarios. El proveedor de persistencia conserva todas las columnas escalares como atributos y luego todas las "columnas" Recordset secundarias como elementos secundarios de la fila primaria. La posición ordinal del campo primario en el conjunto de registros puede obtenerse consultando la definición de esquema del conjunto de registros. Cada campo tiene una propiedad de OLE DB, rs: number, definida en el espacio de nombres de esquema de conjunto de registros que contiene el número ordinal para ese campo.  
  
 Los nombres de todos los campos en el conjunto de registros secundario se concatenan con el nombre del campo en el conjunto de registros que contiene a este elemento secundario del primario. Esto sirve para asegurarse de que no hay ningún colisiones de nombres en casos donde Recordset tanto primarios y secundarios contienen un campo que se obtiene de dos tablas diferentes pero con nombre singular.  
  
 Al guardar los conjuntos de registros jerárquicos en XML, debe tener en cuenta las restricciones siguientes en ADO:  
  
-   Un objeto Recordset jerárquico con actualizaciones pendientes no se puede guardar en XML.  
  
-   Un conjunto de registros jerárquico creado con un comando shape parametrizado no puede persistir (en formato XML o ADTG).  
  
-   Actualmente, ADO guarda la relación entre el elemento primario y el elemento secundario de conjuntos de registros como un objeto binario grande (BLOB). Etiquetas XML para describir esta relación no se ha definido todavía en el espacio de nombres de esquema de conjunto de filas.  
  
-   Cuando se guarda un conjunto de registros jerárquico, todos los secundarios conjuntos de registros se guardan con él. Si el conjunto de registros actual es un elemento secundario de otro conjunto de registros, no se guarda su elemento primario. Todos los secundarios se guardan los conjuntos de registros que componen el subárbol del conjunto de registros actual.  
  
 Cuando un conjunto de registros jerárquico se vuelve a abrir desde su formato XML persistente, debe tener en cuenta las siguientes limitaciones:  
  
-   Si el registro secundario contiene registros para los que no hay ningún registro primario correspondiente, estas filas no se escriben en la representación XML del conjunto de registros jerárquico. Por lo tanto, estas filas se perderán cuando se vuelva a abrir el conjunto de registros desde su ubicación persistente.  
  
-   Si un registro secundario tiene referencias a más de un registro primario, en el conjunto de registros, volver a abrir el conjunto de registros secundario puede contener registros duplicados. Sin embargo, estos duplicados sólo estará visibles si el usuario trabaja directamente con el conjunto de filas secundario subyacente. Si se utiliza un capítulo para desplazarse por el conjunto de registros (es decir, la única manera de navegar a través de ADO) secundario, los duplicados no estarán visibles.  
  
## <a name="see-also"></a>Vea también  
 [Almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)

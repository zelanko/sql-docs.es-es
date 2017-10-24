---
title: "Sección de datos | Documentos de Microsoft"
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
- data section [ADO]
ms.assetid: 43dc42a8-7057-48e6-93d6-880d5c5c51a4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 62eb026fac4588cc159afec1714a6aa51903aa8a
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="data-section"></a>Sección de datos
La sección de datos define los datos del conjunto de filas junto con los pendientes las actualizaciones, inserciones o eliminaciones. La sección de datos puede contener cero o más filas. Solo puede contener datos de un conjunto de filas donde la fila se define el esquema. Además, como se indicó antes, se pueden omitir columnas sin ningún dato. Si se utiliza un atributo o un subelemento en la sección de datos y esa construcción no se ha definido en la sección de esquema, se omite en modo silencioso.  
  
## <a name="string"></a>String  
 Los caracteres XML reservados en datos de texto se deben reemplazar por entidades de caracteres apropiado. Por ejemplo, en el nombre de la compañía "Artículos de Juan", una comilla simple debe sustituirse por una entidad. La fila real podría parecerse a lo siguiente:  
  
```  
<z:row CompanyName="Joe's Garage"/>  
```  
  
 Los caracteres siguientes están reservados en XML y se deben reemplazar por entidades de carácter: {', "&,\<, >}.  
  
## <a name="binary"></a>Binario  
 Datos binarios son tienen codificada bin.hex (es decir, un byte se asigna a dos caracteres, un carácter por cada medio byte).  
  
## <a name="datetime"></a>DateTime  
 Tipos de datos de datos XML no admite directamente el formato VT_DATE variant. El formato correcto para las fechas con componente de fecha y de hora es aaaa-mm-ddThh.  
  
 Para obtener más información acerca de los formatos de fecha especificados mediante XML, consulte el [especificación de datos XML de W3C](https://go.microsoft.com/fwlink/?LinkId=5692).  
  
 Cuando la especificación de datos XML define dos tipos de datos equivalentes (por ejemplo, i4 == int), ADO se escribe el nombre descriptivo pero lee ambos.  
  
## <a name="managing-pending-changes"></a>Administrar cambios pendientes  
 Se puede abrir un conjunto de registros de inmediato o en modo de actualización por lotes. Cuando se abren en modo de actualización por lotes con cursores de cliente, todos los cambios realizados en el conjunto de registros están en un estado pendiente hasta que se llama al método UpdateBatch. Los cambios pendientes también se conservan cuando se guarda el conjunto de registros. En XML, se representan mediante el uso de los elementos de "actualización" definidos en urn: schemas-microsoft-Rowset. Además, si se puede actualizar un conjunto de filas, la propiedad actualizable debe establecerse en true en la definición de la fila. Por ejemplo, para definir que la tabla Shippers contiene cambios pendientes, la definición de la fila podría parecerse apariencia siguiente.  
  
```  
<s:ElementType name="row" content="eltOnly" updatable="true">  
  <s:attribute type="ShipperID"/>  
  <s:attribute type="CompanyName"/>  
  <s:attribute type="Phone"/>  
  <s:extends type="rs:rowbase"/>  
</s:ElementType>  
```  
  
 Esto indica al proveedor de persistencia que muestre datos para que ADO puede construir un objeto de conjunto de registros actualizable.  
  
 Los datos de ejemplo siguiente muestran el aspecto de las inserciones, cambios y eliminaciones en el archivo persistente.  
  
```  
<rs:data>  
  <z:row ShipperID="2" CompanyName="United Package"   
    Phone="(503) 555-3199"/>  
<rs:update>  
  <rs:original>  
    <z:row ShipperID="3" CompanyName="Federal Shipping"   
      Phone="(503) 555-9931"/>  
  </rs:original>  
  <z:row Phone="(503) 552-7134"/>  
</rs:update>  
<rs:insert>  
  <z:row ShipperID="12" CompanyName="Lightning Shipping"   
    Phone="(505) 111-2222"/>  
  <z:row ShipperID="13" CompanyName="Thunder Overnight"   
    Phone="(505) 111-2222"/>  
  <z:row ShipperID="14" CompanyName="Blue Angel Air Delivery"   
    Phone="(505) 111-2222"/>  
</rs:insert>  
<rs:delete>  
  <z:row ShipperID="1" CompanyName="Speedy Express" Phone="(503) 555-9831"/>  
</rs:delete>  
</rs:data>  
```  
  
 Una actualización siempre contiene los datos de fila originales todo seguidos por los datos de la fila modificada. La fila modificada puede contener todas las columnas o solo las columnas que han cambiado realmente. En el ejemplo anterior, no se cambia la fila 2 de remitente, y solo la columna Phone ha cambiado el valor de 3 de remitente y, por tanto, es la única columna incluida en la fila modificada. Las filas insertadas para los transportistas 12, 13 y 14 son por lotes etiqueta rs: insert en una sola juntos. Tenga en cuenta que las filas eliminadas pueden también realizarse por lotes juntos, aunque esto no se muestra en el ejemplo anterior.  
  
## <a name="see-also"></a>Vea también  
 [Almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)


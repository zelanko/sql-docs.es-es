---
title: Sección de datos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data section [ADO]
ms.assetid: 43dc42a8-7057-48e6-93d6-880d5c5c51a4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 76cd14b8ee1c5a55e0312993090bfaf098c7e219
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702138"
---
# <a name="data-section"></a>Sección de datos
La sección de datos define los datos del conjunto de filas junto con el pendiente actualizaciones, inserciones o eliminaciones. La sección de datos puede contener cero o más filas. Solo puede contener datos de un conjunto de filas donde la fila se define el esquema. Además, como se indicó antes, se pueden omitir columnas sin datos. Si se utiliza un atributo o un subelemento en la sección de datos y esa construcción no se ha definido en la sección de esquema, se omite en modo silencioso.  
  
## <a name="string"></a>String  
 Los caracteres XML reservados en datos de texto deben reemplazarse por las entidades de caracteres apropiado. Por ejemplo, en el nombre de la empresa "De Joe garaje", una comilla simple debe sustituirse por una entidad. La fila real sería similar al siguiente:  
  
```  
<z:row CompanyName="Joe's Garage"/>  
```  
  
 Los caracteres siguientes están reservados en XML y debe reemplazarse por las entidades de caracteres: {"," &,\<, >}.  
  
## <a name="binary"></a>Binario  
 Datos binarios están bin.hex codificado (es decir, un byte se asigna a dos caracteres, un carácter por nibble).  
  
## <a name="datetime"></a>DateTime  
 El formato VT_DATE variant no es directamente compatible con tipos de datos XML. El formato correcto para las fechas con el componente de fecha y de hora es aaaa-mm-ddThh.  
  
 Para obtener más información acerca de los formatos de fecha especificados mediante XML, vea el [especificación W3C XML-Data](https://go.microsoft.com/fwlink/?LinkId=5692).  
  
 Cuando la especificación de datos XML define dos tipos de datos equivalentes (por ejemplo, i4 == int), ADO se escribe el nombre descriptivo pero lee ambos.  
  
## <a name="managing-pending-changes"></a>Administrar cambios pendientes  
 Se puede abrir un conjunto de registros de inmediato o modo de actualización por lotes. Cuando se abren en modo de actualización por lotes con cursores de cliente, todos los cambios realizados en el conjunto de registros están en un estado pendiente hasta que se llama al método UpdateBatch. Los cambios pendientes también se conservan cuando se guarda el conjunto de registros. En XML, se representan mediante el uso de los elementos de "actualización" definidos en urn: schemas-microsoft-Rowset. Además, si se puede actualizar un conjunto de filas, la propiedad actualizable debe establecerse en true en la definición de la fila. Por ejemplo, para definir que la tabla de distribuidores contiene cambios pendientes, la definición de fila podría parecerse Buscar siguiente.  
  
```  
<s:ElementType name="row" content="eltOnly" updatable="true">  
  <s:attribute type="ShipperID"/>  
  <s:attribute type="CompanyName"/>  
  <s:attribute type="Phone"/>  
  <s:extends type="rs:rowbase"/>  
</s:ElementType>  
```  
  
 Esto indica al proveedor de persistencia para los datos de superficie para que ADO puede construir un objeto de conjunto de registros actualizable.  
  
 Los datos de ejemplo siguiente muestran cómo buscar las inserciones, cambios y eliminaciones en el archivo almacenado.  
  
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
  
 Una actualización siempre contiene los datos de fila originales todo seguidos por los datos de la fila modificada. La fila modificada puede contener todas las columnas o solo aquellas columnas que han cambiado realmente. En el ejemplo anterior, no se cambia la fila 2 de remitente, y solo la columna Phone ha cambiado los valores para el remitente 3 y, por tanto, es la única columna que se incluyen en la fila modificada. Las filas insertadas para los transportistas 12, 13 y 14 son por lotes juntos en una sola rs: Insertar etiqueta. Tenga en cuenta que las filas eliminadas pueden también se pueden agrupar, aunque esto no se muestra en el ejemplo anterior.  
  
## <a name="see-also"></a>Vea también  
 [Almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)

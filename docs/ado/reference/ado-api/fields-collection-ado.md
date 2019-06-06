---
title: (ADO) de la colección de campos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Fields
- Recordset15::Fields
- _Record::Fields
helpviewer_keywords:
- Fields collection [ADO]
ms.assetid: 7c371474-b88f-4730-afa5-44163a0488d5
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8483a908e31b9e4554c5594ecc5bbf186bbef88f
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695034"
---
# <a name="fields-collection-ado"></a>Fields (colección) (ADO)
Contiene todos los [campo](../../../ado/reference/ado-api/field-object.md) objetos de un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) o [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto.  
  
## <a name="remarks"></a>Comentarios  
 Un **Recordset** objeto tiene un **campos** colección formada por **campo** objetos. Cada **campo** objeto corresponde a una columna de la **Recordset**. Puede rellenar el **campos** colección antes de abrir el **Recordset** mediante una llamada a la [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método en la colección.  
  
> [!NOTE]
>  Consulte la **campo** tema del objeto para obtener una explicación más detallada de cómo usar **campo** objetos.  
  
 El **campos** colección tiene un [Append](../../../ado/reference/ado-api/append-method-ado.md) método, que se crea y agrega provisionalmente una **campo** objeto a la colección y un **actualizar**método, que finaliza las adiciones o eliminaciones.  
  
 Un **registro** objeto tiene dos campos especiales que se pueden indexar con [FieldEnum](../../../ado/reference/ado-api/fieldenum.md) constantes. Una constante obtiene acceso a un campo que contiene la secuencia predeterminada para el **registro**, y el otro tiene acceso a un campo que contiene la cadena de dirección URL absoluta para el **registro**.  
  
 Ciertos proveedores (por ejemplo, el [proveedor Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)) puede rellenar el **campos** colección con un subconjunto de campos disponibles para el **registro** o **Recordset**. No se agregarán otros campos a la colección hasta que se hace referencia por nombre o se indizados por el código en primer lugar.  
  
 Si se intenta hacer referencia a un campo inexistente por nombre, un nuevo **campo** objeto se anexará a la **campos** colección con un [estado](../../../ado/reference/ado-api/status-property-ado-field.md) de  **adFieldPendingInsert**. Cuando se llama a [actualización](../../../ado/reference/ado-api/update-method.md), ADO creará un nuevo campo en el origen de datos si se permite el proveedor.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades de la colección de campos, métodos y eventos](../../../ado/reference/ado-api/fields-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)

---
title: Fields (colección) (ADO) | Documentos de Microsoft
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
apitype: COM
f1_keywords:
- Fields
- Recordset15::Fields
- _Record::Fields
helpviewer_keywords:
- Fields collection [ADO]
ms.assetid: 7c371474-b88f-4730-afa5-44163a0488d5
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4eebfb3b3e401585829446872545063448ec87d6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="fields-collection-ado"></a>Fields (colección) (ADO)
Contiene todos los [campo](../../../ado/reference/ado-api/field-object.md) objetos de un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) o [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto.  
  
## <a name="remarks"></a>Comentarios  
 A **Recordset** objeto tiene una **campos** colección formada por **campo** objetos. Cada **campo** objeto corresponde a una columna de la **conjunto de registros**. Puede rellenar el **campos** colección antes de abrir el **Recordset** mediante una llamada a la [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método en la colección.  
  
> [!NOTE]
>  Consulte la **campo** tema del objeto para obtener una explicación más detallada de cómo usar **campo** objetos.  
  
 El **campos** colección tiene un [anexado](../../../ado/reference/ado-api/append-method-ado.md) método, que provisionalmente, crea y agrega un **campo** objeto a la colección y un **actualizar**método, que finaliza las adiciones o eliminaciones.  
  
 A **registro** objetos tienen dos campos especiales que se pueden indizar con [FieldEnum](../../../ado/reference/ado-api/fieldenum.md) constantes. Una constante obtiene acceso a un campo que contiene la secuencia predeterminada para el **registro**, y el otro tiene acceso a un campo que contiene la cadena de dirección URL absoluta para el **registro**.  
  
 Ciertos proveedores (por ejemplo, el [proveedor Microsoft OLE DB para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)) puede rellenar el **campos** colección con un subconjunto de los campos disponibles para la **registro** o **conjunto de registros**. Otros campos no se agregarán a la colección hasta que hace referencia por nombre o por primera vez indizados por el código.  
  
 Si intenta hacer referencia a un campo inexistente por su nombre, un nuevo **campo** objeto se anexará a la **campos** colección con un [estado](../../../ado/reference/ado-api/status-property-ado-field.md) de  **adFieldPendingInsert**. Cuando se llama a [actualización](../../../ado/reference/ado-api/update-method.md), ADO creará un nuevo campo en el origen de datos si permitido por el proveedor.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades de la colección de campos, métodos y eventos](../../../ado/reference/ado-api/fields-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)

---
title: Colección Fields (ADO) | Microsoft Docs
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
ms.openlocfilehash: 9c9216ee655e371633837c5653ebac56fac1a782
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918712"
---
# <a name="fields-collection-ado"></a>Fields (colección) (ADO)
Contiene todos los objetos de [campo](../../../ado/reference/ado-api/field-object.md) de un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) o un objeto de [registro](../../../ado/reference/ado-api/record-object-ado.md) .  
  
## <a name="remarks"></a>Observaciones  
 Un objeto de **conjunto de registros** tiene una colección **Fields** formada por objetos **Field** . Cada objeto de **campo** corresponde a una columna del **conjunto de registros**. Puede rellenar la colección **Fields** antes de abrir el **conjunto de registros** llamando al método [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) de la colección.  
  
> [!NOTE]
>  Vea el tema objeto de **campo** para obtener una explicación más detallada de cómo usar los objetos de **campo** .  
  
 La colección **Fields** tiene un método [Append](../../../ado/reference/ado-api/append-method-ado.md) , que crea y agrega de forma aprovisionada un objeto **Field** a la colección, y un método **Update** , que finaliza cualquier adición o eliminación.  
  
 Un objeto **Record** tiene dos campos especiales que se pueden indizar con constantes [FieldEnum](../../../ado/reference/ado-api/fieldenum.md) . Una constante obtiene acceso a un campo que contiene la secuencia predeterminada del **registro**y el otro tiene acceso a un campo que contiene la cadena de dirección URL absoluta del **registro**.  
  
 Algunos proveedores (por ejemplo, el [proveedor de Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)) pueden rellenar la colección de **campos** con un subconjunto de campos disponibles para el **registro** o el **conjunto de registros**. No se agregarán otros campos a la colección hasta que se haga referencia a ellos por su nombre o se indexen por primera vez por su código.  
  
 Si intenta hacer referencia a un campo inexistente por su nombre, se anexará un nuevo objeto de **campo** a la colección **Fields** con el [Estado](../../../ado/reference/ado-api/status-property-ado-field.md) **adFieldPendingInsert**. Al llamar a [Update](../../../ado/reference/ado-api/update-method.md), ADO creará un nuevo campo en el origen de datos si lo permite el proveedor.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos de la colección Fields](../../../ado/reference/ado-api/fields-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)

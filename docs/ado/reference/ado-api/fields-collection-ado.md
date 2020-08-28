---
description: Fields (colección) (ADO)
title: Colección Fields (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6f16fd27e7bee9d3f9e922de4db625b897266a61
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973126"
---
# <a name="fields-collection-ado"></a>Fields (colección) (ADO)
Contiene todos los objetos de [campo](./field-object.md) de un [conjunto de registros](./recordset-object-ado.md) o un objeto de [registro](./record-object-ado.md) .  
  
## <a name="remarks"></a>Observaciones  
 Un objeto de **conjunto de registros** tiene una colección **Fields** formada por objetos **Field** . Cada objeto de **campo** corresponde a una columna del **conjunto de registros**. Puede rellenar la colección **Fields** antes de abrir el **conjunto de registros** llamando al método [Refresh](./refresh-method-ado.md) de la colección.  
  
> [!NOTE]
>  Vea el tema objeto de **campo** para obtener una explicación más detallada de cómo usar los objetos de **campo** .  
  
 La colección **Fields** tiene un método [Append](./append-method-ado.md) , que crea y agrega de forma aprovisionada un objeto **Field** a la colección, y un método **Update** , que finaliza cualquier adición o eliminación.  
  
 Un objeto **Record** tiene dos campos especiales que se pueden indizar con constantes [FieldEnum](./fieldenum.md) . Una constante obtiene acceso a un campo que contiene la secuencia predeterminada del **registro**y el otro tiene acceso a un campo que contiene la cadena de dirección URL absoluta del **registro**.  
  
 Algunos proveedores (por ejemplo, el [proveedor de Microsoft OLE DB para la publicación en Internet](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)) pueden rellenar la colección de **campos** con un subconjunto de campos disponibles para el **registro** o el **conjunto de registros**. No se agregarán otros campos a la colección hasta que se haga referencia a ellos por su nombre o se indexen por primera vez por su código.  
  
 Si intenta hacer referencia a un campo inexistente por su nombre, se anexará un nuevo objeto de **campo** a la colección **Fields** con el [Estado](./status-property-ado-field.md) **adFieldPendingInsert**. Al llamar a [Update](./update-method.md), ADO creará un nuevo campo en el origen de datos si lo permite el proveedor.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos de la colección Fields](./fields-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Objeto Field](./field-object.md)
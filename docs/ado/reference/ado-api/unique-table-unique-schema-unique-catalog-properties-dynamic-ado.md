---
description: 'Tabla única, esquema único, propiedades de catálogo únicas: dinámica (ADO)'
title: Controlar los cambios en la tabla base del conjunto de registros (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Unique Table property [ADO]
- Unique Schema property [ADO]
- Unique Catalog property [ADO]
ms.assetid: d0e775d8-e353-46a1-ad10-ed4cc240dfaa
author: rothja
ms.author: jroth
ms.openlocfilehash: 2bd5979526e453e33674441ebd4e433f2a7ad6f3
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777044"
---
# <a name="unique-table-unique-schema-unique-catalog-properties-dynamic-ado"></a>Tabla única, esquema único, propiedades de catálogo únicas: dinámica (ADO)
Permite controlar estrechamente las modificaciones realizadas en una tabla base determinada de un [conjunto de registros](./recordset-object-ado.md) que formaba parte de una operación de combinación en varias tablas base.  
  
-   **Tabla única** especifica el nombre de la tabla base en la que se permiten las actualizaciones, las inserciones y las eliminaciones.  
  
-   **Unique Schema** especifica el *esquema*o el nombre del propietario de la tabla.  
  
-   **Catálogo único** especifica el *Catálogo*o el nombre de la base de datos que contiene la tabla.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor de **cadena** que es el nombre de una tabla, un esquema o un catálogo.  
  
## <a name="remarks"></a>Observaciones  
 La tabla base deseada se identifica de forma única mediante el catálogo, el esquema y los nombres de tabla. Cuando se establece la propiedad de **tabla única** , se usan los valores de las propiedades **Unique Schema** o Unique **Catalog** para buscar la tabla base. Está previsto, pero no es necesario, que el **esquema único** y las propiedades del **catálogo único** se establezcan antes de que se establezca la propiedad de **tabla única** .  
  
 La clave principal de la **tabla única** se trata como la clave principal del conjunto de **registros**completo. Esta es la clave que se usa para cualquier método que requiera una clave principal.  
  
 Mientras se establece la **tabla única** , el método de [eliminación](./delete-method-ado-recordset.md) solo afecta a la tabla con nombre. Los métodos [AddNew](./addnew-method-ado.md), [Resync](./resync-method.md), [Update](./update-method.md)y [UpdateBatch](./updatebatch-method.md) afectan a las tablas base subyacentes adecuadas del **conjunto de registros**.  
  
 Se debe especificar una **tabla única** antes de realizar cualquier resincronización personalizada. Si no se ha especificado una **tabla única** , la propiedad del [comando Resync](./resync-command-property-dynamic-ado.md) no tendrá ningún efecto.  
  
 Si no se encuentra una tabla base única, se produce un error en tiempo de ejecución.  
  
 Todas estas propiedades dinámicas se anexan a la colección de [propiedades](./properties-collection-ado.md) del objeto de **conjunto de registros** cuando la propiedad [CursorLocation](./cursorlocation-property-ado.md) está establecida en **adUseClient**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Objeto de conjunto de registros (ADO)](./recordset-object-ado.md)
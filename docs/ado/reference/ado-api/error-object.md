---
title: Objeto de error | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error
helpviewer_keywords:
- error object [ADO]
ms.assetid: a175d453-fa55-4f49-9ede-a26d83177919
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: bc9dc5f19dacfb6fbdab8c2e0dd8278cbc4b97b3
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719276"
---
# <a name="error-object"></a>Objeto de error
Contiene detalles sobre los errores de acceso de datos que pertenecen a una única operación que implica al proveedor.  
  
## <a name="remarks"></a>Comentarios  
 Cualquier operación que implica objetos ADO puede generar uno o varios errores del proveedor. Cuando se produce cada error, uno o varios **Error** objetos se colocan en el [errores](../../../ado/reference/ado-api/errors-collection-ado.md) colección de la [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto. Cuando otra operación ADO genera un error, el **errores** se borra la colección y el nuevo conjunto de **Error** objetos se coloca en el **errores** colección.  
  
> [!NOTE]
>  Cada **Error** objeto representa un error de proveedor específico, no un error de ADO. Errores de ADO se exponen en el mecanismo de control de excepciones de tiempo de ejecución. Por ejemplo, en Microsoft Visual Basic, la aparición de un error específico de ADO desencadenará una **On Error** eventos y aparecen en la **Error** objeto. Para obtener una lista completa de errores de ADO, vea el [ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md) tema.  
  
 Puede leer un **Error** propiedades del objeto para obtener detalles específicos sobre cada error, incluido lo siguiente:  
  
-   El [descripción](../../../ado/reference/ado-api/description-property.md) propiedad, que contiene el texto del error. Se trata de la propiedad predeterminada.  
  
-   El [número](../../../ado/reference/ado-api/number-property-ado.md) propiedad, que contiene el **largo** valor entero de la constante del error.  
  
-   El [origen](../../../ado/reference/ado-api/source-property-ado-error.md) propiedad, que identifica el objeto que provocó el error. Esto es especialmente útil cuando hay varias **Error** objetos en el **errores** después de una solicitud a un origen de datos de colección.  
  
-   El [SQLState](../../../ado/reference/ado-api/sqlstate-property.md) y [NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md) propiedades, que proporcionan información de orígenes de datos SQL.  
  
 Cuando se produce un error de proveedor, se coloca en el **errores** colección de la **conexión** objeto. ADO admite la devolución de varios errores por una sola operación de ADO para permitir la información de error específico del proveedor. Para obtener esta información de error enriquecida en un controlador de errores, utilice las características de interceptación de errores apropiadas del lenguaje o entorno que esté trabajando y, a continuación, use bucles anidados para enumerar las propiedades de cada **Error** objeto en el **Errores** colección.  
  
> [!NOTE]
>  **Microsoft Visual Basic y los usuarios de VBScript** si no es válido no **conexión** objeto, deberá recuperar la información de error desde el **Error** objeto.  
  
 Al igual que los proveedores de hacer, ADO borra el **información de Error OLE** objeto antes de realizar una llamada que pueda generar un nuevo error de proveedor. Sin embargo, el **errores** colección en el **conexión** objeto está desactivado y se rellena únicamente cuando el proveedor genera un nuevo error, o cuando el [clara](../../../ado/reference/ado-api/clear-method-ado.md) se llama al método.  
  
 Algunos métodos y propiedades devuelven advertencias que aparecen como **Error** objetos en el **errores** colección pero no detienen la ejecución de un programa. Antes de llamar a la [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), o [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) métodos en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto; el [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md) método en un **conexión** objeto; o establecer el [filtro](../../../ado/reference/ado-api/filter-property.md) propiedad en un **Recordset** de objeto, llame a la **borrar**método en el **errores** colección. De este modo, puede leer el [recuento](../../../ado/reference/ado-api/count-property-ado.md) propiedad de la **errores** devuelve de colección para probar las advertencias.  
  
 El **Error** objeto no es seguro para scripting.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades del objeto Error](../../../ado/reference/ado-api/error-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Descripción, HelpContext, HelpFile, NativeError, número, origen y ejemplo de las propiedades SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Descripción, HelpContext, HelpFile, NativeError, número, origen y ejemplo de las propiedades SQLState (VC ++)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Colección de errores (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Apéndice A: proveedores](../../../ado/guide/appendixes/appendix-a-providers.md)

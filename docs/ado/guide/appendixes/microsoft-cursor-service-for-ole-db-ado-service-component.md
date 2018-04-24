---
title: Servicio de cursores de Microsoft para OLE DB (componente de servicio de ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], cursor service for OLE DB
- cursor service for OLE DB [ADO]
ms.assetid: 420d0989-7cfb-4c66-a7b5-f4199d13165d
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 17bf332ec692bbcaaafaaf5a491d47b360064f56
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="microsoft-cursor-service-for-ole-db-overview"></a>Servicio de cursores de Microsoft para información general acerca OLE DB
El servicio de cursores de Microsoft para OLE DB complementa a las funciones de compatibilidad de cursor de proveedores de datos. Como resultado, el usuario percibe una funcionalidad relativamente uniforme en todos los proveedores de datos.

 El servicio de cursores hace que las propiedades dinámicas estén disponibles y mejora el comportamiento de ciertos métodos. Por ejemplo, el [optimizar](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) propiedad dinámica permite la creación de índices temporales para facilitar determinadas operaciones, como el [buscar](../../../ado/reference/ado-api/find-method-ado.md) método.

 El servicio de cursores habilita la compatibilidad con actualización por lotes en todos los casos. También simula más compatible con tipos de cursor, como los cursores dinámicos, cuando un proveedor de datos solo puede proporcionar cursores menos eficaces, como los cursores estáticos.

## <a name="keyword"></a>Palabra clave
 Para llamar a este componente de servicio, establezca el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) o [conexión](../../../ado/reference/ado-api/connection-object-ado.md) del objeto [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad **adUseClient**.

```
connection.CursorLocation=adUseClient
recordset.CursorLocation=adUseClient
```

## <a name="dynamic-properties"></a>Propiedades dinámicas
 Cuando se invoca el servicio de cursores para OLE DB, se agregan las siguientes propiedades dinámicas a la **Recordset** del objeto [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección. La lista completa de **conexión** y **Recordset** propiedades dinámicas de objeto aparece en la [índice de propiedades dinámicas de ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md). Los nombres de propiedad de OLE DB asociados, en su caso, se incluyen entre paréntesis después del nombre de propiedad de ADO.

 Cambios a algunas propiedades dinámicas no son visibles para el origen de datos subyacente una vez se ha invocado el servicio de Cursor. Por ejemplo, si se establece la *tiempo de espera de comando* propiedad en un **Recordset** no serán visibles para el proveedor de datos subyacente.

```

Recordset1.CursorLocation = adUseClient     'invokes cursor service
Recordset1.Open "authors", _
    "Provider=SQLOLEDB;Data Source=DBServer;User Id=MyUserID;" & _
    "Password=MyPassword;Initial Catalog=pubs;",,adCmdTable
Recordset1.Properties.Item("Command Time out") = 50
' 'Command Time out' property on DBServer is still default (30).

```

 Si la aplicación requiere que el servicio de Cursor, pero debe establecer las propiedades dinámicas en el proveedor subyacente, establezca las propiedades antes de invocar el servicio de Cursor. Configuración de propiedades del objeto de comando siempre se pasa al proveedor de datos subyacente, independientemente de la ubicación del cursor. Por lo tanto, también puede usar un objeto de comando para establecer las propiedades en cualquier momento.

> [!NOTE]
>  La propiedad dinámica DBPROP_SERVERDATAONINSERT no es compatible con el servicio de cursor, aunque es compatible con el proveedor de datos subyacente.

|Nombre de propiedad|Description|
|-------------------|-----------------|
|Recálculo automático (DBPROP_ADC_AUTORECALC)|Para conjuntos de registros creados con el servicio de forma de datos, este valor se indica con qué frecuencia se calculan las columnas calculadas y de agregado. El valor predeterminado (valor = 1) es volver a calcular cada vez que el servicio de forma de datos determina que los valores han cambiado. Si el valor es 0, las columnas calculadas o de agregado solo se calculan cuando se elabora inicialmente la jerarquía.|
|Tamaño del lote (DBPROP_ADC_BATCHSIZE)|Indica el número de instrucciones de actualización que pueden realizarse por lotes antes de enviarse al almacén de datos. Las instrucciones de más de un lote, el menos ciclos de ida y a los datos de almacén.|
|Almacenar en caché filas secundarias (DBPROP_ADC_CACHECHILDROWS)|Para conjuntos de registros creados mediante el servicio de forma de datos, este valor indica si los conjuntos de registros secundarios se almacenan en una memoria caché para su uso posterior.|
|Versión del motor de cursor (DBPROP_ADC_CEVER)|Indica la versión del servicio de Cursor que se va a usar.|
|Mantener el estado de cambio (DBPROP_ADC_MAINTAINCHANGESTATUS)|Indica el texto del comando utilizado para volver a sincronizar un una o varias filas en una combinación de varias tablas.|
|[Optimización](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|Indica si se debe crear un índice. Cuando se establece en **True**, autoriza la creación temporal de índices para mejorar la ejecución de determinadas operaciones.|
|[Cambiar la forma de nombre](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|Indica el nombre de la **conjunto de registros**. Puede ser que se hace referencia dentro del actual, o posteriores, comandos de la forma de datos.|
|[Comando Resync](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|Indica una cadena de comando personalizado utilizado por la [Resync](../../../ado/reference/ado-api/resync-method.md) método cuando el [tabla única](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) propiedad está en vigor.|
|[Catálogo único](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Indica el nombre de la base de datos que contiene la tabla que se hace referencia en el **tabla única** propiedad.|
|[Esquema único](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Indica el nombre del propietario de la tabla que se hace referencia en el **tabla única** propiedad.|
|[Tabla única](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Indica el nombre de la tabla de una en una **Recordset** creado a partir de varias tablas que pueden modificarse las inserciones, actualizaciones o eliminaciones.|
|Criterios de actualización (DBPROP_ADC_UPDATECRITERIA)|Indica qué campos de la **donde** cláusula se utilizan para controlar conflictos producidos durante una actualización.|
|[Actualizar resincronización](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) (DBPROP_ADC_UPDATERESYNC)|Indica si la **Resync** implícitamente se invoca el método después de la [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método (y su comportamiento), cuando la **tabla única** propiedad está en vigor.|

 También puede establecer o recuperar una propiedad dinámica al especificar su nombre como el índice de la **propiedades** colección. Por ejemplo, obtener e imprimir el valor actual de la [optimizar](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) propiedades dinámicas, a continuación, establezca un nuevo valor, como se indica a continuación:

```
Debug.Print rs.Properties("Optimize")
rs.Properties("Optimize") = True
```

## <a name="built-in-property-behavior"></a>Comportamiento de la propiedad integrada
 El servicio de cursores para OLE DB también afecta al comportamiento de algunas propiedades integradas.

|Nombre de propiedad|Description|
|-------------------|-----------------|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|Complementa a los tipos de cursores que están disponibles para un **conjunto de registros**.|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|Complementa a los tipos de bloqueos disponibles para un **conjunto de registros**. Habilita las actualizaciones por lotes.|
|[Sort](../../../ado/reference/ado-api/sort-property.md)|Especifica los nombres de los campos de uno o más que el **Recordset** se ordena encendido y si cada campo se ordena en orden ascendente o descendente.|

## <a name="method-behavior"></a>Comportamiento del método
 El servicio de cursores para OLE DB habilita o afecta al comportamiento de la [campo](../../../ado/reference/ado-api/field-object.md) del objeto [anexado](../../../ado/reference/ado-api/append-method-ado.md) método; y la **Recordset** del objeto [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md), [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), y [guardar](../../../ado/reference/ado-api/save-method.md) métodos.

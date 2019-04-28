---
title: Servicio de cursores de Microsoft para OLE DB (componente de servicio de ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], cursor service for OLE DB
- cursor service for OLE DB [ADO]
ms.assetid: 420d0989-7cfb-4c66-a7b5-f4199d13165d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 500a3e38599b0041b036eb148f837afc67260849
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62719837"
---
# <a name="microsoft-cursor-service-for-ole-db-overview"></a>Servicio de cursores de Microsoft para información general OLE DB
El servicio de cursores de Microsoft para OLE DB complementa las funciones de compatibilidad de cursor de proveedores de datos. Como resultado, el usuario percibe una funcionalidad relativamente uniforme en todos los proveedores de datos.

 El servicio de cursores hace que las propiedades dinámicas que estén disponibles y mejora el comportamiento de ciertos métodos. Por ejemplo, el [optimizar](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) propiedad dinámica permite la creación de índices temporales para facilitar determinadas operaciones, como el [buscar](../../../ado/reference/ado-api/find-method-ado.md) método.

 El servicio de cursores habilita la compatibilidad con actualización por lotes en todos los casos. También simula más compatible con tipos de cursor, como los cursores dinámicos, cuando un proveedor de datos solo puede proporcionar cursores menos eficaces, como los cursores estáticos.

## <a name="keyword"></a>Palabra clave
 Para llamar a este componente de servicio, establezca el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) o [conexión](../../../ado/reference/ado-api/connection-object-ado.md) del objeto [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad **adUseClient**.

```vb
connection.CursorLocation=adUseClient
recordset.CursorLocation=adUseClient
```

## <a name="dynamic-properties"></a>Propiedades dinámicas
 Cuando se invoca el servicio de cursores para OLE DB, se agregan las siguientes propiedades dinámicas a la **Recordset** del objeto [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección. La lista completa de **conexión** y **Recordset** propiedades dinámicas de objeto aparece en el [índice de propiedades dinámicas de ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md). Los nombres de propiedad de OLE DB asociados, en su caso, se incluyen entre paréntesis después del nombre de la propiedad ADO.

 Los cambios a algunas propiedades dinámicas no son visibles para el origen de datos subyacente después de que se ha invocado el servicio de cursores. Por ejemplo, si se establece la *tiempo de espera de comando* propiedad en un **Recordset** no será visible para el proveedor de datos subyacente.

```vb

Recordset1.CursorLocation = adUseClient     'invokes cursor service
Recordset1.Open "authors", _
    "Provider=SQLOLEDB;Data Source=DBServer;User Id=MyUserID;" & _
    "Password=MyPassword;Initial Catalog=pubs;",,adCmdTable
Recordset1.Properties.Item("Command Time out") = 50
' 'Command Time out' property on DBServer is still default (30).

```

 Si la aplicación requiere que el servicio de Cursor, pero debe establecer las propiedades dinámicas en el proveedor subyacente, establezca las propiedades antes de invocar el servicio de cursores. Configuración de propiedades del objeto de comando siempre se pasa al proveedor de datos subyacente, independientemente de la ubicación del cursor. Por lo tanto, también puede usar un objeto de comando para establecer las propiedades en cualquier momento.

> [!NOTE]
>  La propiedad dinámica DBPROP_SERVERDATAONINSERT no es compatible con el servicio de cursores, incluso si es compatible con el proveedor de datos subyacente.

|Nombre de la propiedad|Descripción|
|-------------------|-----------------|
|Recálculo automático (DBPROP_ADC_AUTORECALC)|Para conjuntos de registros creados con el servicio de forma de datos, este valor se indica con qué frecuencia se calculan las columnas calculadas y de agregado. El valor predeterminado (valor = 1) es volver a calcular cada vez que el servicio de forma de datos determina que los valores han cambiado. Si el valor es 0, solo se calculan las columnas calculadas o de agregado cuando la jerarquía se crea inicialmente.|
|Tamaño del lote (DBPROP_ADC_BATCHSIZE)|Indica el número de instrucciones de actualización que pueden encontrarse por lotes antes de enviarse al almacén de datos. Las instrucciones de más de un lote, el menos ciclos de ida y a los datos de almacén.|
|Cache Child Rows (DBPROP_ADC_CACHECHILDROWS)|Para conjuntos de registros creadas con el servicio de forma de datos, este valor indica si los conjuntos de registros secundarios se almacenan en una memoria caché para su uso posterior.|
|Versión del motor de cursor (DBPROP_ADC_CEVER)|Indica la versión del servicio de Cursor que se va a usar.|
|Mantener el estado de cambio (DBPROP_ADC_MAINTAINCHANGESTATUS)|Indica el texto del comando utilizado para volver a sincronizar un una o varias filas en una combinación de varias tablas.|
|[Optimización](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|Indica si se debe crear un índice. Cuando se establece en **True**, autoriza la creación de índices para mejorar la ejecución de ciertas operaciones temporal.|
|[Cambiar la forma de nombre](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|Indica el nombre de la **Recordset**. Puede ser que se hace referencia dentro del actual, o posteriores, los comandos de la forma de datos.|
|[Resincronizar comando](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|Indica una cadena de comando personalizado que usa el [Resync](../../../ado/reference/ado-api/resync-method.md) método cuando el [Unique Table](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) propiedad está en vigor.|
|[Catálogo único](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Indica el nombre de la base de datos que contiene la tabla hace referenciada en el **Unique Table** propiedad.|
|[Esquema único](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Indica el nombre del propietario de la tabla hace referenciado en el **Unique Table** propiedad.|
|[Tabla única](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Indica el nombre de la tabla de una en una **Recordset** creado a partir de varias tablas que pueden ser modificadas por las inserciones, actualizaciones o eliminaciones.|
|Criterios de actualización (DBPROP_ADC_UPDATECRITERIA)|Indica qué campos de la **donde** cláusula se utilizan para controlar los conflictos que se producen durante una actualización.|
|[Actualizar la resincronización](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) (DBPROP_ADC_UPDATERESYNC)|Indica si el **Resync** implícitamente se invoca el método después de la [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método (y su comportamiento), cuando el **Unique Table** propiedad está en vigor.|

 También puede establecer o recuperar una propiedad dinámica especificando su nombre como índice de la **propiedades** colección. Por ejemplo, obtener e imprimir el valor actual de la [optimizar](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) propiedad dinámica, a continuación, establezca un nuevo valor, como se indica a continuación:

```vb
Debug.Print rs.Properties("Optimize")
rs.Properties("Optimize") = True
```

## <a name="built-in-property-behavior"></a>Comportamiento de la propiedad integrada
 El servicio de cursores para OLE DB también afecta al comportamiento de ciertas propiedades integradas.

|Nombre de la propiedad|Descripción|
|-------------------|-----------------|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|Complementa los tipos de cursores que están disponibles para un **Recordset**.|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|Complementa los tipos de bloqueos disponibles para un **Recordset**. Permite procesar por lotes las actualizaciones.|
|[Sort](../../../ado/reference/ado-api/sort-property.md)|Especifica los nombres de campo de uno o más que el **Recordset** se ordena encendido y si cada campo se ordena en orden ascendente o descendente.|

## <a name="method-behavior"></a>Comportamiento del método
 El servicio de cursores para OLE DB habilita o afecta al comportamiento de la [campo](../../../ado/reference/ado-api/field-object.md) del objeto [Append](../../../ado/reference/ado-api/append-method-ado.md) método; y la **Recordset** del objeto [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md), [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), y [guardar](../../../ado/reference/ado-api/save-method.md) métodos.

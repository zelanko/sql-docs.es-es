---
title: Proveedor de Microsoft OLE DB para el servicio de indización de Microsoft | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Indexing Service provider [ADO]
- providers [ADO], OLE DB provider for Microsoft Indexing service
- OLE DB provider for Microsoft Indexing service [ADO]
ms.assetid: f86a0598-5097-471b-8318-d2c859d085f2
author: rothja
ms.author: jroth
ms.openlocfilehash: e4bc6669f961e712ced994a590348604e7bd3274
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760481"
---
# <a name="microsoft-ole-db-provider-for-microsoft-indexing-service-overview"></a>Introducción al proveedor de Microsoft OLE DB para el servicio de indización de Microsoft
El proveedor de Microsoft OLE DB para el servicio de indización de Microsoft proporciona acceso de solo lectura mediante programación al sistema de archivos y a los datos Web indexados por el servicio de indización de Microsoft. Las aplicaciones ADO pueden emitir consultas SQL para recuperar contenido e información de propiedades de archivo.

 El proveedor es de subprocesamiento libre y está habilitado para Unicode.

## <a name="connection-string-parameters"></a>Parámetros de la cadena de conexión
 Para conectarse a este proveedor, establezca el argumento **Provider =** en la propiedad [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) en:

```vb
MSIDXS
```

 La lectura de la propiedad [Provider](../../../ado/reference/ado-api/provider-property-ado.md) también devolverá esta cadena.

## <a name="typical-connection-string"></a>Cadena de conexión típica
 Una cadena de conexión típica para este proveedor es:

```vb
"Provider=MSIDXS;Data Source=myCatalog;Locale Identifier=nnnn;"
```

 La cadena consta de estas palabras clave:

|Palabra clave|Descripción|
|-------------|-----------------|
|**Proveedor**|Especifica el proveedor de OLE DB para el servicio de indización de Microsoft. Normalmente, esta es la única palabra clave especificada en la cadena de conexión.|
|**Data Source** (Origen de datos)|Especifica el nombre del catálogo de servicios de Index Server. Si no se especifica esta palabra clave, se utiliza el catálogo predeterminado del sistema.|
|**Identificador de configuración regional**|Especifica un número único de 32 bits (por ejemplo, 1033) que especifica las preferencias relacionadas con el idioma del usuario. Si no se especifica esta palabra clave, se utiliza el identificador de configuración regional predeterminado del sistema.|

## <a name="command-text"></a>Texto de comando
 La sintaxis de consulta SQL de servicio de indización se compone de las extensiones de la instrucción **Select** de sql-92 y sus cláusulas **from** y **Where** . Los resultados de la consulta se devuelven a través de OLE DB conjuntos de filas, que pueden ser consumidos por ADO y manipulados como objetos de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) .

 Puede buscar palabras o frases exactas o usar caracteres comodín para buscar patrones o raíces de palabras. La lógica de búsqueda se puede basar en decisiones booleanas, términos ponderados o proximidad con otras palabras. También puede buscar por "texto libre", que busca coincidencias según el significado, en lugar de palabras exactas.

 El dialecto del comando específico se documenta totalmente en la documentación de los lenguajes de consulta para el servicio de Index Server.

 El proveedor no acepta llamadas a procedimientos almacenados ni nombres de tabla simples (por ejemplo, la propiedad [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) siempre será **adCmdText**).

## <a name="recordset-behavior"></a>Comportamiento del conjunto de registros
 En las tablas siguientes se enumeran las características disponibles con un objeto de **conjunto de registros** abierto con este proveedor. Solo está disponible el tipo de cursor estático (**adOpenStatic**).

 Para obtener información más detallada sobre el comportamiento del **conjunto de registros** para la configuración del proveedor, ejecute el método [Supports](../../../ado/reference/ado-api/supports-method.md) y enumere la colección [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) del **conjunto de registros** para determinar si las propiedades dinámicas específicas del proveedor están presentes.

 **Disponibilidad de propiedades de conjunto de registros de ADO estándar:**

|Propiedad|Disponibilidad|
|--------------|------------------|
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|lectura/escritura|
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|lectura/escritura|
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|solo lectura|
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|solo lectura|
|[Marcador](../../../ado/reference/ado-api/bookmark-property-ado.md)*|lectura/escritura|
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|lectura/escritura|
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|siempre **adUseServer**|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|siempre **adOpenStatic**|
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|siempre **adEditNone**|
|[ALCANZAR](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|solo lectura|
|[Filter](../../../ado/reference/ado-api/filter-property.md)|lectura/escritura|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|lectura/escritura|
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|no disponible|
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|lectura/escritura|
|[NúmeroDePáginas](../../../ado/reference/ado-api/pagecount-property-ado.md)|solo lectura|
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|lectura/escritura|
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|solo lectura|
|[Origen](../../../ado/reference/ado-api/source-property-ado-recordset.md)|lectura/escritura|
|[State](../../../ado/reference/ado-api/state-property-ado.md)|solo lectura|
|[Estado](../../../ado/reference/ado-api/status-property-ado-recordset.md)|solo lectura|

 \*Los marcadores deben estar habilitados en el proveedor para que esta característica exista en el **conjunto de registros**.

 **Disponibilidad de métodos de conjunto de registros de ADO estándar:**

|Método|¿Disponible?|
|------------|----------------|
|[AgregarNuevo](../../../ado/reference/ado-api/addnew-method-ado.md)|No|
|[Cancelar](../../../ado/reference/ado-api/cancel-method-ado.md)|Yes|
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|No|
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|No|
|[Clonar](../../../ado/reference/ado-api/clone-method-ado.md)|Yes|
|[Close](../../../ado/reference/ado-api/close-method-ado.md)|Yes|
|[Eliminar](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|No|
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|Yes|
|[Mover](../../../ado/reference/ado-api/move-method-ado.md)|Yes|
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Yes|
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|Yes|
|[Abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)|Yes|
|[Requery](../../../ado/reference/ado-api/requery-method.md)|Yes|
|[Resincronizar](../../../ado/reference/ado-api/resync-method.md)|Yes|
|[Admite](../../../ado/reference/ado-api/supports-method.md)|Yes|
|[Actualizar](../../../ado/reference/ado-api/update-method.md)|No|
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|No|

 Para obtener detalles de implementación específicos e información funcional acerca del proveedor de Microsoft OLE DB para el servicio de indización de Microsoft, consulte la [Guía del programador de OLE DB](https://msdn.microsoft.com/library/windows/desktop/ms713643.aspx)o visite la página servicios web del sitio web de Windows NT Server.

## <a name="see-also"></a>Consulte también
 [Propiedad CommandType (ADO](../../../ado/reference/ado-api/commandtype-property-ado.md) ) propiedad [ConnectionString (](../../../ado/reference/ado-api/connectionstring-property-ado.md) ADO) [colección de propiedades (](../../../ado/reference/ado-api/properties-collection-ado.md) ADO) [propiedad del proveedor (](../../../ado/reference/ado-api/provider-property-ado.md) ADO) [objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [admite el método](../../../ado/reference/ado-api/supports-method.md)

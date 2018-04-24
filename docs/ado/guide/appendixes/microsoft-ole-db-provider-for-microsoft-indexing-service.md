---
title: Proveedor Microsoft OLE DB para servicios de Index Server de Microsoft | Documentos de Microsoft
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
- Indexing Service provider [ADO]
- providers [ADO], OLE DB provider for Microsoft Indexing service
- OLE DB provider for Microsoft Indexing service [ADO]
ms.assetid: f86a0598-5097-471b-8318-d2c859d085f2
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f84d13fa3f4e2da728c914f2228233a04e64643f
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="microsoft-ole-db-provider-for-microsoft-indexing-service-overview"></a>Proveedor Microsoft OLE DB para Microsoft Introducción al servicio de indización
El proveedor Microsoft OLE DB para servicios de Index Server de Microsoft proporciona acceso mediante programación de solo lectura para el sistema de archivos y datos Web indizados por servicios de Index Server de Microsoft. Las aplicaciones ADO pueden emitir consultas SQL para recuperar información de la propiedad de contenido y de archivos.

 El proveedor es de subprocesamiento libre y está habilitado para UNICODE.

## <a name="connection-string-parameters"></a>Parámetros de cadena de conexión
 Para conectarse a este proveedor, establezca el **proveedor =** argumento pasado a la [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propiedad:

```
MSIDXS
```

 Leer la [proveedor](../../../ado/reference/ado-api/provider-property-ado.md) propiedad devolverá también esta cadena.

## <a name="typical-connection-string"></a>Cadena de conexión típica
 Una cadena de conexión típica para este proveedor es:

```
"Provider=MSIDXS;Data Source=myCatalog;Locale Identifier=nnnn;"
```

 La cadena consta de estas palabras clave:

|Palabra clave|Description|
|-------------|-----------------|
|**Proveedor**|Especifica el proveedor OLE DB para servicios de Index Server de Microsoft. Suele ser la única palabra clave especificada en la cadena de conexión.|
|**Origen de datos**|Especifica el nombre del catálogo de servicios de Index Server. Si no se especifica esta palabra clave, se utiliza el catálogo del sistema de forma predeterminada.|
|**Identificador de configuración regional**|Especifica un número exclusivo de 32 bits (por ejemplo, 1033) que especifica las preferencias relacionadas con el idioma del usuario. Si no se especifica esta palabra clave, se utiliza el identificador de configuración regional del sistema predeterminada.|

## <a name="command-text"></a>Texto de comando
 La sintaxis de consulta de SQL del servicio de Index Server consta de las extensiones de SQL-92 **seleccione** instrucción y su **FROM** y **donde** cláusulas. Los resultados de la consulta se devuelven a través de conjuntos de filas de OLE DB, que pueden ser utilizados por ADO y manipulados como [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objetos.

 Puede buscar palabras o frases exactas o usar caracteres comodín para buscar patrones o raíces de palabras. La lógica de búsqueda se puede basar en decisiones booleanas, términos ponderados o cerca de otra palabra. También puede buscar por "texto libre", que busca a coincidencias basadas en significado en lugar de en palabras exactas.

 El dialecto del comando específico está completamente documentado en los lenguajes de consulta para obtener documentación de servicios de Index Server.

 El proveedor no acepta llamadas a procedimientos almacenados o nombres de tabla simples (por ejemplo, el [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) propiedad siempre será **adCmdText**).

## <a name="recordset-behavior"></a>Comportamiento del conjunto de registros
 Las tablas siguientes enumeran las características disponibles con un **Recordset** objeto abierto con este proveedor. El tipo de cursor estático (**adOpenStatic**) está disponible.

 Para obtener más información acerca de **Recordset** comportamiento de la configuración del proveedor, ejecute el [admite](../../../ado/reference/ado-api/supports-method.md) método y enumerar el [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección de la **Recordset** para determinar si las propiedades dinámicas específicas del proveedor están presentes.

 **Disponibilidad de las propiedades de conjunto de registros ADO estándares:**

|Propiedad|Disponibilidad|
|--------------|------------------|
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|lectura/escritura|
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|lectura/escritura|
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|solo lectura|
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|solo lectura|
|[Marcador](../../../ado/reference/ado-api/bookmark-property-ado.md)*|lectura/escritura|
|[cacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|lectura/escritura|
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|siempre **adUseServer**|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|siempre **adOpenStatic**|
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|siempre **adEditNone**|
|[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|solo lectura|
|[Filtro](../../../ado/reference/ado-api/filter-property.md)|lectura/escritura|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|lectura/escritura|
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|no disponible|
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|lectura/escritura|
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|solo lectura|
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|lectura/escritura|
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|solo lectura|
|[Source](../../../ado/reference/ado-api/source-property-ado-recordset.md)|lectura/escritura|
|[State](../../../ado/reference/ado-api/state-property-ado.md)|solo lectura|
|[Estado](../../../ado/reference/ado-api/status-property-ado-recordset.md)|solo lectura|

 \*Marcadores deben estar habilitados en el proveedor para esta característica exista en el **conjunto de registros**.

 **Disponibilidad de los métodos de conjunto de registros ADO estándar:**

|Método|¿Está disponible?|
|------------|----------------|
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|no|
|[Cancelar](../../../ado/reference/ado-api/cancel-method-ado.md)|Sí|
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|no|
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|no|
|[clon](../../../ado/reference/ado-api/clone-method-ado.md)|Sí|
|[Cerrar](../../../ado/reference/ado-api/close-method-ado.md)|Sí|
|[Eliminar](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|no|
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|Sí|
|[Mover](../../../ado/reference/ado-api/move-method-ado.md)|Sí|
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sí|
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|Sí|
|[Abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)|Sí|
|[Requery](../../../ado/reference/ado-api/requery-method.md)|Sí|
|[Resincronización](../../../ado/reference/ado-api/resync-method.md)|Sí|
|[Es compatible con](../../../ado/reference/ado-api/supports-method.md)|Sí|
|[Update](../../../ado/reference/ado-api/update-method.md)|no|
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|no|

 Para obtener detalles de implementación específicos y funcional información sobre el proveedor Microsoft OLE DB para servicios de Index Server de Microsoft, consulte el [Guía del programador de OLE DB](https://msdn.microsoft.com/library/windows/desktop/ms713643.aspx), o visite la página de servicios Web de la Web del servidor de Windows NT sitio.

## <a name="see-also"></a>Vea también
 [La propiedad CommandType (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md) [propiedad ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [colección Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [(ADO) de la propiedad de proveedor](../../../ado/reference/ado-api/provider-property-ado.md) [ Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [admite (método)](../../../ado/reference/ado-api/supports-method.md)

---
title: Creación de conjuntos de filas de parámetros con valores de tabla | Microsoft Docs
description: Creación de conjuntos de filas de parámetros con valores de tabla estáticos y dinámicos
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, rowset creation
author: pmasl
ms.author: pelopes
ms.openlocfilehash: c771d8bde657b464b29a109dadd7a4d6fa33fbdb
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67994108"
---
# <a name="table-valued-parameter-rowset-creation"></a>Creación de conjuntos de filas de parámetros con valores de tabla
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Aunque los consumidores pueden proporcionar cualquier objeto de conjunto de filas para los parámetros con valores de tabla, los objetos de conjunto de filas típicos se implementan para los almacenes de datos back-end y, por consiguiente, proporcionan un rendimiento limitado. Por esta razón, el controlador OLE DB para SQL Server permite a los consumidores crear un objeto de conjunto de filas especializado basado en los datos en memoria. Este objeto de conjunto de filas especial en memoria es un nuevo objeto COM denominado conjunto de filas de parámetros con valores de tabla. Proporciona una funcionalidad similar a la de los conjuntos de parámetros.  
  
 El consumidor crea explícitamente objetos de conjunto de filas de parámetros con valores de tabla para los parámetros de entrada a través de varias interfaces de nivel de sesión. Hay una instancia de un objeto de conjunto de filas de parámetro con valores de tabla para cada parámetro con valores de tabla. El consumidor puede crear los objetos de conjunto de filas de parámetros con valores de tabla proporcionando información de metadatos que ya se conoce (escenario estático) o detectando esa información a través de interfaces de proveedor (escenario dinámico). En las secciones siguientes se describen los dos escenarios.  
  
## <a name="static-scenario"></a>Escenario estático  
 Cuando se conoce el tipo de información, el consumidor usa ITableDefinitionWithConstraints::CreateTableWithConstraints para crear una instancia de un objeto de conjunto de filas de parámetros con valores de tabla que corresponde a un parámetro con valores de tabla.  
  
 El campo *guid* (parámetro *pTableID*) contiene el GUID especial (CLSID_ROWSET_TVP). El miembro *pwszName* contiene el nombre del tipo de parámetro con valores de tabla del que el consumidor quiere crear una instancia. El campo *eKind* se establecerá en DBKIND_GUID_NAME. Este nombre es necesario en una instrucción SQL ad hoc, pero es opcional en las llamadas a procedimientos.  
  
 Para la agregación, el consumidor pasa el parámetro *pUnkOuter* con el elemento IUnknown de control.  
  
 Las propiedades del objeto de conjunto de filas de parámetros con valores de tabla son de solo lectura, por lo que no se espera que el consumidor establezca ninguna propiedad en *rgPropertySets*.  
  
 Para el miembro *rgPropertySets* de cada estructura DBCOLUMNDESC, el consumidor puede especificar propiedades adicionales para cada columna. Estas propiedades pertenecen a la propiedad DBPROPSET_SQLSERVERCOLUMN establecida. Permiten especificar la configuración calculada y predeterminada de cada columna. Admiten también propiedades de columna existentes, como la nulabilidad y la identidad.  
  
 Para recuperar la información correspondiente de un objeto de conjunto de filas de parámetros con valores de tabla, el consumidor usa IRowsetInfo::GetProperties.  
  
 Para recuperar información sobre el estado null, unique, computed y update de cada columna, el consumidor puede usar IColumnsRowset::GetColumnsRowset o IColumnsInfo::GetColumnInfo. Estos métodos proporcionan información detallada sobre cada columna de conjunto de filas de parámetros con valores de tabla.  
  
 El consumidor especifica el tipo de cada columna del parámetro con valores de tabla. Es similar al modo en que se especifican las columnas cuando se crea una tabla en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El consumidor obtiene un objeto de conjunto de filas de parámetros con valores de tabla de OLE DB Driver for SQL Server mediante el parámetro de salida *ppRowset*.  
  
## <a name="dynamic-scenario"></a>Escenario dinámico  
 Cuando el consumidor no tiene información de tipo, debe utilizar IOpenRowset::OpenRowset para crear una instancia de los objetos de conjunto de filas de parámetros con valores de tabla. Todo lo que el consumidor tiene que proporcionar al proveedor es el nombre de tipo.  
  
 En este escenario, el proveedor obtiene la información de tipo de un objeto de conjunto de filas de parámetros con valores de tabla del servidor en nombre del consumidor.  
  
 Los parámetros *pTableID* y *pUnkOuter* deben establecerse como en el escenario estático. Después, el controlador OLE DB para SQL Server obtiene la información de tipo (la información de columna y las restricciones) del servidor y devuelve un objeto de conjunto de filas de parámetros con valores de tabla a través del parámetro *ppRowset*. Esta operación requiere la comunicación con el servidor y, por tanto, su rendimiento no es tan bueno como el del escenario estático. El escenario dinámico solamente funciona con llamadas a procedimientos parametrizadas.  
  
## <a name="see-also"></a>Consulte también  
 [Parámetros con valores de tabla &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar parámetros con valores de tabla &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  

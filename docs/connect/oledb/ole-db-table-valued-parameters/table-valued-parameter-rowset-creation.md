---
title: Creación de conjuntos de filas de parámetros con valores de tabla | Documentos de Microsoft
description: Creación de conjuntos de filas de parámetro con valores de tabla estática y dinámica
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, rowset creation
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 0bfd6f54e374c77268641e151f738efa8a2385b5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="table-valued-parameter-rowset-creation"></a>Creación de conjuntos de filas de parámetros con valores de tabla
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Aunque los consumidores pueden proporcionar cualquier objeto de conjunto de filas para los parámetros con valores de tabla, los objetos de conjunto de filas típicos se implementan para los almacenes de datos back-end y, por consiguiente, proporcionan un rendimiento limitado. Por este motivo, el controlador OLE DB para SQL Server permite a los consumidores crear un objeto de conjunto de filas especializado encima de los datos en memoria. Este objeto de conjunto de filas especial en memoria es un nuevo objeto COM denominado conjunto de filas de parámetros con valores de tabla. Proporciona una funcionalidad similar a la de los conjuntos de parámetros.  
  
 El consumidor crea explícitamente objetos de conjunto de filas de parámetros con valores de tabla para los parámetros de entrada a través de varias interfaces de nivel de sesión. Hay una instancia de un objeto de conjunto de filas de parámetro con valores de tabla por cada parámetro con valores de tabla. El consumidor puede crear los objetos de conjunto de filas de parámetros con valores de tabla proporcionando información de metadatos que ya se conoce (escenario estático) o detectando esa información a través de interfaces de proveedor (escenario dinámico). En las secciones siguientes se describen los dos escenarios.  
  
## <a name="static-scenario"></a>Escenario estático  
 Cuando se conoce la información de tipo, el consumidor utiliza ITableDefinitionWithConstraints::CreateTableWithConstraints para crear instancias de un objeto de conjunto de filas de parámetro con valores de tabla que corresponde a un parámetro con valores de tabla.  
  
 El *guid* campo (*pTableID* parámetro) contiene el GUID especial (CLSID_ROWSET_TVP). El *pwszName* miembro contiene el nombre del parámetro con valores de tabla de tipo que el consumidor desea crear una instancia. El *eKind* campo se establecerá en DBKIND_GUID_NAME. Este nombre es necesario cuando la instrucción SQL ad hoc; el nombre es opcional si es una llamada a procedimiento.  
  
 Para la agregación, el consumidor pasa el *pUnkOuter* parámetro con el IUnknown de control.  
  
 Las propiedades del objeto de conjunto de filas de parámetro con valores de tabla son de solo lectura, por lo que no espera que el consumidor para establecer las propiedades en *rgPropertySets*.  
  
 Para el *rgPropertySets* miembro de cada estructura DBCOLUMNDESC, el consumidor puede especificar propiedades adicionales para cada columna. Estas propiedades pertenecen a la propiedad DBPROPSET_SQLSERVERCOLUMN establecida. Permiten especificar la configuración calculada y predeterminada de cada columna. Admiten también propiedades de columna existentes, como la nulabilidad y la identidad.  
  
 Para recuperar la información correspondiente de un objeto de conjunto de filas de parámetro con valores de tabla, el consumidor utiliza IRowsetInfo:: GetProperties.  
  
 Para recuperar información sobre el valor null, unique, calculadas y actualizar el estado de cada columna, el consumidor puede utilizar IColumnsRowset:: GetColumnsRowset o IColumnsInfo:: GetColumnInfo. Estos métodos proporcionan información detallada sobre cada columna de conjunto de filas de parámetros con valores de tabla.  
  
 El consumidor especifica el tipo de cada columna del parámetro con valores de tabla. Es similar a cómo se especifican las columnas cuando se crea una tabla en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El consumidor Obtiene un objeto de conjunto de filas de parámetro con valores de tabla desde el controlador OLE DB para SQL Server a través de la *ppRowset* parámetro de salida.  
  
## <a name="dynamic-scenario"></a>Escenario dinámico  
 Cuando el consumidor no tiene información de tipo, debe usar IOpenRowset:: OpenRowset para crear instancias de objetos de conjunto de filas de parámetro con valores de tabla. Todo lo que el consumidor tiene que proporcionar al proveedor es el nombre de tipo.  
  
 En este escenario, el proveedor obtiene la información de tipo de un objeto de conjunto de filas de parámetros con valores de tabla del servidor en nombre del consumidor.  
  
 El *pTableID* y *pUnkOuter* parámetros deben establecerse como en el escenario estático. El controlador OLE DB para SQL Server, a continuación, obtiene la información de tipo (información de columnas y restricciones) desde el servidor y devolver un objeto de conjunto de filas de parámetro con valores de tabla a través de la *ppRowset* parámetro. Esta operación requiere la comunicación con el servidor y, por tanto, no funciona, así como el escenario estático. El escenario dinámico solamente funciona con llamadas a procedimientos parametrizadas.  
  
## <a name="see-also"></a>Vea también  
 [Parámetros con valores de tabla &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar con valores de tabla parámetros & #40; OLE DB & #41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  

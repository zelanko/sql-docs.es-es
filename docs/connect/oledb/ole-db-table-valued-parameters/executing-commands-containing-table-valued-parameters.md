---
title: Ejecutar comandos que contienen parámetros con valores de tabla | Documentos de Microsoft
description: Ejecutar comandos que contienen parámetros con valores de tabla
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
- table-valued parameters, executing commands containing
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: b3433ccbfd2cc8aa16b453a3a9f34c1f19fa17a0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="executing-commands-containing-table-valued-parameters"></a>Ejecutar comandos que contienen parámetros con valores de tabla
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Ejecutar un comando con parámetros con valores de tabla consta de dos fases:  
  
1.  Especificar los tipos de parámetros.  
  
2.  Enlazar los datos de los parámetros.  
  
## <a name="table-valued-parameter-specification"></a>Especificación de parámetros con valores de tabla  
 El consumidor puede especificar el tipo del parámetro con valores de tabla. Esta información incluye el nombre del tipo del parámetro con valores de tabla. También incluye el nombre del esquema, si el tipo de tabla definido por el usuario para el parámetro con valores de tabla no está en el esquema predeterminado actual para la conexión. Según la compatibilidad del servidor, el consumidor también puede especificar la información de metadatos opcionales, como el orden de las columnas y puede indicar que todas las filas de ciertas columnas tengan valores predeterminados.  
  
 Para especificar un parámetro con valores de tabla, el consumidor llama ISSCommandWithParamter::SetParameterInfo y opcionalmente llama isscommandwithparameters:: SetParameterProperties. Para un parámetro con valores de tabla, el *pwszDataSourceType* los campos de la estructura DBPARAMBINDINFO tiene un valor de DBTYPE_TABLE. El *ulParamSize* campo se establece en ~ 0 para indicar que la longitud es desconocido. Determinadas propiedades para los parámetros con valores de tabla, como nombre de esquema, nombre de tipo, orden de las columnas y las columnas de forma predeterminada, se pueden establecer a través de isscommandwithparameters:: SetParameterProperties.  
  
## <a name="table-valued-parameter-binding"></a>Enlace de parámetros con valores de tabla  
 Un parámetro con valores de tabla puede ser cualquier objeto de conjunto de filas. Durante la ejecución, el proveedor lee en este objeto mientras envía los parámetros con valores de tabla al servidor.  
  
 Para enlazar el parámetro con valores de tabla, el consumidor llama a IAccessor:: CreateAccessor. El *wType* campo de la estructura DBBINDING para el parámetro con valores de tabla está establecido en DBTYPE_TABLE. El *pObject* miembro de la estructura DBBINDING es distinto de NULL y la *pObject*del *iid* miembro se establece en IID_IRowset o cualquier otro objeto de conjunto de filas de parámetro con valores de tabla interfaces. Los campos restantes de la estructura DBBINDING deben establecerse la misma manera que está configurados para BLOB transmitidos.  
  
 En los enlaces para el parámetro con valores de tabla y el objeto de conjunto de filas asociado a un parámetro con valores de tabla, se aplican las restricciones siguientes:  
  
-   Los únicos valores de estado permitidos para los datos de columnas de conjunto de filas de parámetro con valores de tabla son DBSTATUS_S_ISNULL y DBSTATUS_S_OK. DBSTATUS_S_DEFAULT producirá un error y el valor de estado enlazado se establecerá en DBSTATUS_E_BADSTATUS.  
  
-   Un parámetro con valores de tabla se puede marcar con el estado DBSTATUS_S_DEFAULT. Los únicos valores válidos son DBSTATUS_S_DEFAULT y DBSTATUS_S_OK. Cuando el estado se establece en DBSTATUS_S_DEFAULT, el valor del parámetro con valores de tabla corresponde a una tabla vacía.  
  
-   Las columnas de solo lectura en parámetros con valores de tabla (columnas de identidad o calculadas) se deben marcar como predeterminadas utilizando la propiedad SSPROP_PARAM_TABLE_DEFAULT_COLUMNS. Las columnas que tienen un valor predeterminado también se deben marcar como predeterminadas mediante la propiedad SSPROP_PARAM_TABLE_DEFAULT_COLUMNS para que se pueda utilizar el valor predeterminado para los valores de datos de la columna para un parámetro con valores de tabla determinado. El proveedor no tendrá en cuenta los valores de datos enlazados para las columnas marcadas como predeterminadas.  
  
-   Los datos se enviarán al servidor para las columnas con DBPROP_COL_AUTOINCREMENT o SSPROP_COL_COMPUTED, a menos que también se establezca SSPROP_PARAM_TABLE_DEFAULT.  
  
## <a name="see-also"></a>Vea también  
 [Parámetros con valores de tabla &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar con valores de tabla parámetros & #40; OLE DB & #41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  

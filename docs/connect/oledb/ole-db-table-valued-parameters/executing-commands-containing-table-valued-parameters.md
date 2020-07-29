---
title: Ejecutar comandos que contienen parámetros con valores de tabla | Microsoft Docs
description: Ejecutar comandos que contienen parámetros con valores de tabla
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, executing commands containing
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 4a7fccfe3e5d24673f9fe5b9429f212bf2df7e7a
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008768"
---
# <a name="executing-commands-containing-table-valued-parameters"></a>Ejecutar comandos que contienen parámetros con valores de tabla
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  La ejecución de un comando con parámetros con valores de tabla consta de dos fases:  
  
1.  Especificar los tipos de parámetros.  
  
2.  Enlazar los datos de los parámetros.  
  
## <a name="table-valued-parameter-specification"></a>Especificación de parámetros con valores de tabla  
 El consumidor puede especificar el tipo del parámetro con valores de tabla. Esta información incluye el nombre del tipo del parámetro con valores de tabla. También incluye el nombre de esquema si el tipo de tabla definido por el usuario para el parámetro con valores de tabla no está en el esquema predeterminado actual de la conexión. En función de la compatibilidad del servidor, el consumidor también puede especificar información opcional sobre los metadatos, como el orden de las columnas, y puede indicar que todas las filas de ciertas columnas tienen valores predeterminados.  
  
 Para especificar un parámetro con valores de tabla, el consumidor llama a ISSCommandWithParameter::SetParameterInfo y, opcionalmente, llama a ISSCommandWithParameters::SetParameterProperties. En el caso de un parámetro con valores de tabla, el campo *pwszDataSourceType* de la estructura DBPARAMBINDINFO tiene un valor de DBTYPE_TABLE. El campo *ulParamSize* se establece en ~0 para indicar que no se conoce la longitud. Algunas propiedades de los parámetros con valores de tabla, como nombre de esquema, nombre de tipo, orden de columnas y columnas predeterminadas, se pueden establecer mediante ISSCommandWithParameters::SetParameterProperties.  
  
## <a name="table-valued-parameter-binding"></a>Enlace de parámetros con valores de tabla  
 Un parámetro con valores de tabla puede ser cualquier objeto de conjunto de filas. Durante la ejecución, el proveedor lee en este objeto mientras envía los parámetros con valores de tabla al servidor.  
  
 Para enlazar el parámetro con valores de tabla, el consumidor llama a IAccessor::CreateAccessor. El campo *wType* de la estructura DBBINDING del parámetro con valores de tabla se establece en DBTYPE_TABLE. El miembro *pObject* de la estructura DBBINDING es distinto de NULL y el miembro *iid* de *pObject* se establece en IID_IRowset o cualquier otra interfaz de objeto de conjunto de filas de parámetro con valores de tabla. Los campos restantes de la estructura DBBINDING se deben establecer de la misma manera que los BLOB transmitidos.  
  
 En los enlaces para el parámetro con valores de tabla y el objeto de conjunto de filas asociado a un parámetro con valores de tabla, se aplican las restricciones siguientes:  
  
-   Los únicos valores de estado permitidos para los datos de columnas de conjunto de filas de parámetro con valores de tabla son DBSTATUS_S_ISNULL y DBSTATUS_S_OK. DBSTATUS_S_DEFAULT producirá un error y el valor de estado enlazado se establecerá en DBSTATUS_E_BADSTATUS.  
  
-   Un parámetro con valores de tabla se puede marcar con el estado DBSTATUS_S_DEFAULT. Los únicos valores válidos son DBSTATUS_S_DEFAULT y DBSTATUS_S_OK. Cuando el estado se establece en DBSTATUS_S_DEFAULT, el valor del parámetro con valores de tabla corresponde a una tabla vacía.  
  
-   Las columnas de solo lectura en parámetros con valores de tabla (columnas de identidad o calculadas) se deben marcar como predeterminadas utilizando la propiedad SSPROP_PARAM_TABLE_DEFAULT_COLUMNS. Las columnas que tienen un valor predeterminado también se deben marcar como predeterminadas mediante la propiedad SSPROP_PARAM_TABLE_DEFAULT_COLUMNS para que se pueda utilizar el valor predeterminado para los valores de datos de la columna para un parámetro con valores de tabla determinado. El proveedor no tendrá en cuenta los valores de datos enlazados para las columnas marcadas como predeterminadas.  
  
-   Los datos se enviarán al servidor para las columnas con DBPROP_COL_AUTOINCREMENT o SSPROP_COL_COMPUTED, a menos que también se establezca SSPROP_PARAM_TABLE_DEFAULT.  
  
## <a name="see-also"></a>Consulte también  
 [Parámetros con valores de tabla &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar parámetros con valores de tabla &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  

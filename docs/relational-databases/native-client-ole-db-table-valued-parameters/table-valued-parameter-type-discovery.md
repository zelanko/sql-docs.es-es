---
title: Detección de tipos de parámetros con valores de tabla | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, type discovery
ms.assetid: f55818c2-ebb5-4cf6-8c0c-0da41f592560
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1d006c9159ce718186a690a532eebe1cef08642d
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86012990"
---
# <a name="table-valued-parameter-type-discovery"></a>Detección de tipos de parámetros con valores de tabla
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  El consumidor, es decir, la aplicación cliente que usa el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client, puede detectar el tipo de cada parámetro de comando si se ha proporcionado el texto del comando al proveedor de OLE DB. Después de conocer el tipo de un parámetro con valores de tabla, el consumidor puede detectar la información de metadatos de cada columna individual del parámetro con valores de tabla.  
  
 La información de tipo de los parámetros de procedimiento es compatible con ICommandWithParameters::GetParameterInfo en la mayoría de tipos de parámetro. A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], con la introducción de los tipos definidos por el usuario y el tipo de datos **xml**, no bastaba con usar el método GetParameterInfo para este propósito porque no se podía proporcionar información de los tipos definidos por el usuario (nombre, esquema y catálogo) mediante ICommandWithParameters. Se definió una nueva interfaz, ISSCommandWithParameters, para proporcionar información de tipo extendido.  
  
 En el caso de los parámetros con valores de tabla, también usará la interfaz ISSCommandWithParameters para detectar información detallada. El cliente llama a ISSCommandWithParameters::GetParameterInfo después de preparar el objeto de comando. Para los parámetros con valores de tabla, el proveedor establece el miembro *wType* de la estructura DBPARAMINFO en DBTYPE_TABLE. El campo *ulParamSize* de la estructura de DBPARAMINFO tiene un valor de ~0.  
  
 El consumidor solicitará después propiedades adicionales (el nombre de catálogo del tipo de parámetro con valores de tabla, el nombre de esquema del tipo de parámetro con valores de tabla, el nombre del tipo de parámetro con valores de tabla, el orden de las columnas y las columnas predeterminadas) mediante ISSCommandWithParameters::GetParameterProperties.  
  
 Una vez conocido el nombre de tipo, para recuperar la información de cada columna individual, el consumidor debe llamar a IOpenRowset::OpenRowsetor u obtener el conjunto de filas DBSCHEMA_TABLE_TYPE_COLUMNS al especificar el nombre del tipo de parámetro con valores de tabla como el nombre de la tabla.  
  
## <a name="see-also"></a>Consulte también  
 [Parámetros con valores de tabla &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar parámetros con valores de tabla &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  

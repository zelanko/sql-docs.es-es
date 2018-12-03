---
title: Detección de tipos de parámetro con valores de tabla | Microsoft Docs
description: Con valores de tabla detección de tipos parámetro mediante el controlador de OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, type discovery
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: aab78327d575858675ade3bbc5d652cce5db12a5
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52506249"
---
# <a name="table-valued-parameter-type-discovery"></a>Detección de tipos de parámetros con valores de tabla
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El consumidor, es decir, la aplicación cliente que usa el controlador OLE DB para SQL Server, puede detectar el tipo de parámetro de cada comando si se ha proporcionado el texto del comando al proveedor OLE DB. Después de conocer el tipo de un parámetro con valores de tabla, el consumidor puede detectar la información de metadatos de cada columna individual del parámetro con valores de tabla.  
  
 La información de tipos de parámetros de procedimiento es compatible con ICommandWithParameters:: GetParameterInfo para la mayoría de los tipos de parámetro. A partir de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], con la introducción de los tipos definidos por el usuario y el tipo de datos **xml**, no bastaba con usar el método GetParameterInfo para este propósito porque no se podía proporcionar información de los tipos definidos por el usuario (nombre, esquema y catálogo) mediante ICommandWithParameters. Se definió una nueva interfaz, ISSCommandWithParameters, para proporcionar información de tipo extendido.  
  
 Para los parámetros con valores de tabla, también se usa la interfaz ISSCommandWithParameters para detectar información detallada. El cliente llama a ISSCommandWithParameters::GetParameterInfo después de preparar el objeto de comando. Para los parámetros con valores de tabla, el proveedor establece el miembro *wType* de la estructura DBPARAMINFO en DBTYPE_TABLE. El campo *ulParamSize* de la estructura de DBPARAMINFO tiene un valor de ~0.  
  
 El consumidor solicitará después propiedades adicionales (el nombre de catálogo del tipo de parámetro con valores de tabla, el nombre de esquema del tipo de parámetro con valores de tabla, el nombre del tipo de parámetro con valores de tabla, el orden de las columnas y las columnas predeterminadas) mediante ISSCommandWithParameters::GetParameterProperties.  
  
 Una vez conocido el nombre de tipo, para recuperar la información de cada columna individual, el consumidor debe llamar a IOpenRowset::OpenRowsetor u obtener el conjunto de filas DBSCHEMA_TABLE_TYPE_COLUMNS al especificar el nombre del tipo de parámetro con valores de tabla como el nombre de la tabla.  
  
## <a name="see-also"></a>Ver también  
 [Parámetros con valores de tabla &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar parámetros con valores de tabla &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  

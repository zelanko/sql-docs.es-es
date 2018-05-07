---
title: Detección de tipos de parámetro con valores de tabla | Documentos de Microsoft
description: Con valores de tabla detección de tipo parámetro mediante el controlador OLE DB para SQL Server
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
- table-valued parameters, type discovery
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 502db140bbfb63bf4d0c3d7c6a82bb2459633384
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="table-valued-parameter-type-discovery"></a>Detección de tipos de parámetros con valores de tabla
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El consumidor, es decir, la aplicación de cliente con el controlador OLE DB para SQL Server, puede detectar el tipo de cada parámetro de comando si el texto del comando se ha proporcionado el proveedor OLE DB. Después de que se conoce el tipo de un parámetro con valores de tabla, el consumidor puede detectar la información de metadatos para cada columna del parámetro con valores de tabla.  
  
 La información de tipo de parámetros de procedimiento es compatible con ICommandWithParameters:: GetParameterInfo para la mayoría de los tipos de parámetro. A partir de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], con la introducción de tipos definidos por el usuario y la **xml** tipo de datos, el método GetParameterInfo no es suficiente para este propósito porque no era posible proporcionar el tipo definido por el usuario información (nombre, esquema y catálogo) a través de ICommandWithParameters. Se definió una nueva interfaz, ISSCommandWithParameters, para proporcionar información de tipo extendido.  
  
 Para los parámetros con valores de tabla, también se usa la interfaz ISSCommandWithParameters para detectar información detallada. El cliente llama a ISSCommandWithParameters::GetParameterInfo después de preparar el objeto de comando. Para los parámetros con valores de tabla, el *wType* miembro de la estructura DBPARAMINFO está establecido en DBTYPE_TABLE por el proveedor. El *ulParamSize* campo de la estructura DBPARAMINFO tiene un valor de ~ 0.  
  
 El consumidor solicitará a continuación propiedades adicionales (nombre de catálogo del tipo de parámetro con valores de tabla, nombre de esquema del tipo de parámetro con valores de tabla, nombre de tipo de parámetro con valores de tabla, ordenar las columnas y las columnas predeterminadas) utilizando ISSCommandWithParamters:: GetParameterProperties.  
  
 Después de que se conoce el nombre de tipo, para recuperar la información de columna individuales, el consumidor debe llamar a IOpenRowset::OpenRowsetor obtener el conjunto de filas DBSCHEMA_TABLE_TYPE_COLUMNS especificando el nombre del tipo de parámetro con valores de tabla como el nombre de tabla.  
  
## <a name="see-also"></a>Vea también  
 [Parámetros con valores de tabla &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar con valores de tabla parámetros & #40; OLE DB & #41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  

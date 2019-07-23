---
title: Procesando resultados | Microsoft Docs
description: Procesar resultados
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, results processing
- OLE DB, processing results
- rowsets [SQL Server], results processing
- results [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 9d29e75f75332f207c64a7b502e60300e9aae3d5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994973"
---
# <a name="processing-results"></a>Procesar los resultados (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Si se crea un objeto de conjunto de filas por la ejecución de un comando o por la generación de un objeto de conjunto de filas directamente del proveedor, el consumidor necesita recuperar y tener acceso a los datos del conjunto de filas.  
  
 Los conjuntos de filas son los objetos centrales que permiten al controlador de OLE DB para SQL Server exponer los datos en formato tabular. Conceptualmente, un conjunto de filas es un conjunto de filas en las que cada fila tiene datos de columna. Un objeto de conjunto de filas expone interfaces como **IRowset** (contiene los métodos para capturar secuencialmente las filas del conjunto de filas), **IAccessor** (permite la definición de un grupo de enlaces de columna que describen la manera en que los datos tabulares se enlazan a las variables de programa del consumidor), **IColumnsInfo** (proporciona información sobre las columnas en el conjunto de filas) e **IRowsetInfo** (proporciona información sobre el conjunto de filas).  
  
 Un consumidor puede llamar al método **IRowset::GetData** para recuperar una fila de datos del conjunto de filas en un búfer. Antes de llamar a **GetData**, el consumidor describe el búfer mediante un conjunto de estructuras DBBINDING. Cada enlace describe cómo una columna en un conjunto de filas se almacena en un búfer del consumidor y contiene lo siguiente:  
  
-   Ordinal de la columna (o parámetro) al que se aplica el enlace.  
  
-   Información acerca de qué se enlaza (por ejemplo, valor de los datos, longitud de los datos y su estado de enlace).  
  
-   Información acerca de qué se desplaza en el búfer a cada una de estas partes.  
  
-   La longitud y el tipo de los valores de datos tal y como existen en el búfer del consumidor.  
  
 Al obtener datos, el proveedor usa información en cada enlace para determinar donde y cómo recuperar los datos del búfer del consumidor. Al establecer datos en el búfer del consumidor, el proveedor usa información en cada enlace para determinar donde y cómo devolver los datos en el búfer del consumidor.  
  
 Una vez especificadas las estructuras DBBINDING, se crea un descriptor de acceso (**IAccessor::CreateAccessor**). Un descriptor de acceso es una colección de enlaces que se usa para obtener o establecer los datos en el búfer del consumidor.  
  
## <a name="see-also"></a>Consulte también  
 [Creación de un controlador OLE DB para la aplicación de SQL Server](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)   
 [Temas de procedimientos de OLE DB](../../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  

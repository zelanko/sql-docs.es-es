---
title: Procesar resultados | Documentos de Microsoft
description: Procesar resultados
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb-driver-for-sql-server
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, results processing
- OLE DB, processing results
- rowsets [SQL Server], results processing
- results [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 485e6303d2d27997f2ce6ee9c1b7619e8996dd04
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="processing-results"></a>Procesar los resultados (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Si se crea un objeto de conjunto de filas por la ejecución de un comando o por la generación de un objeto de conjunto de filas directamente del proveedor, el consumidor necesita recuperar y tener acceso a los datos del conjunto de filas.  
  
 Conjuntos de filas son los objetos centrales que permiten que el controlador OLE DB para SQL Server exponer los datos en formato tabular. Conceptualmente, un conjunto de filas es un conjunto de filas en las que cada fila tiene datos de columna. Un objeto de conjunto de filas expone interfaces como **IRowset** (contiene métodos para capturar secuencialmente las filas del conjunto de filas), **IAccessor** (permite la definición de un grupo de enlaces de columna que describe la forma datos tabulares se enlazan a variables de programa del consumidor), **IColumnsInfo** (proporciona información acerca de las columnas del conjunto de filas), y **IRowsetInfo** (proporciona información sobre el conjunto de filas).  
  
 Un consumidor puede llamar a la **IRowset:: GetData** método para recuperar una fila de datos del conjunto de filas en un búfer. Antes de **GetData** es llama, el consumidor describe el búfer mediante un conjunto de estructuras DBBINDING. Cada enlace describe cómo una columna en un conjunto de filas se almacena en un búfer del consumidor y contiene lo siguiente:  
  
-   Ordinal de la columna (o parámetro) al que se aplica el enlace.  
  
-   Información acerca de qué se enlaza (por ejemplo, valor de los datos, longitud de los datos y su estado de enlace).  
  
-   Información acerca de qué se desplaza en el búfer a cada una de estas partes.  
  
-   La longitud y el tipo de los valores de datos tal y como existen en el búfer del consumidor.  
  
 Al obtener datos, el proveedor usa información en cada enlace para determinar donde y cómo recuperar los datos del búfer del consumidor. Al establecer datos en el búfer del consumidor, el proveedor usa información en cada enlace para determinar donde y cómo devolver los datos en el búfer del consumidor.  
  
 Después de haber especifican las estructuras DBBINDING, se crea un descriptor de acceso (**IAccessor:: CreateAccessor**). Un descriptor de acceso es una colección de enlaces que se usa para obtener o establecer los datos en el búfer del consumidor.  
  
## <a name="see-also"></a>Vea también  
 [Crear un controlador OLE DB para la aplicación de SQL Server](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)   
 [Temas "Cómo..." de OLE DB](../../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  

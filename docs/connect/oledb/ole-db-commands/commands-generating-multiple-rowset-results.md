---
title: Comandos que generan resultados de varios conjuntos de filas | Documentos de Microsoft
description: Comandos que generan resultados de varios conjuntos de filas
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- OLE DB Driver for SQL Server, commands
- OLE DB Driver for SQL Server, multiple rowsets
- commands [OLE DB]
- multiple-rowset results
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: e0c3e581d5776e2f36756fc4bd09c1f76dd70841
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="commands-generating-multiple-rowset-results"></a>Comandos que generan resultados de varios conjuntos de filas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El controlador OLE DB para SQL Server puede devolver varios conjuntos de filas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instrucciones. Las instrucciones [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devuelven resultados de varios conjuntos de filas si se dan las condiciones siguientes:  
  
-   Las instrucciones SQL por lotes se envían como un comando único.  
  
-   Los procedimientos almacenados implementan un lote de instrucciones SQL.  
  
## <a name="batches"></a>Lotes  
 El controlador OLE DB para SQL Server reconoce el carácter de punto y coma como delimitador de lote de instrucciones SQL:  
  
```  
WCHAR*       wSQLString = L"SELECT * FROM Categories; "  
                          L"SELECT * FROM Products";  
```  
  
 El envío de varias instrucciones SQL en un lote es más eficaz que la ejecución de cada instrucción SQL por separado. Al enviar un lote, se reducen los viajes de ida y vuelta (round trip) del cliente al servidor en la red.  
  
## <a name="stored-procedures"></a>Procedimientos almacenados  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devuelve un conjunto de resultados para cada instrucción de un procedimiento almacenado, por lo que la mayoría de los procedimientos almacenados de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devuelven varios conjuntos de resultados.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Utilizar IMultipleResults para procesar varios conjuntos de resultados](../../oledb/ole-db-commands/using-imultipleresults-to-process-multiple-result-sets.md)  
  
## <a name="see-also"></a>Vea también  
 [Comandos](../../oledb/ole-db-commands/commands.md)  
  
  

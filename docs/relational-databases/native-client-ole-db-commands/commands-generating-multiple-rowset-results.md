---
title: Comandos que generan resultados de varios conjuntos de filas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- SQL Server Native Client OLE DB provider, commands
- SQL Server Native Client OLE DB provider, multiple rowsets
- commands [OLE DB]
- multiple-rowset results
ms.assetid: 4567668d-35fd-4162-b61f-f7536862cdcb
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 34c5eafbca22ba40cf1852220ab19cfad6452403
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37414867"
---
# <a name="commands-generating-multiple-rowset-results"></a>Comandos que generan resultados de varios conjuntos de filas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client puede devolver varios conjuntos de filas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instrucciones. Las instrucciones [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelven resultados de varios conjuntos de filas si se dan las condiciones siguientes:  
  
-   Las instrucciones SQL por lotes se envían como un comando único.  
  
-   Los procedimientos almacenados implementan un lote de instrucciones SQL.  
  
## <a name="batches"></a>Lotes  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client reconoce el carácter de punto y coma como delimitador de lote de instrucciones SQL:  
  
```  
WCHAR*       wSQLString = L"SELECT * FROM Categories; "  
                          L"SELECT * FROM Products";  
```  
  
 El envío de varias instrucciones SQL en un lote es más eficaz que la ejecución de cada instrucción SQL por separado. Al enviar un lote, se reducen los viajes de ida y vuelta (round trip) del cliente al servidor en la red.  
  
## <a name="stored-procedures"></a>Procedimientos almacenados  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve un conjunto de resultados para cada instrucción de un procedimiento almacenado, por lo que la mayoría de los procedimientos almacenados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelven varios conjuntos de resultados.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Utilizar IMultipleResults para procesar varios conjuntos de resultados](../../relational-databases/native-client-ole-db-commands/using-imultipleresults-to-process-multiple-result-sets.md)  
  
## <a name="see-also"></a>Vea también  
 [Comandos](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  

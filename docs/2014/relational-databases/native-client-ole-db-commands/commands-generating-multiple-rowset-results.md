---
title: Comandos que generan resultados de varios conjuntos de filas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
ms.openlocfilehash: 04a7db670171f6f890f55a89e2da987ef2309f0e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62657685"
---
# <a name="commands-generating-multiple-rowset-results"></a>Comandos que generan resultados de varios conjuntos de filas
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
  
-   [Utilizar IMultipleResults para procesar varios conjuntos de resultados](using-imultipleresults-to-process-multiple-result-sets.md)  
  
## <a name="see-also"></a>Vea también  
 [Comandos](commands.md)  
  
  

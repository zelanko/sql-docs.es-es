---
title: Comandos que generan resultados de varios conjuntos de filas | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
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
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: da8db391849392ccae05e3abb330fbfa112fcc49
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36110699"
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
  
  
---
title: "Conjuntos de resultados de automatización OLE | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-ole
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [SQL Server], OLE Automation
- two-dimensional arrays
- one-dimensional arrays
- result sets [SQL Server], OLE Automation
- OLE Automation [SQL Server], result sets
- arrays [SQL Server]
ms.assetid: b2f99e33-2303-427c-94b9-9d55f8e2a6ab
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8b3cf49bb4116a3cbf8bf58c327cdb6af5c11468
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="ole-automation-result-sets"></a>Conjuntos de resultados de automatización OLE
  Si una propiedad o método de automatización OLE devuelve datos en una matriz de una o dos dimensiones, la matriz se devuelve al cliente como un conjunto de resultados:  
  
-   Se devuelve al cliente una matriz unidimensional como conjunto de resultados de fila única con tantas columnas como elementos tenga la matriz. Por ejemplo, array(10) se devuelve como una fila única de 10 columnas.  
  
-   Se devuelve al cliente una matriz bidimensional como conjunto de resultados con tantas columnas como elementos haya en la primera dimensión de la matriz y con tantas filas como elementos haya en la segunda dimensión de la matriz. Por ejemplo, array(2,3) se devuelve como 2 columnas en 3 filas.  
  
 Cuando un valor devuelto por una propiedad o por un método es una matriz, sp_OAGetProperty o sp_OAMethod devuelven un conjunto de resultados al cliente. (Los parámetros de salida del método no pueden ser matrices.) Estos procedimientos recorren todos los valores de datos de la matriz para determinar los tipos de datos y las longitudes de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] adecuados para cada columna del conjunto de resultados. Para una columna determinada, estos procedimientos utilizan el tipo y la longitud de datos necesarios para representar todos los valores de los datos de la columna.  
  
 Cuando todos los valores de datos de una columna comparten el mismo tipo de datos, se utiliza ese tipo para toda la columna. Cuando los valores de datos de una columna son tipos de datos diferentes, el tipo de datos de toda la columna se elige según la tabla siguiente. Para utilizar la tabla siguiente, busque un tipo de datos a lo largo del eje de la fila izquierdo y un segundo tipo de datos a lo largo del eje de la columna superior. La intersección de la fila y columna describe el tipo de datos de la columna del conjunto de resultados.  
  
||||||||  
|-|-|-|-|-|-|-|  
||**int**|**float**|**money**|**datetime**|**varchar**|**nvarchar**|  
|**int**|**int**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**float**|**float**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**money**|**money**|**money**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**datetime**|**varchar**|**varchar**|**varchar**|**datetime**|**varchar**|**nvarchar**|  
|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**nvarchar**|  
|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|  
  
## <a name="related-content"></a>Contenido relacionado  
 [Procedimientos almacenados de automatización OLE &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
  
 [Ole Automation Procedures (opción de configuración del servidor)](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)  
  
  


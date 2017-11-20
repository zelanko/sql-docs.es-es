---
title: Metadatos del conjunto de resultado | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 6d134515-e34d-4563-96d7-8ad7714818fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0f5de9f9b5b2a6da81fa175f24cd5bdf1b14e6e8
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="result-set-metadata"></a>Metadatos del conjunto de resultados
*Metadatos* son datos que describen otros datos. Por ejemplo, los metadatos del conjunto de resultados describen el conjunto de resultados, como el número de columnas del conjunto de resultados, los tipos de datos de esas columnas, sus nombres, precisión, nulabilidad y así sucesivamente.  
  
 Aplicaciones interoperables deben comprobar siempre los metadatos de columnas del conjunto de resultados. Los metadatos de una columna en un conjunto de resultados pueden diferir de los metadatos de la columna devuelta por una función de catálogo. Por ejemplo, suponga que una columna actualizable se incluye en un conjunto de resultados que se crean mediante la combinación de dos tablas. Mientras **SQLColumnPrivileges** puede indicar que un usuario puede actualizar la columna, los metadatos del conjunto de resultados podrían no si la columna se encuentra en el lado "varios" de la combinación; muchos orígenes de datos pueden actualizarse las columnas en el lado "uno" de una combinación, pero no en la " lado "varios" ". Incluso los tipos de datos no se puede suponer que para ser el mismo, porque el origen de datos puede promover el tipo de datos al crear el conjunto de resultados.  
  
 Esta sección contiene los temas siguientes.  
  
-   [¿Forma de metadatos utiliza?](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol y SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)


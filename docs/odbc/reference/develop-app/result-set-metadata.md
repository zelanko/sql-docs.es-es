---
title: Como resultado de los metadatos del conjunto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 6d134515-e34d-4563-96d7-8ad7714818fd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7dc88892fab2fd18dbcbec5ce54fa09c9c9b89e7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199381"
---
# <a name="result-set-metadata"></a>Metadatos del conjunto de resultados
*Metadatos* son datos que describen otros datos. Por ejemplo, los metadatos del conjunto de resultados describen el conjunto de resultados, como el número de columnas del conjunto de resultados, los tipos de datos de esas columnas, sus nombres, precisión, nulabilidad y así sucesivamente.  
  
 Aplicaciones interoperables siempre deberían comprobar los metadatos de columnas del conjunto de resultados. Los metadatos de una columna en un conjunto de resultados pueden diferir de los metadatos de la columna devuelta por una función de catálogo. Por ejemplo, suponga que una columna actualizable se incluye en un conjunto de resultados creado mediante la combinación de dos tablas. Mientras **SQLColumnPrivileges** podría indicar que un usuario puede actualizar la columna, los metadatos del conjunto de resultados podrían no si la columna se encuentra en el lado "varios" de la combinación; muchos orígenes de datos pueden actualizar las columnas del lado "uno" de una combinación, pero no en el " lado "varios" ". Incluso los tipos de datos no se puede suponer que para ser el mismo, porque el origen de datos puede promover el tipo de datos al crear el conjunto de resultados.  
  
 Esta sección contiene los temas siguientes.  
  
-   [¿Forma de metadatos utiliza?](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol y SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)

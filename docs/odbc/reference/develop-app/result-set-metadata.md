---
title: Metadatos del conjunto de resultados | Microsoft Docs
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
ms.openlocfilehash: 1d8da8c15c861fff4767aa598e1b989d8f699c95
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020587"
---
# <a name="result-set-metadata"></a>Metadatos del conjunto de resultados
Los metadatos *son datos* que describen otros datos. Por ejemplo, los metadatos del conjunto de resultados describen el conjunto de resultados, como el número de columnas del conjunto de resultados, los tipos de datos de esas columnas, sus nombres, precisión, nulabilidad, etc.  
  
 Las aplicaciones interoperables siempre deben comprobar los metadatos de las columnas del conjunto de resultados. Los metadatos de una columna de un conjunto de resultados pueden diferir de los metadatos de la columna devueltos por una función de catálogo. Por ejemplo, supongamos que una columna actualizable se incluye en un conjunto de resultados creado mediante la combinación de dos tablas. Aunque **SQLColumnPrivileges** puede indicar que un usuario puede actualizar la columna, los metadatos del conjunto de resultados podrían no ser si la columna está en el lado "varios" de la combinación; muchos orígenes de datos pueden actualizar columnas en el lado "uno" de una combinación, pero no en el lado "varios". Incluso no se puede suponer que los tipos de datos son iguales, porque el origen de datos podría promover el tipo de datos al crear el conjunto de resultados.  
  
 Esta sección contiene los temas siguientes.  
  
-   [¿Forma de metadatos utiliza?](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol y SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)

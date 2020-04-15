---
title: Metadatos del conjunto de resultados ( Result Set Metadata) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b78cdeb4c8b3522f4677c0277401cd9395a36a5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300085"
---
# <a name="result-set-metadata"></a>Metadatos del conjunto de resultados
*Los metadatos* son datos que describen otros datos. Por ejemplo, los metadatos del conjunto de resultados describen el conjunto de resultados, como el número de columnas del conjunto de resultados, los tipos de datos de esas columnas, sus nombres, precisión, nulabilidad, etc.  
  
 Las aplicaciones interoperables siempre deben comprobar los metadatos de las columnas del conjunto de resultados. Los metadatos de una columna de un conjunto de resultados pueden diferir de los metadatos de la columna devueltos por una función de catálogo. Por ejemplo, supongamos que una columna actualizable se incluye en un conjunto de resultados creado mediante la unión de dos tablas. Aunque **SQLColumnPrivileges** puede indicar que un usuario puede actualizar la columna, es posible que los metadatos del conjunto de resultados no si la columna está en el lado "muchos" de la combinación; muchos orígenes de datos pueden actualizar columnas en el lado "uno" de una combinación, pero no en el lado "muchos". Incluso los tipos de datos no se puede suponer que sean los mismos, porque el origen de datos podría promover el tipo de datos al crear el conjunto de resultados.  
  
 Esta sección contiene los temas siguientes.  
  
-   [¿Forma de metadatos utiliza?](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol y SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)

---
title: Limitaciones del uso de cursores controlados por conjuntos de claves Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], cursors
- keyset-driven cursors [ODBC]
ms.assetid: 59d86fed-387c-4719-9550-36343e74da44
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2aeb5a0c50192118dfff8ed7d866c3911c2b4007
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284155"
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>Limitaciones del uso de los cursores controlados por conjunto de claves
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Debe poder recuperar una sola columna ROWID para la tabla consultada. Un cursor controlado por conjunto de claves no se puede utilizar en combinaciones, consultas o instrucciones que contengan cláusulas DISTINCT, GROUP BY, UNION, INTERSECT o MINUS.  
  
 Además, si la aplicación utiliza alias de tabla, los cursores controlados por conjuntos de claves no funcionarán; Se requieren tipos de cursor estáticos o de solo avance. El uso del tipo de cursor de conjunto de claves con alias de tabla provocará el siguiente error: "[Microsoft][controlador ODBC para Oracle]No se puede utilizar el cursor controlado por conjunto de claves en la combinación, con unión, intersección o menos o en conjunto de resultados de solo lectura."  
  
> [!NOTE]  
>  Debido a la forma en que el controlador controla la instrucción SQL que se envía al servidor de Oracle, Oracle devuelve internamente el siguiente mensaje de error: "ORA-00964: nombre de tabla no en la lista FROM."

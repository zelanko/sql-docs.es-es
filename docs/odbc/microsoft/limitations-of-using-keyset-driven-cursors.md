---
title: Limitaciones del uso de cursores controlados por conjunto de claves | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284155"
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>Limitaciones del uso de los cursores controlados por conjunto de claves
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Debe poder recuperar una sola columna ROWID para la tabla consultada. No se puede usar un cursor controlado por conjunto de claves en combinaciones, consultas o instrucciones que contengan cláusulas DISTINCt, GROUP BY, UNION, INTERSECT o MINUs.  
  
 Además, si la aplicación utiliza alias de tabla, los cursores controlados por conjunto de claves no funcionarán. se requieren tipos de cursor de solo avance o estáticos. El uso del tipo de cursor de conjunto de claves con alias de tabla producirá el siguiente error: "[Microsoft] [controlador ODBC para Oracle] no puede usar un cursor controlado por conjunto de claves en la combinación, con Union, Intersect o minu o en un conjunto de resultados de solo lectura".  
  
> [!NOTE]  
>  Debido a la forma en que el controlador controla la instrucción SQL que se envía al servidor de Oracle, Oracle devuelve internamente el siguiente mensaje de error: "ORA-00964: el nombre de la tabla no está en la lista".

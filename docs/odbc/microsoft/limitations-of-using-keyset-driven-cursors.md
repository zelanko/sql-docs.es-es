---
title: Limitaciones del uso de los cursores dinámicos | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c4910ebd2c6dd988e937f1e9d6a3281bb0e9741
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47668113"
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>Limitaciones del uso de los cursores controlados por conjunto de claves
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el controlador ODBC proporcionado por Oracle.  
  
 Debe ser capaz de recuperar una sola columna ROWID para la tabla consultada. No se puede usar un cursor controlado por conjunto de claves en combinaciones, las consultas o instrucciones que contienen DISTINCT, GROUP BY, UNION, INTERSECT o menos cláusulas.  
  
 Además, si la aplicación usa los alias de tabla, los cursores dinámicos no funcionará; se requieren tipos de cursor estático o de solo avance. Mediante el conjunto de claves, el tipo de cursor con alias de tabla provocará el siguiente error: "[Microsoft] [controlador ODBC para Oracle] no puede usar cursores dinámicos en una combinación con union, intersect o menos, o de solo lectura de conjunto de resultados."  
  
> [!NOTE]  
>  Debido al modo en que el controlador controla la instrucción SQL que se envía al servidor de Oracle, Oracle internamente devuelve el siguiente mensaje de error: "ORA-00964: tabla nombre no está en el de la lista."

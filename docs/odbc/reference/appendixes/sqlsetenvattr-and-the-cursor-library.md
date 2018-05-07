---
title: SQLSetEnvAttr y la biblioteca de cursores | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC], Cursor Library
ms.assetid: 59cc8eae-09ae-4796-869a-c5806488ae83
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 11e0e7d0925b6e5e72965e93cf48f7eae7793df1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetenvattr-and-the-cursor-library"></a>SQLSetEnvAttr y la biblioteca de cursores
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Este tema describe el uso de la **SQLSetEnvAttr** función con la biblioteca de cursores. Para obtener información general sobre **SQLSetEnvAttr**, consulte [función SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
 La biblioteca de cursores no se ve afectada por el valor del atributo entorno SQL_ATTR_ODBC_VERSION, independientemente de la versión de la aplicación o la versión del controlador.

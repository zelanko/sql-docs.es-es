---
title: SQLExtendedFetch (controlador ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b28af112-fb47-4143-b11e-3b743b2ae1b8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2d01c25044bf7b03e2fabe9c615668fc7837312
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47667159"
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: completo  
  
 Conformidad de la API de ODBC: 2 de nivel  
  
 Similar a [SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) pero devuelve varias filas utilizando una matriz para cada columna. El conjunto de resultados es desplazable de avance y se puede realizar con versiones anteriores desplazable si el cursor se define como estático, no sólo hacia delante.  
  
 De forma predeterminada, el controlador ODBC de Visual FoxPro no devuelve las filas marcadas como eliminadas en una tabla de FoxPro. No se incluyen filas marcados para su eliminación pero todavía no se han quitado de una tabla en el cursor de conjunto de resultados. Puede cambiar este comportamiento mediante la [SET DELETED](../../odbc/microsoft/set-deleted-command.md) comando.  
  
 Para obtener más información, consulte [SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md) en el *referencia del programador de ODBC*.

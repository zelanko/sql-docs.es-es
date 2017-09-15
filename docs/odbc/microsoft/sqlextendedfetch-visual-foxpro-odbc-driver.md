---
title: SQLExtendedFetch (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b28af112-fb47-4143-b11e-3b743b2ae1b8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 25a9e0b16551ca27a6818fcfd890e56aeabfb44b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: completo  
  
 Conformidad de la API de ODBC: 2 de nivel  
  
 Similar a [SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) pero devuelve varias filas utilizando una matriz para cada columna. El conjunto de resultados se puede desplazar hacia delante y puede realizarse con versiones anteriores desplazable si el cursor se define como estático, no de solo avance.  
  
 De forma predeterminada, el controlador ODBC de Visual FoxPro no devuelve filas marcadas como eliminadas de una tabla de FoxPro. Filas marcados para su eliminación pero no se han quitado de una tabla no se incluyen en el cursor de conjunto de resultados. Puede cambiar este comportamiento mediante la [SET DELETED](../../odbc/microsoft/set-deleted-command.md) comando.  
  
 Para obtener más información, consulte [SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md) en el *referencia del programador de ODBC*.

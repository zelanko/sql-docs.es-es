---
title: SQLExtendedFetch (Controlador ODBC de Visual FoxPro) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ecff538198a2b517f980cc63acfc97d29a9f162
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298655"
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte: Completo  
  
 Conformidad de la API ODBC: Nivel 2  
  
 Similar a [SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) pero devuelve varias filas mediante una matriz para cada columna. El conjunto de resultados se puede desplazar hacia delante y se puede hacer desplazable hacia atrás si el cursor se define como estático, no de solo avance.  
  
 De forma predeterminada, el controlador ODBC de Visual FoxPro no devuelve filas marcadas como eliminadas en una tabla FoxPro. Las filas marcadas para su eliminación pero aún no eliminadas de una tabla no se incluyen en el cursor del conjunto de resultados. Puede cambiar este comportamiento mediante el comando [SET DELETED.](../../odbc/microsoft/set-deleted-command.md)  
  
 Para obtener más información, vea [SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md) en la *referencia del programador ODBC*.

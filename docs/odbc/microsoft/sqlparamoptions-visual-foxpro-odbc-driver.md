---
title: SQLParamOptions (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLParamOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 7f94a6e2-9c34-405c-b2b0-304d94269715
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cb73b760a0d63dcf1aa57ea0448dece6cb58b3f2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqlparamoptions-visual-foxpro-odbc-driver"></a>SQLParamOptions (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: completo  
  
 Ajuste de la API de ODBC: Nivel 1  
  
 Permite que una aplicación especificar varios valores para el conjunto de parámetros asignados por [SQLBindParameter](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md). La capacidad de especificar varios valores para un conjunto de parámetros es útil para las inserciones masivas y otro trabajo que requiere el origen de datos para procesar la misma instrucción SQL varias veces con distintos valores de parámetro. Por ejemplo, una aplicación puede especificar tres conjuntos de valores para el conjunto de parámetros asociados a un **insertar** instrucción y, a continuación, ejecute el **insertar** instrucción una sola vez para realizar las tres insertar operaciones.  
  
 Para obtener más información, consulte [SQLParamOptions](../../odbc/reference/syntax/sqlparamoptions-function.md) en el *referencia del programador de ODBC*.

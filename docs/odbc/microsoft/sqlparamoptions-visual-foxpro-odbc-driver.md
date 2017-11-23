---
title: SQLParamOptions (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLParamOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 7f94a6e2-9c34-405c-b2b0-304d94269715
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 47dc4be8925623a9dad87f1f7233211956ea5b67
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sqlparamoptions-visual-foxpro-odbc-driver"></a>SQLParamOptions (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: completo  
  
 Ajuste de la API de ODBC: Nivel 1  
  
 Permite que una aplicación especificar varios valores para el conjunto de parámetros asignados por [SQLBindParameter](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md). La capacidad de especificar varios valores para un conjunto de parámetros es útil para las inserciones masivas y otro trabajo que requiere el origen de datos para procesar la misma instrucción SQL varias veces con distintos valores de parámetro. Por ejemplo, una aplicación puede especificar tres conjuntos de valores para el conjunto de parámetros asociados a un **insertar** instrucción y, a continuación, ejecute el **insertar** instrucción una sola vez para realizar las tres insertar operaciones.  
  
 Para obtener más información, consulte [SQLParamOptions](../../odbc/reference/syntax/sqlparamoptions-function.md) en el *referencia del programador de ODBC*.

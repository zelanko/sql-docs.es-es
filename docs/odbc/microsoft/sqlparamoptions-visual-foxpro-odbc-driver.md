---
title: SQLParamOptions (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
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
- SQLParamOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 7f94a6e2-9c34-405c-b2b0-304d94269715
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 17a82974d8531d0524f4bac89701d6c97a05198d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlparamoptions-visual-foxpro-odbc-driver"></a>SQLParamOptions (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: completo  
  
 Ajuste de la API de ODBC: Nivel 1  
  
 Permite que una aplicación especificar varios valores para el conjunto de parámetros asignados por [SQLBindParameter](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md). La capacidad de especificar varios valores para un conjunto de parámetros es útil para las inserciones masivas y otro trabajo que requiere el origen de datos para procesar la misma instrucción SQL varias veces con distintos valores de parámetro. Por ejemplo, una aplicación puede especificar tres conjuntos de valores para el conjunto de parámetros asociados a un **insertar** instrucción y, a continuación, ejecute el **insertar** instrucción una sola vez para realizar las tres insertar operaciones.  
  
 Para obtener más información, consulte [SQLParamOptions](../../odbc/reference/syntax/sqlparamoptions-function.md) en el *referencia del programador de ODBC*.

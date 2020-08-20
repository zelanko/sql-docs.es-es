---
description: Tipos de datos admitidos (controlador ODBC de Visual FoxPro)
title: Tipos de datos admitidos (controlador ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], data types
- FoxPro ODBC driver [ODBC], data types
- data types [ODBC], Visual FoxPro ODBC driver
ms.assetid: ab529cc6-d157-4b35-b6f9-6ffd09af098c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 04f2039d18f134fe2c48397f6c0dc987e97bf47d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471527"
---
# <a name="supported-data-types-visual-foxpro-odbc-driver"></a>Tipos de datos admitidos (controlador ODBC de Visual FoxPro)
La lista de tipos de datos admitidos por el controlador se presenta a través de la API de ODBC y en Microsoft Query.  
  
## <a name="data-types-in-c-applications"></a>Tipos de datos en aplicaciones de C  
 Puede obtener una lista de tipos de datos admitidos por el controlador ODBC de Visual FoxPro mediante la función [SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md) en aplicaciones de C o C++.  
  
## <a name="data-types-in-applications-using-microsoft-query"></a>Tipos de datos en aplicaciones que usan Microsoft Query  
 Si la aplicación usa Microsoft Query para crear una nueva tabla en un origen de datos de Visual FoxPro, Microsoft Query muestra el cuadro de diálogo **nueva definición de tabla** . En **Descripción de campo**, el cuadro **tipo** muestra los tipos de datos de [campo de Visual FoxPro](../../odbc/microsoft/visual-foxpro-field-data-types.md), representados por caracteres individuales.

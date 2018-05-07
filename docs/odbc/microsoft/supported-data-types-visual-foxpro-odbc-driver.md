---
title: Admite los tipos de datos (el controlador ODBC de Visual FoxPro) | Documentos de Microsoft
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
- Visual FoxPro ODBC driver [ODBC], data types
- FoxPro ODBC driver [ODBC], data types
- data types [ODBC], Visual FoxPro ODBC driver
ms.assetid: ab529cc6-d157-4b35-b6f9-6ffd09af098c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 030bcc12bb8790f133af3e265cf26ffba2d23573
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="supported-data-types-visual-foxpro-odbc-driver"></a>Tipos de datos admitidos (controlador ODBC de Visual FoxPro)
La lista de tipos de datos admitidos por el controlador se presentan a través de la API de ODBC y Microsoft Query.  
  
## <a name="data-types-in-c-applications"></a>Tipos de datos en aplicaciones de C  
 Puede obtener una lista de tipos de datos admitidos por el controlador ODBC de Visual FoxPro utilizando la [SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md) función en aplicaciones de C o C++.  
  
## <a name="data-types-in-applications-using-microsoft-query"></a>Tipos de datos en las aplicaciones que usan Microsoft Query  
 Si la aplicación utiliza Microsoft Query para crear una nueva tabla en un origen de datos de Visual FoxPro, Microsoft Query muestra el **nueva definición de tabla** cuadro de diálogo. En **campo Descripción**, **tipo** cuadro listas [tipos de datos de campo Visual FoxPro](../../odbc/microsoft/visual-foxpro-field-data-types.md), representado por caracteres individuales.

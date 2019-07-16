---
title: Mensajes de error (controlador ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error messages [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], error messages
- SQLSTATE [ODBC]
- FoxPro ODBC driver [ODBC], error messages
ms.assetid: 58ea9734-4edf-44da-ba80-938aa7b340e4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6072a6e317ab87118376b08790fc0fb49c495e3b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952515"
---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>Mensajes de error (el controlador ODBC de Visual FoxPro)
Cuando se produce un error, el controlador de Visual FoxPro devuelve la siguiente información:  
  
-   El número de error nativo y el texto del mensaje de error  
  
-   SQLSTATE (un código de error ODBC) y el texto del mensaje de error  
  
 Obtener acceso a esta información de error mediante una llamada a [SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md).  
  
## <a name="native-errors"></a>Errores nativos  
 Para los errores que se producen en el origen de datos, el controlador de Visual FoxPro devuelve el número de error nativo y el texto del mensaje de error. Para obtener una lista de números de errores nativos, vea [Visual FoxPro ODBC Driver nativo mensajes](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md).  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (códigos de error ODBC)  
 El controlador de errores que se detectan y devueltos por el controlador de Visual FoxPro, asigna el número de error nativo devuelto al SQLSTATE correspondiente. Si un número de error nativo no tiene un código de error ODBC para asignar a, el controlador de Visual FoxPro devuelve SQLSTATE S1000 (error General).  
  
 Para obtener una lista de valores SQLSTATE generados por el controlador ODBC de Visual FoxPro para errores de Visual FoxPro correspondientes, consulte [códigos de Error ODBC](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md).  
  
## <a name="syntax"></a>Sintaxis  
 Los mensajes de error tienen el formato siguiente:  
  
 **[** *vendor* **][** *ODBC_component* **]** *error_message*  
  
 Los prefijos de corchetes ([]) identifican el origen del error, tal como se define en la tabla siguiente.  
  
|Origen de datos|Prefijo|Valor|  
|-----------------|------------|-----------|  
|Administrador de controladores|[proveedor]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[Administrador de controladores ODBC]<br />N/D|  
|Controlador de Visual FoxPro|proveedor]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[Controlador ODBC de Visual FoxPro]<br />N/D|  
  
 Por ejemplo, si el controlador ODBC de Visual FoxPro no se pudo encontrar el archivo employee.dbf, podría devolver el mensaje de error siguiente:  
  
 "[*Microsoft*] [*controlador ODBC de Visual FoxPro*] no existe el archivo 'employee.dbf'"

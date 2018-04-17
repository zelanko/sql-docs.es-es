---
title: Mensajes de error (el controlador ODBC de Visual FoxPro) | Documentos de Microsoft
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
- error messages [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], error messages
- SQLSTATE [ODBC]
- FoxPro ODBC driver [ODBC], error messages
ms.assetid: 58ea9734-4edf-44da-ba80-938aa7b340e4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0d8bb313af52507b1b14cd085044c334f3e664f0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>Mensajes de error (el controlador ODBC de Visual FoxPro)
Cuando se produce un error, el controlador de Visual FoxPro devuelve la siguiente información:  
  
-   El número de error nativo y el texto del mensaje de error  
  
-   SQLSTATE (un código de error ODBC) y el texto del mensaje de error  
  
 Acceso a esta información de error llamando [SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md).  
  
## <a name="native-errors"></a>Errores nativos  
 Para los errores que se producen en el origen de datos, el controlador de Visual FoxPro devuelve el número de error nativo y el texto del mensaje de error. Para obtener una lista de números de errores nativos, vea [Visual FoxPro ODBC Driver nativo mensajes](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md).  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (códigos de error ODBC)  
 Para los errores que se detectan y se devuelve el controlador de Visual FoxPro, el controlador asigna el número de error nativo devuelto al SQLSTATE correspondiente. Si un número de error nativo no tiene un código de error ODBC para asignar a, el controlador de Visual FoxPro devuelve SQLSTATE S1000 (error General).  
  
 Para obtener una lista de valores SQLSTATE generados por el controlador ODBC de Visual FoxPro para errores de Visual FoxPro correspondientes, consulte [códigos de Error de ODBC](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md).  
  
## <a name="syntax"></a>Sintaxis  
 Mensajes de error tienen el formato siguiente:  
  
 **[** *proveedor* **] [** *ODBC_component* **]** *error_message*  
  
 Los prefijos de corchetes ([]) identifican el origen del error, tal como se define en la tabla siguiente.  
  
|Origen de datos|Prefijo|Value|  
|-----------------|------------|-----------|  
|Administrador de controladores|[proveedor]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[Administrador de controladores ODBC]<br />N/D|  
|Controlador de Visual FoxPro|proveedor]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[Controlador ODBC de Visual FoxPro]<br />N/D|  
  
 Por ejemplo, si el controlador ODBC de Visual FoxPro no se pudo encontrar el archivo employee.dbf, podría devolver el mensaje de error siguiente:  
  
 "[*Microsoft*] [*controlador ODBC de Visual FoxPro*] no existe el archivo 'employee.dbf'"

---
title: Mensajes de error (controlador ODBC de Visual FoxPro) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31f894e58da93fe6091dba306f8b765d14bac2cb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286405"
---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>Mensajes de error (el controlador ODBC de Visual FoxPro)
Cuando se produce un error, el controlador de Visual FoxPro devuelve la siguiente información:  
  
-   El número de error nativo y el texto del mensaje de error  
  
-   SQLSTATE (un código de error ODBC) y el texto del mensaje de error  
  
 Puede acceder a esta información de error llamando a [SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md).  
  
## <a name="native-errors"></a>Errores nativos  
 Para los errores que se producen en el origen de datos, el controlador de Visual FoxPro devuelve el número de error nativo y el texto del mensaje de error. Para obtener una lista de números de error nativos, vea Mensajes de [error nativos del controlador ODBC](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)de Visual FoxPro .  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (códigos de error ODBC)  
 Para los errores detectados y devueltos por el controlador de Visual FoxPro, el controlador asigna el número de error nativo devuelto al SQLSTATE adecuado. Si un número de error nativo no tiene un código de error ODBC al que asignarse, el controlador de Visual FoxPro devuelve SQLSTATE S1000 (error general).  
  
 Para obtener una lista de los valores SQLSTATE generados por el controlador ODBC de Visual FoxPro para los errores de Visual FoxPro correspondientes, vea [Códigos](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)de error ODBC .  
  
## <a name="syntax"></a>Sintaxis  
 Los mensajes de error tienen el siguiente formato:  
  
 **[** *proveedor* **][** *ODBC_component* **]** *error_message*  
  
 Los prefijos entre corchetes ([ ]) identifican el origen del error tal como se define en la tabla siguiente.  
  
|Origen de datos|Prefijo|Value|  
|-----------------|------------|-----------|  
|Administrador de controladores|[proveedor]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[Administrador de controladores ODBC]<br />N/D|  
|Controlador Visual FoxPro|proveedor]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[Controlador ODBC Visual FoxPro]<br />N/D|  
  
 Por ejemplo, si el controlador ODBC de Visual FoxPro no pudo encontrar el archivo employee.dbf, podría devolver el siguiente mensaje de error:  
  
 "[*Microsoft*][*ODBC Visual FoxPro Driver*]El archivo 'employee.dbf' no existe"

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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31f894e58da93fe6091dba306f8b765d14bac2cb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286405"
---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>Mensajes de error (el controlador ODBC de Visual FoxPro)
Cuando se produce un error, el controlador de Visual FoxPro devuelve la siguiente información:  
  
-   El número de error nativo y el texto del mensaje de error  
  
-   SQLSTATE (código de error ODBC) y texto del mensaje de error  
  
 Para obtener acceso a esta información de error, se llama a [SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md).  
  
## <a name="native-errors"></a>Errores nativos  
 En el caso de los errores que se producen en el origen de datos, el controlador de Visual FoxPro devuelve el número de error nativo y el texto del mensaje de error. Para obtener una lista de números de error nativos, consulte [los mensajes de error nativos del controlador ODBC de Visual FoxPro](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md).  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (códigos de error ODBC)  
 En el caso de los errores detectados y devueltos por el controlador de Visual FoxPro, el controlador asigna el número de error nativo devuelto al SQLSTATE adecuado. Si un número de error nativo no tiene un código de error ODBC al que asignar, el controlador de Visual FoxPro devuelve SQLSTATE S1000 (error general).  
  
 Para obtener una lista de los valores SQLSTATE generados por el controlador ODBC de Visual FoxPro para los errores de Visual FoxPro correspondientes, vea [códigos de error ODBC](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md).  
  
## <a name="syntax"></a>Sintaxis  
 Los mensajes de error tienen el siguiente formato:  
  
 **[** *proveedor* **] [** *ODBC_component* **]** *error_message*  
  
 Los prefijos entre corchetes ([]) identifican el origen del error tal y como se define en la tabla siguiente.  
  
|Origen de datos|Prefijo|Value|  
|-----------------|------------|-----------|  
|Administrador de controladores|proveedor<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[Administrador de controladores ODBC]<br />N/D|  
|Controlador de Visual FoxPro|proveedor<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[Controlador ODBC para Visual FoxPro]<br />N/D|  
  
 Por ejemplo, si el controlador ODBC de Visual FoxPro no encontró el archivo Employee. DBF, podría devolver el mensaje de error siguiente:  
  
 "[*Microsoft*] [*controlador ODBC para Visual FoxPro*] el archivo ' Employee. DBF ' no existe

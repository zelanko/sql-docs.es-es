---
title: SQLGetConnectOption (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
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
- SQLGetConnectOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5703eb39-f3b2-4f3a-8676-a5625ae29a41
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fd94e03f54eda8af1c7199bcf6d716e20af70a5b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetconnectoption-visual-foxpro-odbc-driver"></a>SQLGetConnectOption (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: parcial  
  
 Ajuste de la API de ODBC: Nivel 1  
  
 Devuelve el valor actual de una opción de conexión. Esta función se admite parcialmente: el controlador es compatible con todos los valores para la *fOption* argumento pero no es compatible con algunos de *vParam* los valores para la *fOption* argumento SQL_TXN_ISOLATION.  
  
 La tabla siguiente describen solo los argumentos con comportamiento específico de la implementación del controlador ODBC de Visual FoxPro de **SQLGetConnectOption**.  
  
|*fOption*|Comentarios|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|Si elige SQL_AUTOCOMMIT_OFF, la aplicación debe confirmar o revertir las transacciones con explícitamente [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); el controlador ODBC de Visual FoxPro no confirma automáticamente una instrucción permiten transacciones tras la finalización. El controlador de iniciar una transacción si la instrucción se permiten transacciones.|  
|SQL_CURRENT_QUALIFIER|Puede ser un nombre de base de datos completo (archivo .dbc) o la ruta de acceso completa a un directorio que contiene cero o más tablas (archivos .dbf).|  
|SQL_LOGINTIMEOUT|Devuelve el error "Controladores no compatibles con".|  
|SQL_CURSORS|Devuelve el error "Controladores no compatibles con".|  
|SQL_PACKET_SIZE|Devuelve el error "Controladores no compatibles con".|  
|SQL_TXN_ISOLATION|El controlador permite solo SQL_TXN_READ_COMMITTED.<br /><br /> El siguiente *vParam*no son compatibles:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 Para obtener más información, consulte [SQLGetConnectOption](../../odbc/reference/syntax/sqlgetconnectoption-function.md) en el *referencia del programador de ODBC*.

---
title: SQLGetConnectOption (Controlador ODBC de Visual FoxPro) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetConnectOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5703eb39-f3b2-4f3a-8676-a5625ae29a41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2dd801988343ded46305665ab2a99aa4e7d76cba
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298635"
---
# <a name="sqlgetconnectoption-visual-foxpro-odbc-driver"></a>SQLGetConnectOption (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte: Parcial  
  
 Conformidad de la API ODBC: Nivel 1  
  
 Devuelve la configuración actual de una opción de conexión. Esta función se admite parcialmente: el controlador admite todos los valores para el argumento *fOption,* pero no admite algunos de los valores *vParam* para el argumento *fOption* SQL_TXN_ISOLATION.  
  
 En la tabla siguiente se describen solo los argumentos con un comportamiento específico de la implementación del controlador ODBC de Visual FoxPro de **SQLGetConnectOption**.  
  
|*fOption*|Observaciones|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|Si elige SQL_AUTOCOMMIT_OFF, la aplicación debe confirmar o revertir explícitamente transacciones con [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); el controlador ODBC de Visual FoxPro no confirma automáticamente una instrucción transactable al finalizar. El controlador inicia una transacción si la instrucción es transaccionable.|  
|SQL_CURRENT_QUALIFIER|Puede ser un nombre de base de datos completo (archivo .dbc) o una ruta de acceso completa a un directorio que contenga cero o más tablas (archivos .dbf).|  
|SQL_LOGINTIMEOUT|Devuelve el error "Driver Not Capable".|  
|SQL_CURSORS|Devuelve el error "Driver Not Capable".|  
|SQL_PACKET_SIZE|Devuelve el error "Driver Not Capable".|  
|SQL_TXN_ISOLATION|El controlador sólo permite SQL_TXN_READ_COMMITTED.<br /><br /> No se admiten las siguientes *vParam*s:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 Para obtener más información, vea [SQLGetConnectOption](../../odbc/reference/syntax/sqlgetconnectoption-function.md) en la *referencia del programador ODBC*.

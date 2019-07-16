---
title: SQLGetConnectOption (controlador ODBC de Visual FoxPro) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c17cd473d3c96032817c2b183bf65fe360cf3cdc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053684"
---
# <a name="sqlgetconnectoption-visual-foxpro-odbc-driver"></a>SQLGetConnectOption (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: Parcial  
  
 Conformidad de la API de ODBC: Nivel 1  
  
 Devuelve el valor actual de una opción de conexión. Esta función se admite parcialmente: El controlador es compatible con todos los valores para el *fOption* argumento pero no admite algunos de *vParam* valores para el *fOption* argumento SQL_TXN_ISOLATION.  
  
 En la tabla siguiente se describe solo esos argumentos con el comportamiento específico de la implementación del controlador ODBC de Visual FoxPro de **SQLGetConnectOption**.  
  
|*fOption*|Comentarios|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|Si elige SQL_AUTOCOMMIT_OFF, la aplicación debe confirmar o revertir las transacciones con explícitamente [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); el controlador ODBC de Visual FoxPro no confirma automáticamente una instrucción permiten transacciones tras la finalización. El controlador de iniciar una transacción si la instrucción se permiten transacciones.|  
|SQL_CURRENT_QUALIFIER|Puede ser un nombre de base de datos completo (archivo .dbc) o la ruta de acceso completa a un directorio que contiene cero o más tablas (archivos).|  
|SQL_LOGINTIMEOUT|Devuelve el error "Controladores no compatibles con".|  
|SQL_CURSORS|Devuelve el error "Controladores no compatibles con".|  
|SQL_PACKET_SIZE|Devuelve el error "Controladores no compatibles con".|  
|SQL_TXN_ISOLATION|El controlador permite sólo SQL_TXN_READ_COMMITTED.<br /><br /> La siguiente *vParam*s no se admiten:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 Para obtener más información, consulte [SQLGetConnectOption](../../odbc/reference/syntax/sqlgetconnectoption-function.md) en el *referencia del programador de ODBC*.

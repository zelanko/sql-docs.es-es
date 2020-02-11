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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053684"
---
# <a name="sqlgetconnectoption-visual-foxpro-odbc-driver"></a>SQLGetConnectOption (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Compatibilidad: parcial  
  
 Conformidad con la API de ODBC: nivel 1  
  
 Devuelve el valor actual de una opción de conexión. Esta función es parcialmente compatible: el controlador admite todos los valores del argumento *fOption* , pero no admite algunos de los valores de *vParam* para el argumento *fOption* SQL_TXN_ISOLATION.  
  
 En la tabla siguiente se describen solo los argumentos con el comportamiento específico de la implementación del controlador ODBC de Visual FoxPro de **SQLGetConnectOption**.  
  
|*fOption*|Observaciones|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|Si elige SQL_AUTOCOMMIT_OFF, la aplicación debe confirmar o revertir explícitamente las transacciones con [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); el controlador ODBC de Visual FoxPro no confirma automáticamente una instrucción transactable al finalizar. El controlador inicia una transacción si la instrucción es transactable.|  
|SQL_CURRENT_QUALIFIER|Puede ser un nombre completo de base de datos (archivo. DBC) o una ruta de acceso completa a un directorio que contenga cero o más tablas (archivos. dbf).|  
|SQL_LOGINTIMEOUT|Devuelve el error "controlador no compatible".|  
|SQL_CURSORS|Devuelve el error "controlador no compatible".|  
|SQL_PACKET_SIZE|Devuelve el error "controlador no compatible".|  
|SQL_TXN_ISOLATION|El controlador solo permite SQL_TXN_READ_COMMITTED.<br /><br /> No se admiten los siguientes *vParam*s:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 Para obtener más información, vea [SQLGetConnectOption](../../odbc/reference/syntax/sqlgetconnectoption-function.md) en la *Referencia del programador de ODBC*.

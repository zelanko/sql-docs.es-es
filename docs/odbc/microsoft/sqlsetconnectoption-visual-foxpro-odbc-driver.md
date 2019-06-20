---
title: SQLSetConnectOption (controlador ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5a35449e-4694-4ee5-9fa1-45d5a8fe7823
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 398d098615a0453cb016286867836388fd817540
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63473025"
---
# <a name="sqlsetconnectoption-visual-foxpro-odbc-driver"></a>SQLSetConnectOption (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: Parcial  
  
 Conformidad de la API de ODBC: Nivel 1  
  
 Establece las opciones que controlan aspectos de las conexiones. Esta función se admite parcialmente: El controlador es compatible con todos los valores para el *fOption* argumento pero no admite algunos de *vParam* valores para el *fOption* argumento SQL_TXN_ISOLATION.  
  
 En la tabla siguiente se describe solo esos argumentos con el comportamiento específico de la implementación del controlador ODBC de Visual FoxPro de **SQLSetConnectOption**.  
  
|*fOption*|Comentarios|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|Si elige SQL_AUTOCOMMIT_OFF, la aplicación debe confirmar o revertir las transacciones con explícitamente [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); el controlador ODBC de Visual FoxPro no confirma automáticamente una instrucción permiten transacciones tras la finalización. El controlador de iniciar una transacción si la instrucción se permiten transacciones.|  
|SQL_CURRENT_QUALIFIER|Puede ser un nombre completo [base de datos](../../odbc/microsoft/visual-foxpro-terminology.md) nombre o ruta de acceso completa a un directorio que contiene cero o más [libre tablas](../../odbc/microsoft/visual-foxpro-terminology.md).|  
|SQL_LOGINTIMEOUT|Devuelve el error "No compatible con el controlador".|  
|SQL_CURSORS|Devuelve el error "No compatible con el controlador".|  
|SQL_PACKET_SIZE|Devuelve el error "No compatible con el controlador".|  
|SQL_TXN_ISOLATION|El controlador permite sólo SQL_TXN_READ_COMMITTED.<br /><br /> La siguiente *vParam*s no se admiten:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 Para obtener más información, consulte [SQLSetConnectOption](../../odbc/reference/syntax/sqlsetconnectoption-function.md) en el *referencia del programador de ODBC*.

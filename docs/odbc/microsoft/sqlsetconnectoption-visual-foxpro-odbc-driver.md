---
title: SQLSetConnectOption (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
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
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5a35449e-4694-4ee5-9fa1-45d5a8fe7823
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bf786b51ad01bd3f61bdfcbafda23347db4c3aba
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetconnectoption-visual-foxpro-odbc-driver"></a>SQLSetConnectOption (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: parcial  
  
 Ajuste de la API de ODBC: Nivel 1  
  
 Establece las opciones que controlan aspectos de las conexiones. Esta función se admite parcialmente: el controlador es compatible con todos los valores para la *fOption* argumento pero no es compatible con algunos de *vParam* los valores para la *fOption* argumento SQL_TXN_ISOLATION.  
  
 La tabla siguiente describen solo los argumentos con comportamiento específico de la implementación del controlador ODBC de Visual FoxPro de **SQLSetConnectOption**.  
  
|*fOption*|Comentarios|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|Si elige SQL_AUTOCOMMIT_OFF, la aplicación debe confirmar o revertir las transacciones con explícitamente [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); el controlador ODBC de Visual FoxPro no confirma automáticamente una instrucción permiten transacciones tras la finalización. El controlador de iniciar una transacción si la instrucción se permiten transacciones.|  
|SQL_CURRENT_QUALIFIER|Puede ser un nombre completo [base de datos](../../odbc/microsoft/visual-foxpro-terminology.md) nombre o ruta de acceso completa a un directorio que contiene cero o más [libre tablas](../../odbc/microsoft/visual-foxpro-terminology.md).|  
|SQL_LOGINTIMEOUT|Devuelve el error "No compatible con el controlador".|  
|SQL_CURSORS|Devuelve el error "No compatible con el controlador".|  
|SQL_PACKET_SIZE|Devuelve el error "No compatible con el controlador".|  
|SQL_TXN_ISOLATION|El controlador permite solo SQL_TXN_READ_COMMITTED.<br /><br /> El siguiente *vParam*no son compatibles:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 Para obtener más información, consulte [SQLSetConnectOption](../../odbc/reference/syntax/sqlsetconnectoption-function.md) en el *referencia del programador de ODBC*.

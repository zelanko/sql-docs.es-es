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
ms.openlocfilehash: 48a4c8666ab7aa7e210289564210d99c947e5631
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68071712"
---
# <a name="sqlsetconnectoption-visual-foxpro-odbc-driver"></a>SQLSetConnectOption (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Compatibilidad: parcial  
  
 Conformidad con la API de ODBC: nivel 1  
  
 Establece opciones que rigen aspectos de las conexiones. Esta función es parcialmente compatible: el controlador admite todos los valores del argumento *fOption* , pero no admite algunos de los valores de *vParam* para el argumento *fOption* SQL_TXN_ISOLATION.  
  
 En la tabla siguiente se describen solo los argumentos con el comportamiento específico de la implementación del controlador ODBC de Visual FoxPro de **SQLSetConnectOption**.  
  
|*fOption*|Observaciones|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|Si elige SQL_AUTOCOMMIT_OFF, la aplicación debe confirmar o revertir explícitamente las transacciones con [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); el controlador ODBC de Visual FoxPro no confirma automáticamente una instrucción transactable al finalizar. El controlador inicia una transacción si la instrucción es transactable.|  
|SQL_CURRENT_QUALIFIER|Puede ser un nombre de [base de datos](../../odbc/microsoft/visual-foxpro-terminology.md) completo o una ruta de acceso completa a un directorio que contenga cero o más [tablas libres](../../odbc/microsoft/visual-foxpro-terminology.md).|  
|SQL_LOGINTIMEOUT|Devuelve el error "controlador no compatible".|  
|SQL_CURSORS|Devuelve el error "controlador no compatible".|  
|SQL_PACKET_SIZE|Devuelve el error "controlador no compatible".|  
|SQL_TXN_ISOLATION|El controlador solo permite SQL_TXN_READ_COMMITTED.<br /><br /> No se admiten los siguientes *vParam*s:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 Para obtener más información, vea [SQLSetConnectOption](../../odbc/reference/syntax/sqlsetconnectoption-function.md) en la *Referencia del programador de ODBC*.

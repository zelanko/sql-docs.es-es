---
title: Historial de los controladores de escritorio de la base de datos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], history
- ODBC desktop database drivers [ODBC], history
- desktop database drivers [ODBC], history
ms.assetid: b4a2aff8-bde7-4bd5-8580-bc50f27311c8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d225bac273558b928e3e8fd2f41bd121a723f6ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952370"
---
# <a name="history-of-the-desktop-database-drivers"></a>Historial de los controladores de escritorio de la base de datos
En la tabla siguiente se muestra el historial de versiones de controladores de base de datos de escritorio.  
  
|`Version`|Fecha de la versión|Descripción|  
|-------------|------------------|-----------------|  
|1.0|Agosto de 1993|Usa el procesador de consultas SIMBA producido por PageAhead Software. SIMBA recibe llamadas ODBC y las instrucciones SQL, ellos había transformado en llamadas de Microsoft Jet instalables ISAM y, a continuación, llama a la capa de expedición de Microsoft Jet ISAM para cargar y llamar el controlador ISAM instalable apropiado.|  
|2.0|Diciembre de 1994|Puede usar con ODBC 2.0, que expande considerablemente la funcionalidad ODBC. El cambio principal en la versión 2.0 era que el motor de base de datos Microsoft Jet reemplaza el procesador de consultas SIMBA. Con el motor de base de datos Microsoft Jet, los controladores de base de datos de escritorio integrado más profundamente con la tecnología de Microsoft Access y controladores de Microsoft Jet instalables ISAM. Fueron mejoras importantes:<br /><br /> -Compatibilidad con los cursores desplazables nativo.<br />-Compatibilidad con nativo para las combinaciones externas, combinaciones heterogéneas y actualizables y transacciones.<br />-versiones de 32 bits de los controladores para Microsoft Windows NT.|  
|3.0|Octubre de 1995|Proporciona compatibilidad con Windows 95 y Windows NT Workstation o NT 3.51 del servidor. Controladores de 32 bits solo se incluyeron en esta versión; se quitaron los controladores de 16 bits para la versión 3.1 de Windows.|  
|3.5|Octubre de 1996|Estos controladores fueron el juego de caracteres de doble byte (DBCS)-enabled, se ajusten mejor para su uso con aplicaciones de Internet que en versiones anteriores y admite el uso de nombres de origen de datos de archivo (DSN). El controlador de Microsoft Access se publicó en una versión RISC para su uso en plataformas Alpha para Windows 95/98 y Windows NT 3.51 y sistemas operativos posteriores.|  
|4.0|En tiempo de ejecución de 1998|Proporciona compatibilidad con el formato Unicode de motor Jet de Microsoft junto con la compatibilidad para el formato ANSI de versiones anteriores.|  
  
> [!NOTE]  
>  Los controladores versión3. 5 se diseñaron para trabajar con ODBC2. *x*. Aunque también funcionan con ODBC 3.0, no admiten todas las características de ODBC 3.0. Para obtener más información acerca de cómo funcionan estos controladores con ODBC 3.0, consulte [compatibilidad con versiones anteriores y el cumplimiento de estándares](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).

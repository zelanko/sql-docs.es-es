---
description: Historial de los controladores de escritorio de la base de datos
title: Historial de los controladores de base de datos de escritorio | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 80e8f1b52abac92ba09b97d35d45dfe0506963ec
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500328"
---
# <a name="history-of-the-desktop-database-drivers"></a>Historial de los controladores de escritorio de la base de datos
En la tabla siguiente se muestra el historial de versiones de los controladores de base de datos de escritorio.  
  
|Versión|Fecha de la versión|Descripción|  
|-------------|------------------|-----------------|  
|1.0|1993 de agosto|Usó el procesador de consultas SIMBA generado por el software PageAhead. SIMBA recibió llamadas ODBC y instrucciones SQL, las procesó en llamadas ISAM instalables de Microsoft Jet y, a continuación, llamó a la capa de distribución ISAM de Microsoft Jet para cargar y llamar al controlador ISAM instalable adecuado.|  
|2.0|1994 de diciembre|Se usa con ODBC 2,0, que amplió significativamente la funcionalidad ODBC. El cambio más importante en la versión 2,0 era que el motor de base de datos de Microsoft Jet reemplazase al procesador de consultas de SIMBA. Con el motor de base de datos de Microsoft Jet, los controladores de base de datos de escritorio están integrados mucho más estrechamente con los controladores ISAM instalables de Microsoft Jet y la tecnología de Microsoft Access. Las mejoras importantes fueron:<br /><br /> -Compatibilidad nativa con cursores desplazables.<br />-Compatibilidad nativa con combinaciones externas, combinaciones actualizables y heterogéneas, y transacciones.<br />-versiones de 32 bits de los controladores para Microsoft Windows NT.|  
|3.0|1995 de octubre|Compatibilidad con Windows 95 y Windows NT Workstation o NT Server 3,51. En esta versión solo se incluyeron controladores de 32 bits; se han quitado los controladores de 16 bits para Windows versión 3,1.|  
|3,5|1996 de octubre|Estos controladores eran compatibles con el juego de caracteres de doble byte (DBCS), eran más adecuados para su uso con aplicaciones de Internet que con las versiones anteriores y admitían el uso de nombres de origen de datos (DSN) de archivo. El controlador de Microsoft Access se lanzó en una versión RISC para su uso en plataformas Alpha para Windows 95/98 y Windows NT 3,51 y sistemas operativos posteriores.|  
|4.0|Tarde 1998|Proporciona compatibilidad con el formato Unicode del motor de Microsoft Jet junto con la compatibilidad con el formato ANSI de versiones anteriores.|  
  
> [!NOTE]  
>  Los controladores de la versión 3.5 se diseñaron para trabajar con ODBC2. *x*. Aunque también funcionan con ODBC 3,0, no admiten todas las características de ODBC 3,0. Para obtener más información sobre cómo funcionan estos controladores con ODBC 3,0, consulte [compatibilidad con versiones anteriores y cumplimiento de estándares](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).

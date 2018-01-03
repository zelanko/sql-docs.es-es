---
title: Historial de los controladores de base de datos de escritorio | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], history
- ODBC desktop database drivers [ODBC], history
- desktop database drivers [ODBC], history
ms.assetid: b4a2aff8-bde7-4bd5-8580-bc50f27311c8
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6dfa1dc1b533c9e40175e9a3d29dc872344bd664
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="history-of-the-desktop-database-drivers"></a>Historial de los controladores de escritorio de la base de datos
En la tabla siguiente se muestra el historial de versiones de controladores de base de datos de escritorio.  
  
|Versión|Fecha de la versión|Description|  
|-------------|------------------|-----------------|  
|1,0|Agosto de 1993|Usa el procesador de consultas SIMBA generado por PageAhead Software. SIMBA recibe llamadas ODBC y las instrucciones SQL, procesa las llamadas ISAM instalables de Microsoft Jet y, a continuación, llama a la capa de envío de Microsoft Jet ISAM para cargar y llamar el controlador ISAM instalable apropiado.|  
|2.0|Diciembre de 1994|Se utiliza con ODBC 2.0, que expandido significativamente la funcionalidad de ODBC. El cambio principal en la versión 2.0 era que el motor de base de datos de Microsoft Jet reemplaza el procesador de consultas SIMBA. Con el motor de base de datos Microsoft Jet, los controladores de base de datos de escritorio integrado mucho más estrechamente con la tecnología de Microsoft Access y controladores ISAM instalables de Microsoft Jet. Eran importantes mejoras:<br /><br /> -Compatibilidad con cursores desplazables nativo.<br />-Compatibilidad para las combinaciones externas, combinaciones actualizables y heterogéneas y las transacciones.<br />-las versiones de 32 bits de los controladores para Microsoft Windows NT.|  
|3.0|Octubre de 1995|Se ofrece compatibilidad con Windows 95 y Windows NT Workstation o NT 3.51 del servidor. Controladores de 32 bits solo se incluyen en esta versión; se quitaron los controladores de 16 bits para la versión 3.1 de Windows.|  
|3.5|Octubre de 1996|Estos controladores fueron juego de caracteres de doble byte (DBCS)-habilitado, se ajustan mejor para su uso con aplicaciones de Internet que en versiones anteriores y adaptar el uso de nombres de origen de datos (DSN) de archivo. El controlador de Microsoft Access se publicó en una versión RISC para su uso en plataformas Alpha para Windows 95 o Windows 98 y Windows NT 3.51 y sistemas operativos posteriores.|  
|4.0|Tiempo de ejecución de 1998|Proporciona compatibilidad con el formato Unicode de motor Jet de Microsoft junto con compatibilidad para el formato ANSI de versiones anteriores.|  
  
> [!NOTE]  
>  Los controladores de versión3.5 se diseñaron para trabajar con ODBC2. *x*. Aunque también funcionan con ODBC 3.0, no admiten todas las características de ODBC 3.0. Para obtener más información acerca de cómo funcionan estos controladores con ODBC 3.0, consulte [compatibilidad con versiones anteriores y el cumplimiento de estándares](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).

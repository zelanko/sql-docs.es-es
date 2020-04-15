---
title: Historial de los controladores de base de datos de escritorio ? Microsoft Docs
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
ms.openlocfilehash: 89434b397c07fdee751ca4272b65ac2eada94cf3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304986"
---
# <a name="history-of-the-desktop-database-drivers"></a>Historial de los controladores de escritorio de la base de datos
En la tabla siguiente se muestra el historial de versiones de Controladores de base de datos de escritorio.  
  
|Versión|Fecha de la versión|Descripción|  
|-------------|------------------|-----------------|  
|1.0|Agosto de 1993|Se ha utilizado el procesador de consultas SIMBA producido por PageAhead Software. SIMBA recibió llamadas ODBC e instrucciones SQL, las procesó en llamadas ISAM instalables de Microsoft Jet y, a continuación, llamó a la capa de envío ISAM de Microsoft Jet para cargar y llamar al controlador ISAM instalable adecuado.|  
|2.0|Diciembre de 1994|Se utiliza con ODBC 2.0, que amplió significativamente la funcionalidad ODBC. El principal cambio en la versión 2.0 fue que el motor de base de datos Microsoft Jet reemplazó al procesador de consultas SIMBA. Con el motor de base de datos Microsoft Jet, los controladores de base de datos de escritorio se integraron mucho más estrechamente con los controladores ISAM instalables de Microsoft Jet y la tecnología Microsoft Access. Mejoras significativas fueron:<br /><br /> - Soporte nativo para cursores desplazables.<br />- Soporte nativo para uniones externas, uniones actualizables y heterogéneas y transacciones.<br />- Versiones de 32 bits de los controladores para Microsoft Windows NT.|  
|3.0|Octubre de 1995|Se proporciona compatibilidad con Windows 95 y Windows NT Workstation o NT Server 3.51. Solo se incluyeron controladores de 32 bits en esta versión; los controladores de 16 bits para la versión 3.1 de Windows se eliminaron.|  
|3,5|Octubre de 1996|Estos controladores estaban habilitados para el juego de caracteres de doble byte (DBCS), eran más adecuados para su uso con aplicaciones de Internet que las versiones anteriores y daban cabida al uso de nombres de origen de datos de archivo (DSN). El controlador de Microsoft Access fue lanzado en una versión RISC para su uso en plataformas Alpha para Windows 95/98 y Windows NT 3.51 y sistemas operativos posteriores.|  
|4.0|Finales de 1998|Proporciona compatibilidad con el formato Unicode de Microsoft Jet Engine junto con compatibilidad con el formato ANSI de versiones anteriores.|  
  
> [!NOTE]  
>  Los controladores version3.5 se diseñaron para funcionar con ODBC2. *x*. Aunque también funcionan con ODBC 3.0, no admiten todas las características de ODBC 3.0. Para obtener más información acerca de cómo funcionan estos controladores con ODBC 3.0, vea [Compatibilidad con versiones anteriores y Cumplimiento](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)de normas .

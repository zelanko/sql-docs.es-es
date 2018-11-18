---
title: MSSQLSERVER_833 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 833 (Database Engine error)
ms.assetid: 14129cc4-be80-4772-9e3f-0e5da4d0696b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5cbf9d361ff50758c8eb0a3f7b13e234fcf81a38
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51677624"
---
# <a name="mssqlserver833"></a>MSSQLSERVER_833
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|833|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|BUF_LONG_IO|  
|Texto del mensaje|SQL Server ha detectado %d instancias de solicitudes de E/S que están tardando más de %d segundos en completarse en el archivo [%ls] de la base de datos `[%ls] (%d)`.  El identificador de archivo del SO es 0x%p.  El desplazamiento de la operación de E/S más reciente y más larga es: %#016I64x.|  
  
## <a name="explanation"></a>Explicación  
Este mensaje indica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha emitido una solicitud de lectura o escritura desde el disco y que la solicitud ha tardado más de 15 segundos en volver. Este error ha sido notificado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e indica un problema con el subsistema de E/S.  
  
### <a name="possible-causes"></a>Posibles causas  
Este problema puede producirse debido a problemas de rendimiento del sistema, errores de hardware y de firmware, problemas de los controladores de dispositivos o intervención de los controladores de filtro en el proceso de E/S.  
  
## <a name="user-action"></a>Acción del usuario  
Solucione este error examinando el registro de eventos del sistema para localizar mensajes de error relacionados con el hardware. Examine también registros específicos de hardware si están disponibles.  
  
Use el Monitor de rendimiento para examinar los siguientes contadores:  
  
-   **Average Disk Sec/Transfer**  
  
-   **Average Disk Queue Length**  
  
-   **Current Disk Queue Length**  
  
Por ejemplo, el tiempo de **Average Disk Sec/Transfer** en un equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suele ser inferior a 15 milisegundos. Si el valor de la **Average Disk Sec/Transfer** aumenta, esto indica que el subsistema de E/S no se mantiene al nivel de forma óptima de la demanda de E/S.  
  
> [!NOTE]  
> El acceso al disco puede ralentizarse debido a un programa antivirus. Para aumentar la velocidad de acceso, excluya los archivos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se especifican en el mensaje de error de las búsquedas de virus activos.  
  
Para obtener más información sobre de los errores de E/S, vea el [capítulo 2 del documento sobre elementos fundamentales de E/S de Microsoft SQL Server ](https://go.microsoft.com/fwlink/?LinkId=69370) y el artículo de Knowledge Base en [https://support.microsoft.com/kb/897284/en-us](https://support.microsoft.com/kb/897284/en-us).  
  

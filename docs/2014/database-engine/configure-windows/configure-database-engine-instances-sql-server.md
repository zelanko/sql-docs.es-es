---
title: Configurar instancias del motor de base de datos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 84e36fcb-2c78-48e8-8e4b-bf784a3ee557
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5d98d75e74c52a4c9108b1cb46202906aa69e505
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935766"
---
# <a name="configure-database-engine-instances-sql-server"></a>Configurar instancias del motor de base de datos (SQL Server)
  Cada instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] debe configurarse satisfacer los requisitos de rendimiento y disponibilidad definidos para las bases de datos hospedadas por la instancia. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] incluye opciones de configuración que controlan comportamientos como el uso de recursos y la disponibilidad de características como la los comportamientos de control como el uso de los recursos y la disponibilidad de características como auditoría o recursividad de desencadenador.  
  
## <a name="instance-configuration"></a>Configuración de instancia  
 Cuando una base de datos se implementa en producción a menudo hay un contrato de nivel de servicio (SLA) que define áreas como los niveles de rendimiento requeridos a partir de la base de datos y el nivel de disponibilidad necesario de la base de datos. Los términos del SLA controlan normalmente los requisitos de configuración para la instancia.  
  
 Una instancia se configura normalmente inmediatamente después de que ha instalado. La configuración inicial se determina normalmente por los requisitos del SLA de los tipos de bases de datos planeadas para implementarse en la instancia. Una vez implementadas las bases de datos, los administradores de bases de datos supervisan el rendimiento de la instancia y ajustan la configuración según sea necesaria si las métricas de rendimiento muestran que la instancia no cumple los requisitos del SLA.  
  
## <a name="configuration-tasks"></a>Tareas de configuración  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe las distintas opciones de configuración de la instancia y cómo se pueden ver o cambiar estas opciones.|[Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)|  
|Describe cómo ver y configurar las ubicaciones predeterminadas de los archivos de datos y registro nuevos en la instancia.|[Ver o cambiar las ubicaciones predeterminadas de los archivos de datos y registro &#40;SQL Server Management Studio&#41;](view-or-change-the-default-locations-for-data-and-log-files.md)|  
|Describe cómo configurar SQL Server para que use soft-NUMA.|[Configure SQL Server para usar &#40;de Soft-NUMA SQL Server&#41;](soft-numa-sql-server.md)|  
|Describe cómo asignar un puerto TCP/IP a la afinidad del nodo de acceso a memoria no uniforme (NUMA).|[Asignación de puertos TCP/IP a nodos NUMA &#40;SQL Server&#41;](map-tcp-ip-ports-to-numa-nodes-sql-server.md)|  
|Describe cómo habilitar la directiva de Bloquear páginas en memoria de Windows. Esta directiva determina qué cuentas pueden usar un proceso que mantiene los datos en memoria física, impidiendo que el sistema lleve los datos a páginas de memoria virtual (disco).|[Habilitar la opción Bloquear páginas en la memoria &#40;Windows&#41;](enable-the-lock-pages-in-memory-option-windows.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Instancias del motor de base de datos &#40;SQL Server&#41;](database-engine-instances-sql-server.md)  
  
  

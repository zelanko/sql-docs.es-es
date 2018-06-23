---
title: Instalar la replicación de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- components [SQL Server replication]
- command line installations [SQL Server replication]
- installing replication
- replication [SQL Server], installing
- command prompt [SQL Server replication]
ms.assetid: c50ad078-060b-4a8d-ad45-9e31a8d85729
caps.latest.revision: 40
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f63d8eee7708b70eedf9b9e00b85e646132dd986
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108150"
---
# <a name="install-sql-server-replication"></a>Instalar la replicación de SQL Server
  Los componentes de replicación se pueden instalar mediante el Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o en un símbolo del sistema. Instale la replicación al instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o al modificar una instancia existente.  
  
 Después de instalar los componentes de replicación, debe configurar el servidor antes de poder utilizar la replicación. Para obtener más información, vea [Configurar la distribución](../../relational-databases/replication/configure-distribution.md) en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  Si instala componentes de replicación al modificar una instancia existente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe detener y reiniciar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] una vez completada la instalación. De esta forma contribuye a asegurarse de que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reconozca los subsistemas del agente de replicación y pueda llamar a los agentes de replicación mediante pasos de trabajos.  
  
## <a name="installing-replication-by-using-setup"></a>Instalar la replicación mediante el programa de instalación  
 **Para instalar la replicación al instalar una nueva instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
-   Para instalar componentes de replicación, incluido Replication Management Objects (RMO), seleccione **Replicación de SQL Server** en la página **Selección de características** del Asistente para la instalación.  
  
## <a name="installing-replication-from-the-command-prompt"></a>Instalar la replicación desde el símbolo del sistema  
 **Para instalar la replicación al instalar una nueva instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
-   Vea [instalar SQL Server 2014 desde el símbolo del sistema](install-sql-server-from-the-command-prompt.md).  
  
## <a name="see-also"></a>Vea también  
 [Instalar a SQL Server 2014](install-sql-server.md)   
 [Instalar a SQL Server 2014 desde el símbolo del sistema](install-sql-server-from-the-command-prompt.md)   
 [Características compatibles con las ediciones de SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
  
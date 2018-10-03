---
title: Otros problemas de actualización de replicación | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- system tables [SQL Server], replication
- passwords [SQL Server replication]
- versions [SQL Server replication]
- connections [SQL Server replication]
- scripts [SQL Server replication]
- ActiveX controls [SQL Server replication]
ms.assetid: 8a5e74be-4992-4f17-b20c-c3dce8f49329
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e5ffde063d94f0e08ea0e82e6b5998a6d23cfaac
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200735"
---
# <a name="other-replication-upgrade-issues"></a>Otros problemas de actualización de replicación
  En este tema se analiza una serie de problemas de actualización que el Asesor de actualizaciones no notifica.  
  
## <a name="versions-supported"></a>Versiones admitidas  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] admite la actualización de bases de datos replicadas de versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No es necesario detener la actividad en otros nodos mientras se actualiza un nodo. Asegúrese de cumplir las reglas relativas a las versiones admitidas en una topología.  
  
 Cuando se usa la replicación entre versiones diferentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], normalmente se está limitado por las funciones de la versión más antigua que se está usando.  
  
> [!NOTE]  
>  Dado que el formato de almacenamiento en disco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es el mismo en los entornos de 64 bits y de 32 bits, una topología de replicación puede combinar instancias del servidor que se ejecutan en un entorno de 32 bits e instancias del servidor que se ejecutan en un entorno de 64 bits.  
  
 Para todos los tipos de replicación, la versión del distribuidor no debe ser anterior a la versión del publicador. (Con frecuencia, el distribuidor es la misma instancia que el publicador).  
  
 Para la replicación transaccional, un suscriptor de una publicación transaccional puede ser de cualquiera de las dos versiones del publicador.  
  
 Para la replicación de mezcla, un suscriptor para una publicación de combinación puede ser de cualquier versión que no sea posterior a la versión del publicador.  
  
## <a name="merge-replication-batches-changes"></a>Cambios de lotes de replicación de mezcla  
 Los cambios realizados por el Agente de mezcla se ejecutan en lotes para mejorar el rendimiento; por lo tanto, se puede insertar, actualizar o eliminar más de una fila en una sola instrucción. Si las tablas publicadas en las bases de datos de publicaciones o suscripciones tienen desencadenadores, asegúrese de que estos pueden controlar inserciones, actualizaciones y eliminaciones en varias filas. Para obtener más información, vea "Consideraciones acerca de operaciones con varias filas para desencadenadores DML" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="activex-control-changes"></a>Cambios de controles ActiveX  
 Se han realizado los cambios siguientes en los controles ActiveX de replicación:  
  
-   Todos los controles ActiveX están marcados como no seguros para scriptings e inicialización.  
  
-   Se ha quitado el control ActiveX de instantáneas. Puede crear y administrar instantáneas utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o mediante programación usando procedimientos almacenados de replicación. Para obtener más información, vea los temas "Cómo crear y aplicar la instantánea inicial ([!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)])" y "Cómo crear la instantánea inicial (programación de la replicación con Transact-SQL)" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   El control ActiveX de distribución y el control ActiveX de mezcla han quedado desusados. Se proporciona una funcionalidad similar para las aplicaciones de código administrado mediante Replication Management Objects (RMO). Para obtener más información, vea "Sincronizar suscripciones (Programación con RMO)" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de replicación](../../../2014/sql-server/install/replication-upgrade-issues.md)  
  
  

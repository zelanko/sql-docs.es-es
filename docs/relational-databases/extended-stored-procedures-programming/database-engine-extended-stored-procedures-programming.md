---
description: Programación de procedimientos almacenados extendidos de motor de base de datos +
title: Programar procedimientos almacenados extendidos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- gateway applications [SQL Server]
- extended stored procedures [SQL Server], about extended stored procedures
- Open Data Services [SQL Server]
- ODS [SQL Server]
ms.assetid: 561305cd-c803-48af-9eec-2c19f4d311ce
author: rothja
ms.author: jroth
ms.openlocfilehash: c9b17ecfe69eef7f30015cdcef84aaef4790afc3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460853"
---
# <a name="database-engine-extended-stored-procedures---programming"></a>Programación de procedimientos almacenados extendidos de motor de base de datos +
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 En el pasado, los Servicios abiertos de datos se usaban para escribir las aplicaciones de servidor, como las puertas de enlace a entornos de bases de datos que no son de SQL Server. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite las partes obsoletas de la API Servicios abiertos de datos. La única parte de la API Servicios abiertos de datos original que todavía se admite en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son las funciones de procedimiento almacenado extendido, de modo que se ha cambiado el nombre de la API por el de la API Procedimiento almacenado extendido.  
  
 Con la aparición de las más recientes y eficaces tecnologías, como las consultas distribuidas y la integración CLR, se ha reemplazado en gran medida la necesidad de aplicaciones basadas en la API Procedimiento almacenado extendido.  
  
> [!NOTE]  
>  Si tiene aplicaciones de puerta de enlace existentes, no puede utilizar opends60.dll que se distribuye con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ejecutar las aplicaciones. Ya no se admiten las aplicaciones de puerta de enlace.  
  
## <a name="extended-stored-procedures-vs-clr-integration"></a>Procedimientos almacenados extendidos frente a integración CLR  
 En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los procedimientos almacenados extendidos (XP) proporcionaban el único mecanismo disponible para que los programadores de aplicaciones de base de datos escribieran la lógica del servidor, que era difícil de expresar o imposible de escribir en [!INCLUDE[tsql](../../includes/tsql-md.md)]. La integración CLR es una alternativa más consolidada para escribir tales procedimientos almacenados. Además, con la integración CLR, la lógica que se solía escribir en forma de procedimientos almacenados generalmente se expresa mejor como funciones con valores de tabla, que permiten que los resultados generados por la función se consulten en las instrucciones SELECT incrustándolos en la cláusula FROM.  
  
## <a name="see-also"></a>Consulte también  
 [Información general sobre la integración de Common Language Runtime &#40;CLR&#41;](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md)   
 [Funciones con valores de tabla en CLR](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-table-valued-functions.md)  
  
  

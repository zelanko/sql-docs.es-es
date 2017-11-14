---
title: Interbloqueos con nivel de aislamiento Repeatable de lectura | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deadlocks in RDS [ADO]
- read repeatable in RDS [ADO]
ms.assetid: 29f3683f-12f3-4304-8a54-fe133c25a423
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 02e8b890b7973626676b8439471a782d6fba3f27
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="deadlocks-with-read-repeatable-isolation-level"></a>Interbloqueos con nivel de aislamiento Repeatable de lectura
Si un objeto comercial personalizado utiliza un nivel de aislamiento de lectura repetible para obtener acceso a un servidor SQL Server y el objeto de negocio recibe simultáneamente la llamada de dos clientes que envían una consulta y se actualizan en la misma transacción, es posible un interbloqueo. Servicio de datos remoto está diseñado para permitir que uno de los procesos de tiempo de espera y libere el interbloqueo, pero se producirá un error de la actualización para ese cliente.  
  
 Use la [servicio Cursor](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) **tiempo de espera de comando** propiedades dinámicas para modificar la duración del tiempo de espera.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Vea también  
 [Conceptos básicos de RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)





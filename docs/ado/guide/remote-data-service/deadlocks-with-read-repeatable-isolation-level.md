---
title: Interbloqueos con nivel de aislamiento Repeatable de lectura | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- deadlocks in RDS [ADO]
- read repeatable in RDS [ADO]
ms.assetid: 29f3683f-12f3-4304-8a54-fe133c25a423
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a063bfa08ee0c405b52c123f0af03397751a2289
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63214873"
---
# <a name="deadlocks-with-read-repeatable-isolation-level"></a>Interbloqueos con nivel de aislamiento de lectura repetible
Si un objeto comercial personalizado utiliza un nivel de aislamiento de lectura repetible para tener acceso a un servidor SQL Server y el objeto de negocios se llama al mismo tiempo dos clientes que envían una consulta y se actualizan en la misma transacción, es posible un interbloqueo. Servicio de datos remoto está diseñado para permitir que uno de los procesos en tiempo de espera para liberar el interbloqueo, pero se producirá un error de la actualización para el cliente.  
  
 Use la [Cursor servicio](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) **tiempo de espera de comando** propiedad dinámica para modificar la duración del tiempo de espera.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Vea también  
 [Aspectos básicos de RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)




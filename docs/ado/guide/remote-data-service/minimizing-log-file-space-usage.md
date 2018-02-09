---
title: Minimizar el uso de espacio de archivo de registro | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- log file space in RDS [ADO]
ms.assetid: 669662a0-e20f-483e-ab28-53f66c524c98
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ccad217647f8aa2f7bde912f12914055d0f65808
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="minimizing-log-file-space-usage"></a>Minimizar el uso de espacio de archivo de registro
Un archivo de registro podrían llenar rápidamente (por lo tanto la detención del servidor) si hay un gran volumen de actividad en una base de datos de SQL Server. Puede establecer el archivo de registro en **truncar en punto de comprobación** ampliar significativamente la vida del archivo de registro para una base de datos.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-65"></a>Para habilitar truncar en punto de comprobación en Microsoft SQL Server 6.5  
  
1.  Inicie el Administrador corporativo de Microsoft SQL Server, abra el árbol para el servidor y, a continuación, abra el árbol de dispositivos de la base de datos.  
  
2.  Haga doble clic en el nombre de la base de datos en el que se habilitará esta característica.  
  
3.  Desde el **base de datos** ficha, seleccione **Truncate**.  
  
4.  Desde el **opciones** ficha, seleccione **Truncate Log on Checkpoint**y, a continuación, haga clic en **Aceptar**.  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-70"></a>Para habilitar truncar en punto de comprobación en Microsoft SQL Server 7.0  
  
1.  Inicie el Administrador corporativo de Microsoft SQL Server, abra el árbol del servidor y, a continuación, abra el árbol de las bases de datos.  
  
2.  Haga clic en el nombre de la base de datos en el que se habilitará esta característica y seleccione **propiedades**.  
  
3.  Desde el **opciones** ficha, seleccione **Truncate Log on Checkpoint**y, a continuación, haga clic en **Aceptar**.  
  
 Para obtener más información sobre la **truncar en punto de comprobación** de características, consulte la documentación de Microsoft SQL Server.  
  
## <a name="see-also"></a>Vea también  
 [Aspectos básicos de RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)



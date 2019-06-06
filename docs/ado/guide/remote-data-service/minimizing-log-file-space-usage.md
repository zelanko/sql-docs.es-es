---
title: Minimizar el uso de espacio de archivo de registro | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- log file space in RDS [ADO]
ms.assetid: 669662a0-e20f-483e-ab28-53f66c524c98
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1c6894a19c39df171dea3b621773daf31971895f
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704270"
---
# <a name="minimizing-log-file-space-usage"></a>Minimización del uso de espacio de archivo de registro
Un archivo de registro puede llenar rápidamente (detener, por tanto, el servidor) si hay un gran volumen de actividad en una base de datos de SQL Server. Puede establecer el archivo de registro en **Truncate en punto de comprobación** ampliar significativamente la vida del archivo de registro para una base de datos.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-65"></a>Para habilitar truncar en punto de comprobación en Microsoft SQL Server 6.5  
  
1.  Iniciar el Administrador corporativo de Microsoft SQL Server, abra el árbol para el servidor y, a continuación, abra el árbol de los dispositivos de la base de datos.  
  
2.  Haga doble clic en el nombre de la base de datos en el que se habilitará esta característica.  
  
3.  Desde el **base de datos** ficha, seleccione **Truncate**.  
  
4.  Desde el **opciones** ficha, seleccione **truncar registro en punto de comprobación**y, a continuación, haga clic en **Aceptar**.  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-70"></a>Para habilitar truncar en punto de comprobación en Microsoft SQL Server 7.0  
  
1.  Iniciar el Administrador corporativo de Microsoft SQL Server, abra el árbol para el servidor y, a continuación, abra el árbol de las bases de datos.  
  
2.  Haga clic en el nombre de la base de datos en el que se habilitará esta característica y elija **propiedades**.  
  
3.  Desde el **opciones** ficha, seleccione **truncar registro en punto de comprobación**y, a continuación, haga clic en **Aceptar**.  
  
 Para obtener más información sobre la **Truncate en punto de comprobación** de características, consulte la documentación de Microsoft SQL Server.  
  
## <a name="see-also"></a>Vea también  
 [Aspectos básicos de RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)



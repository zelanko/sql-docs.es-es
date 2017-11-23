---
title: "Copia de seguridad y carga de información general de hardware para APS PDW"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "Para implementar los datos de end-to-end con almacenamiento de datos paralelos de SQL Server (PDW) de la solución en Analytics Platform System (APS) de almacenamiento, debe crear un plan de copia de seguridad del almacenamiento de datos y cargar los datos."
ms.date: 10/20/2016
ms.topic: article
ms.assetid: 3a2ae046-f8d8-4a5c-b3c1-6ecee005df6c
caps.latest.revision: "9"
ms.openlocfilehash: 0bdf529aacf1644f55cd44da3d0a7590e509a323
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="backup-and-loading-hardware-overview"></a>Copia de seguridad y cargar la información general de hardware
Para implementar los datos de end-to-end con almacenamiento de datos paralelos de SQL Server (PDW) de la solución en Analytics Platform System (APS) de almacenamiento, debe crear un plan de copia de seguridad del almacenamiento de datos y cargar los datos. Utilice esta guía para adquirir y configurar servidores de copia de seguridad y cargar que satisfacen sus requisitos empresariales.  
  
## <a name="acquire-and-configure-backup-servers"></a>Adquirir y configurar servidores de copia de seguridad  
![Proceso de copia de seguridad](media/backup-process.png "proceso de copia de seguridad")  
  
Para una base de datos PDW de copia de seguridad, necesita uno o más servidores de copia de seguridad. Puede usar su propio hardware existente o adquirir nuevo hardware. Para obtener más información, consulte [adquirir y configurar un servidor de copia de seguridad](acquire-and-configure-backup-server.md). Estas instrucciones incluyen un [hoja de planificación de capacidad de servidor de copia de seguridad](backup-capacity-planning-worksheet.md) le ayudará a planear la solución correcta para la copia de seguridad.  
  
## <a name="acquire-and-configure-loading-servers"></a>Adquirir y configurar servidores de carga  
![Proceso de carga](media/loading-process.png "proceso de carga")  
  
Para cargar datos, tendrá que uno o más servidores de carga. Puede usar su propio ETL existente u otros servidores, o puede comprar nuevos servidores. Para obtener más información, consulte [adquirir y configurar un servidor de carga](acquire-and-configure-loading-server.md). Estas instrucciones incluyen un [cargar la hoja de cálculo de planeación de capacidad servidor](loading-server-capacity-planning-worksheet.md) le ayudará a planear la solución adecuada para la carga.  
  
## <a name="see-also"></a>Vea también  
[Información general de copia de seguridad y restauración](backup-and-restore-overview.md)  
[Información general de carga](load-overview.md)  
  

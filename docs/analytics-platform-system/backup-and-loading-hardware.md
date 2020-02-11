---
title: Copia de seguridad & carga de hardware
description: Para implementar una solución de almacenamiento de datos de un extremo a otro en Analytics Platform System (APS) con almacenamiento de datos paralelos (PDW), debe crear un plan para realizar una copia de seguridad del almacenamiento de datos y cargar los datos. Use esta guía para adquirir y configurar servidores de copia de seguridad y carga que cumplan los requisitos empresariales.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4dd4fba91b1507f711a66a88f40b2fa2ea35e1ae
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401360"
---
# <a name="backup-and-loading-hardware-overview---parallel-data-warehouse"></a>Información general del hardware de copia de seguridad y carga: almacenamiento de datos paralelos
Para implementar una solución de almacenamiento de datos de un extremo a otro en Analytics Platform System (APS) con almacenamiento de datos paralelos (PDW), debe crear un plan para realizar una copia de seguridad del almacenamiento de datos y cargar los datos. Use esta guía para adquirir y configurar servidores de copia de seguridad y carga que cumplan los requisitos empresariales.  
  
## <a name="acquire-and-configure-backup-servers"></a>Adquirir y configurar servidores de copia de seguridad  
![Proceso de copia de seguridad](media/backup-process.png "Proceso de copia de seguridad")  
  
Para realizar una copia de seguridad de una base de datos de PDW, se necesitan uno o varios servidores de copia de seguridad. Puede usar su propio hardware existente o adquirir hardware nuevo. Para obtener más información, vea [adquirir y configurar un servidor de copia de seguridad](acquire-and-configure-backup-server.md). Estas instrucciones incluyen una [hoja de cálculo de planeamiento](backup-capacity-planning-worksheet.md) de la capacidad del servidor de copia de seguridad para ayudarle a planear la solución adecuada para la copia de seguridad.  
  
## <a name="acquire-and-configure-loading-servers"></a>Adquirir y configurar servidores de carga  
![Cargando proceso](media/loading-process.png "Cargando proceso")  
  
Para cargar datos, necesita uno o más servidores de carga. Puede usar su propio ETL existente u otros servidores, o puede adquirir nuevos servidores. Para obtener más información, vea [adquirir y configurar un servidor de carga](acquire-and-configure-loading-server.md). Estas instrucciones incluyen una [hoja de cálculo de planeamiento](loading-server-capacity-planning-worksheet.md) de la capacidad del servidor de carga para ayudarle a planear la solución adecuada para la carga.  
  
## <a name="see-also"></a>Consulte también  
[Información general sobre copias de seguridad y restauración](backup-and-restore-overview.md)  
[Información general sobre la carga](load-overview.md)  
  

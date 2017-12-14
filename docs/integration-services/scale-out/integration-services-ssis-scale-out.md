---
title: Escalabilidad horizontal de SQL Server Integration Services (SSIS) | Microsoft Docs
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
caps.latest.revision: "6"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0277d312ce4dab14e7ba64529e3eb2251a0d2d02
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="integration-services-ssis-scale-out"></a>Escalado horizontal de Integration Services (SSIS)
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] El escalado horizontal proporciona una ejecución de paquetes de alto rendimiento al distribuir las ejecuciones en varias máquinas. Puede enviar una solicitud para varias ejecuciones de paquetes en SQL Server Management Studio. Estos paquetes se ejecutarán en paralelo, en un modo de escalado horizontal.  

[!INCLUDE[ssIS_md](../../includes/ssis-md.md)] La escalabilidad horizontal consta de un patrón de escalabilidad horizontal de [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] y de uno o varios trabajos de escalabilidad horizontal de [!INCLUDE[ssIS_md](../../includes/ssis-md.md)]. El patrón se encarga de la administración del escalado horizontal y recibe solicitudes de ejecución de paquetes de los usuarios. Los trabajador extraen tareas de ejecución del patrón de escalado horizontal y llevan a cabo el trabajo de ejecución de paquetes. Para obtener más información, consulte [Patrón de escalado horizontal](integration-services-ssis-scale-out-master.md) y [Trabajador de escalado horizontal](integration-services-ssis-scale-out-worker.md).

[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] La escalabilidad horizontal puede configurarse en una máquina, en la que haya un patrón de escalabilidad horizontal y un trabajo de escalabilidad horizontal configurados en paralelo. El escalado horizontal también puede ejecutarse en varios equipos; en este caso, cada trabajador de escalado horizontal está en un equipo diferente.
- [Tutorial: configuración del escalado horizontal de Integration Services](walkthrough-set-up-integration-services-scale-out.md)

El escalado horizontal admite la ejecución en paralelo de varios paquetes en el catálogo SSISDB. Para obtener más información, consulte [Ejecutar paquetes en el escalado horizontal](run-packages-in-integration-services-ssis-scale-out.md).

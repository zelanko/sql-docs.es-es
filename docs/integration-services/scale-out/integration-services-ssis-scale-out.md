---
title: SQL Server Integration Services (SSIS) escalada | Documentos de Microsoft
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ce7fb96901e8af4da74392fe0a0a85c6e2ec05a4
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-ssis-scale-out"></a>Escalado horizontal de Integration Services (SSIS)
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] El escalado horizontal proporciona una ejecución de paquetes de alto rendimiento al distribuir las ejecuciones en varias máquinas. Puede enviar una solicitud de varias ejecuciones de paquetes en SQL Server Management Studio. Estos paquetes se ejecutarán en paralelo, en un modo de escalado horizontal.  

[!INCLUDE[ssIS_md](../../includes/ssis-md.md)]Horizontalmente consta de un [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] escala Out maestro y uno o más [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] trabajadores fuera de la escala. El patrón se encarga de la administración del escalado horizontal y recibe solicitudes de ejecución de paquetes de los usuarios. Los trabajador extraen tareas de ejecución del patrón de escalado horizontal y llevan a cabo el trabajo de ejecución de paquetes. Para obtener más información, consulte [Patrón de escalado horizontal](integration-services-ssis-scale-out-master.md) y [Trabajador de escalado horizontal](integration-services-ssis-scale-out-worker.md).

[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]Horizontalmente puede configurarse en un equipo, donde un patrón de salida de escala y una escala Out trabajo se configuran en paralelo en el equipo. El escalado horizontal también puede ejecutarse en varios equipos; en este caso, cada trabajador de escalado horizontal está en un equipo diferente.
- [Tutorial: configuración del escalado horizontal de Integration Services](walkthrough-set-up-integration-services-scale-out.md)

El escalado horizontal admite la ejecución en paralelo de varios paquetes en el catálogo SSISDB. Para obtener más información, consulte [Ejecutar paquetes en el escalado horizontal](run-packages-in-integration-services-ssis-scale-out.md).


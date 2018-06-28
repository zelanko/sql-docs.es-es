---
title: Escalabilidad horizontal de SQL Server Integration Services (SSIS) | Microsoft Docs
description: En este artículo se proporciona información general sobre la característica Escalabilidad horizontal de SQL Server Integration Services (SSIS), que permite la ejecución de alto rendimiento de paquetes SSIS.
ms.custom: performance
ms.date: 12/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7fc57db9bc8a305450aa2619d9b7c222fda91763
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35334089"
---
# <a name="integration-services-ssis-scale-out"></a>Escalado horizontal de Integration Services (SSIS)
La escalabilidad horizontal de SQL Server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS) proporciona una ejecución de alto rendimiento de paquetes de SSIS mediante la distribución de ejecuciones de paquetes en varios equipos. Tras configurar la escalabilidad horizontal, puede ejecutar múltiples ejecuciones de paquetes en paralelo (en el modo de escalabilidad horizontal) desde SQL Server Management Studio (SSMS).

## <a name="components"></a>Components
[!INCLUDE[ssIS_md](../../includes/ssis-md.md)] La escalabilidad horizontal consta de un patrón de escalabilidad horizontal de [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] y de uno o varios trabajadores de escalabilidad horizontal de [!INCLUDE[ssIS_md](../../includes/ssis-md.md)].

-   El patrón se encarga de la administración del escalado horizontal y recibe solicitudes de ejecución de paquetes de los usuarios. Para obtener más información, vea [Patrón de escalabilidad horizontal](integration-services-ssis-scale-out-master.md).

-   Los trabajadores de escalabilidad horizontal extraen las tareas de ejecución del patrón de escalabilidad horizontal y ejecutan los paquetes. Para obtener más información, vea [Trabajador de escalabilidad horizontal](integration-services-ssis-scale-out-worker.md).

## <a name="configuration-options"></a>Opciones de configuración
Puede configurar la escalabilidad horizontal mediante las siguientes configuraciones:

-   **En un único equipo** en el que un patrón y un trabajador de escalabilidad horizontal se ejecutan en paralelo en el mismo equipo.

-   **En varios equipos** en los que cada trabajador de escalabilidad horizontal se encuentre en un equipo distinto.

## <a name="what-you-can-do"></a>Qué puede hacer
Tras configurar la escalabilidad horizontal, puede hacer lo siguiente:

-   Ejecutar varios paquetes implementados en paralelo en el catálogo de SSISDB. Para obtener más información, vea [Ejecutar paquetes en la escalabilidad horizontal](run-packages-in-integration-services-ssis-scale-out.md).

-   Administrar la topología de la escalabilidad horizontal en la aplicación Scale Out Manager. Para obtener más información, vea [Scale Out Manager de Integration Services](integration-services-ssis-scale-out-manager.md).

## <a name="next-steps"></a>Pasos siguientes
-   [Introducción a la escalabilidad horizontal de Integration Services (SSIS) en un único equipo](get-started-with-ssis-scale-out-onebox.md)

-   [Tutorial: configuración del escalado horizontal de Integration Services](walkthrough-set-up-integration-services-scale-out.md)

---
title: Escalabilidad horizontal de SQL Server Integration Services (SSIS) | Microsoft Docs
ms.description: This article provides an overview of the SQL Server Integration Services (SSIS) Scale Out feature, which provides high-performance execution of SSIS packages
ms.custom: ''
ms.date: 12/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: scale-out
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7dae1d65334003843ea5ad55143db40f862715a6
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
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

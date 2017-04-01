---
title: "Escalado horizontal de Integration Services (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
caps.latest.revision: 6
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 6
---
# Escalado horizontal de Integration Services (SSIS)
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] El escalado horizontal proporciona una ejecución de paquetes de alto rendimiento al distribuir las ejecuciones en varias máquinas. Se puede enviar una solicitud para varias ejecuciones de paquetes en SQL Server Management Studio. Estos paquetes se ejecutarán en paralelo, en un modo de escalado horizontal.  


## <a name="ssis-scale-out-master-and-scale-out-worker"></a>Patrón y trabajador de escalado horizontal de SSIS
[!INCLUDE[ssIS_md](../includes/ssis-md.md)] El escalado horizontal consta de un [!INCLUDE[ssIS_md](../includes/ssis-md.md)] patrón de escalado horizontal y de varios [!INCLUDE[ssIS_md](../includes/ssis-md.md)] trabajadores de escalado horizontales. El patrón se encarga de la administración del escalado horizontal y recibe solicitudes de ejecución de paquetes de los usuarios. Los trabajador extraen tareas de ejecución del patrón de escalado horizontal y llevan a cabo el trabajo de ejecución de paquetes. Para obtener más información, consulte [Patrón de escalado horizontal](../integration-services/integration-services-ssis-scale-out-master.md) y [Trabajador de escalado horizontal](../integration-services/integration-services-ssis-scale-out-worker.md).


## <a name="how-to-set-up-scale-out"></a>Cómo configurar el escalado horizontal
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] El escalado horizontal se puede ejecutar en un equipo, en el que hay un patrón de escalado horizontal y un trabajador de escalado horizontal configurados en paralelo. El escalado horizontal también puede ejecutarse en varios equipos; en este caso, cada trabajador de escalado horizontal está en un equipo diferente.
- [Tutorial: configuración del escalado horizontal de Integration Services](../integration-services/walkthrough-set-up-integration-services-scale-out.md)


## <a name="run-packages-in-scale-out"></a>Ejecutar paquetes en el escalado horizontal
El escalado horizontal admite la ejecución en paralelo de varios paquetes en el catálogo SSISDB. Para obtener más información, consulte [Ejecutar paquetes en el escalado horizontal](../integration-services/run-packages-in-integration-services-ssis-scale-out.md).


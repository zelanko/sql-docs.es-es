---
title: "Novedades de Integration Services en SQL Server vNext | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e26d7884-e772-46fa-bfdc-38567fe976a1
caps.latest.revision: 4
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 3
---
# Novedades de Integration Services en SQL Server vNext
En este tema, se describen las características que se han agregado o actualizado en [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].

>   [!NOTE] SQL Server vNext también incluye las características de SQL Server 2016 y las características agregadas en las actualizaciones de SQL Server 2016. Para obtener información sobre las nuevas características de SSIS en SQL Server 2016, consulte [Novedades de Integration Services en SQL Server 2016](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md).

## <a name="new-in-ssis-in-sql-server-vnext-ctp-11"></a>Novedades de SSIS en SQL Server vNext CTP 1.1

No hay características nuevas de SSIS en SQL Server vNext CTP 1.1.

## <a name="new-in-ssis-in-sql-server-vnext-ctp-10"></a>Novedades de SSIS en SQL Server vNext CTP 1.0

### <a name="scale-out-for-ssis"></a>Escalado horizontal para SSIS

La característica de escalado horizontal facilita mucho la ejecución de [!INCLUDE[ssIS_md](../includes/ssis-md.md)] en varios equipos. 
   
Después de instalar el patrón y los trabajadores de escalado horizontal, se puede distribuir el paquete para su ejecución automática en diferentes trabajadores. Si la ejecución finaliza inesperadamente, se vuelve a intentar automáticamente. Además, todas las ejecuciones y los trabajadores pueden administrarse de manera centralizada mediante el patrón.
   
Para obtener más información, consulte [Escalado horizontal de Integration Services](../integration-services/integration-services-ssis-scale-out.md).
   
### <a name="support-for-microsoft-dynamics-online-resources"></a>Compatibilidad con recursos de Microsoft Dynamics Online

El origen OData y el administrador de conexiones OData ahora admiten la conexión a fuentes de OData de Microsoft Dynamics AX Online y Microsoft Dynamics CRM Online.

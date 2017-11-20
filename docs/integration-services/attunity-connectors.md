---
title: Conectores de Microsoft para Oracle y Teradata de Attunity (SSIS) | Documentos de Microsoft
ms.date: 05/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 926c0c51b5a55a2869b73666f5620fa56e139cca
ms.openlocfilehash: fd8b0177227167f6caa3417029bb2acb974fe181
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="microsoft-connectors-for-oracle-and-teradata-by-attunity-for-integration-services-ssis"></a>Conectores de Microsoft para Oracle y Teradata de Attunity para Integration Services (SSIS)

Puede descargar conectores para los servicios de integración de Attunity que optimizar el rendimiento cuando se cargan datos hacia o desde Oracle o Teradata en un paquete SSIS.

## <a name="download-the-latest-attunity-connectors"></a>Descargar los conectores de Attunity más recientes

Obtener la versión más reciente de los conectores aquí:  
[V5.0 de conectores de Microsoft para Oracle y Teradata](https://www.microsoft.com/download/details.aspx?id=55179)

## <a name="issue---the-attunity-connectors-arent-visible-in-the-ssis-toolbox"></a>Problema: los conectores de Attunity no están visibles en el cuadro de herramientas de SSIS

Para ver los conectores de Attunity en el cuadro de herramientas de SSIS, siempre tiene que instalar la versión de los conectores que destinos de la misma versión de SQL Server que la versión de SQL Server Data Tools (SSDT) instalado en el equipo. (También puede tener versiones anteriores de los conectores instalados.) Este requisito es independiente de la versión de SQL Server que desea usar como destino en los paquetes y proyectos de SSIS.

Por ejemplo, si ha instalado la versión más reciente de SSDT, tiene la versión 17 de SSDT con un número de compilación que empieza con 14. Esta versión de SSDT agrega compatibilidad para SQL Server 2017. Para ver y usar el Attunity conectores en SSIS empaquetar development - incluso si desea tener como destino una versión anterior de SQL Server, también tendrá que instalar la versión más reciente de los conectores de Attunity, versión 5.0. Esta versión de los conectores también agrega compatibilidad para SQL Server 2017.

Comprobar la versión instalada de SSDT en Visual Studio desde **ayuda** | **acerca de Microsoft Visual Studio**, o bien en **programas y características** en el Panel de Control. A continuación, instale la versión correspondiente de los conectores de Attunity desde la tabla siguiente.

|Versión SSDT|Número de compilación SSDT|Versión de SQL Server de destino|Versión requerida de conectores|
|---------|---------|---------|---------|
|17|Comienza con 14|SQL Server 2017|[V5.0 de conectores de Microsoft para Oracle y Teradata](https://www.microsoft.com/download/details.aspx?id=55179)|
|16|Comienza con 13|SQL Server 2016|[V4.0 de conectores de Microsoft para Oracle y Teradata](https://www.microsoft.com/download/details.aspx?id=52950)|
||||

## <a name="download-the-latest-sql-server-data-tools-ssdt"></a>Descargar la última SQL Server Data Tools (SSDT)

Obtener la versión más reciente de SSDT aquí:  
[Descargar SQL Server Data Tools (SSDT)](..//ssdt/download-sql-server-data-tools-ssdt.md)


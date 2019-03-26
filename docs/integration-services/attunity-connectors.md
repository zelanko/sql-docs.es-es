---
title: Microsoft Connectors para Oracle y Teradata de Attunity (SSIS) | Microsoft Docs
ms.date: 05/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.custom: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ''
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3d73eff658ecfa8f5f145f29c8522a0723d93ff8
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/20/2019
ms.locfileid: "58275709"
---
# <a name="microsoft-connectors-for-oracle-and-teradata-by-attunity-for-integration-services-ssis"></a>Microsoft Connectors para Oracle y Teradata de Attunity para Integration Services (SSIS)

Puede descargar conectores para Integration Services de Attunity que optimizan el rendimiento al cargar datos a o desde Oracle o Teradata en un paquete SSIS.

## <a name="download-the-latest-attunity-connectors"></a>Descargar los conectores de Attunity más recientes

Obtenga la versión más reciente de los conectores aquí:  
[Microsoft Connectors v5.0 para Oracle y Teradata](https://www.microsoft.com/download/details.aspx?id=55179)

## <a name="issue---the-attunity-connectors-arent-visible-in-the-ssis-toolbox"></a>Problema: los conectores de Attunity no están visibles en el cuadro de herramientas de SSIS

Para ver los conectores de Attunity en el cuadro de herramientas de SSIS, deberá instalar la versión de los conectores que corresponde a la misma versión de SQL Server que la versión de SQL Server Data Tools (SSDT) instalada en el equipo. (También es posible que tenga versiones anteriores de los conectores instaladas). Este requisito es independiente de la versión de SQL Server a la que quiera dirigirse en los paquetes y proyectos de SSIS.

Por ejemplo, si instaló la versión más reciente de SSDT, tiene la versión 17 de SSDT con un número de compilación que empieza con 14. Esta versión de SSDT agrega compatibilidad con SQL Server 2017. Para ver y usar los conectores de Attunity en el desarrollo del paquete de SSIS, incluso si desea orientarse a una versión anterior de SQL Server, deberá instalar igualmente la versión más reciente de los conectores de Attunity, versión 5.0. Esta versión de los conectores también agrega compatibilidad con SQL Server 2017.

Compruebe la versión instalada de SSDT en Visual Studio en **Ayuda** | **Acerca de Microsoft Visual Studio**, o bien en **Programas y características** del Panel de control. A continuación, instale la versión correspondiente de los conectores de Attunity de la tabla siguiente.

|Versión de SSDT|Número de compilación de SSDT|Versión de SQL Server de destino|Versión necesaria de los conectores|
|---------|---------|---------|---------|
|17|Empieza por 14|SQL Server 2017|[Microsoft Connectors v5.0 para Oracle y Teradata](https://www.microsoft.com/download/details.aspx?id=55179)|
|16|Empieza por 13|SQL Server 2016|[Microsoft Connectors v4.0 para Oracle y Teradata](https://www.microsoft.com/download/details.aspx?id=52950)|
||||

## <a name="download-the-latest-sql-server-data-tools-ssdt"></a>Descargar la última versión de SQL Server Data Tools (SSDT)

Descargue la última versión de SSDT aquí:  
[Descargar SQL Server Data Tools (SSDT)](..//ssdt/download-sql-server-data-tools-ssdt.md)

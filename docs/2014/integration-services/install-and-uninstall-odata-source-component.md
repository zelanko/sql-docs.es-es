---
title: Instalar y desinstalar el componente de origen OData | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 0a3ae788-e8c8-4a4d-bb15-34c673abcd17
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 86aa25f148c44343a57e0e55831663155d288830
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53374447"
---
# <a name="install-and-uninstall-odata-source-component"></a>Instalar y desinstalar el Componente de origen OData
  Este tema proporciona instrucciones para instalar o quitar el Componente de origen OData en el equipo.  
  
## <a name="installation"></a>Instalación  
 El Componente de origen OData requiere la instalación de los componentes necesarios siguientes en el equipo.  
  
-   SQL Server Data Tools (para diseñar paquetes)  
  
-   SQL Server Integration Services (para ejecutar paquetes fuera de Visual Studio)  
  
 Para instalar el Componente de origen OData, descargue [SQL Server 2014 Feature Pack](https://go.microsoft.com/fwlink/p/?LinkId=391999) y ejecute uno de los siguientes archivos MSI.  
  
-   ODataSourceForSQLServer2014-amd64.msi para las plataformas de 64 bits  
  
-   ODataSourceForSQLServer2014-x86.msi para las plataformas de 32 bits  
  
> [!IMPORTANT]  
>  El instalador de 64 bits instalará las versiones de 32 y 64 bits del Componente de origen OData. Si usa un sistema operativo de 32 bits, solo necesita ejecutar el programa de instalación de 32 bits.  
  
## <a name="uninstallation"></a>Desinstalación  
 El Componente de origen OData se puede desinstalar desde el menú **Programas y características** . Busque la entrada **Componente de origen OData de Microsoft SQL Server SSIS (x64)** y haga clic en **Desinstalar**.  
  
  

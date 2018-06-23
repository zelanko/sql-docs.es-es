---
title: Instalar Microsoft Connector for 1.1 SAP BW | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3bfb9023-9597-4f59-9085-4b9057e7702e
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: dc6bbbf5972615880d3852d5f56a955862c9f22b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203228"
---
# <a name="installing-the-microsoft-connector-for-11-sap-bw"></a>Instalar Microsoft Connector for 1.1 SAP BW
  Para instalar el [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector 1.1 for SAP BW y su documentación, descargue y ejecute el paquete de Windows installer desde la página Web de SQL Server Feature Pack.  
  
> [!IMPORTANT]  
>  La documentación de Microsoft Connector 1.1 for SAP BW da por supuesto que se está familiarizado con el entorno SAP Netweaver BW. Para obtener más información acerca de SAP Netweaver BW, o sobre cómo configurar los objetos y los procesos de SAP Netweaver BW, vea la documentación de SAP.  
  
> [!IMPORTANT]  
>  La extracción de datos de SAP Netweaver BW requiere una licencia SAP adicional. Póngase en contacto con SAP para comprobar estos requisitos.  
  
## <a name="required-sap-files"></a>Archivos necesarios de SAP  
 Para usar el [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector 1.1 for SAP BW, no es necesario instalar el software SAP Front-End (GUI de SAP) en el equipo local.  
  
 Sin embargo, debe copiar el archivo del conector .NET de SAP, librfc32.dll, en la subcarpeta del sistema de la carpeta Windows. (Normalmente, la ubicación de esta carpeta es **C:\Windows\system32**).  
  
## <a name="considerations-for-64-bit-computers"></a>Consideraciones para equipos de 64 bits  
 El [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector 1.1 for SAP BW es totalmente compatible con la versión de 64 bits de [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows. En un equipo de 64 bits, la [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector 1.1 for SAP BW tiene los siguientes requisitos adicionales:  
  
-   Para ejecutar paquetes en modo de 64 bits en cualquier sistema operativo Windows de 64 bits, copie la versión de 64 bits del archivo de la GUI de SAP, librfc32.dll, a la carpeta **system32** de la carpeta Windows. (Normalmente, la ubicación de este archivo es **C:\Windows\system32**).  
  
-   Para ejecutar paquetes en modo de 32 bits en cualquier sistema operativo Windows de 64 bits, copie el archivo de la GUI de SAP, librfc32.dll, a la carpeta **SysWow64** de la carpeta Windows. (Normalmente, la ubicación de esta carpeta es **C:\Windows\SysWow64**).  
  
  
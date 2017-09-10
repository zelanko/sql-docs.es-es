---
title: Configurar un cliente de ciencia de datos | Microsoft Docs
ms.custom: 
ms.date: 02/10/2017
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d15ee956-918f-40e0-b986-2bf929ef303a
caps.latest.revision: 14
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0661b2fcf9b23d3c81cb0d80f0424d87dbde7ef8
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="set-up--a-data-science-client"></a>Configurar un cliente de ciencia de datos
  Después de configurar una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para usar **R Services (en bases de datos)**, probablemente le interesará configurar un entorno de desarrollo de R que sea capaz de conectarse al servidor para la ejecución y la implementación remotas. 
  
  Este entorno debe incluir los paquetes de ScaleR y, opcionalmente, incluir un entorno de desarrollo de cliente.
  
 ## <a name="where-to-get-scaler"></a>Dónde obtener ScaleR 
  
  El entorno de cliente debe incluir Microsoft R Open, así como los paquetes de RevoScaleR adicionales que admiten la ejecución distribuida de R en SQL Server.  Hay varias maneras de instalar estos paquetes:
  
+ Instalar el [Cliente de Microsoft R](http://aka.ms/rclient/download). Aquí encontrará más instrucciones de instalación: [Introducción a Microsoft R Client](https://msdn.microsoft.com/microsoft-r/r-client-get-started)
+ Instalar Microsoft R Server. Puede obtener Microsoft R Server desde el programa de instalación de SQL Server o si usa el nuevo instalador independiente de Windows. Para más información, vea [Crear un R Server independiente](../../advanced-analytics/r-services/create-a-standalone-r-server.md) e [Introducción a R Server](https://msdn.microsoft.com/microsoft-r/rserver).

Si tiene un contrato de licencia de R Server, se recomienda usar Microsoft R Server (independiente) para soslayar las limitaciones de R en cuanto a procesamiento de subprocesos y datos en memoria.


## <a name="how-to-set-up-the-r-development-environment"></a>Cómo configurar el entorno de desarrollo de R

Puede usar cualquier entorno de desarrollo de R de su elección que sea compatible con Windows. 

+ Herramientas de R para Visual Studio admite la integración con Microsoft R Open
+ RStudio es un entorno libre muy conocido  

Tras la instalación, tendrá que reconfigurar el entorno para usar las bibliotecas de Microsoft R Open de forma predeterminada o, de lo contrario, no tendrá acceso a las bibliotecas de ScaleR. Para más información, vea [Getting Started with Microsoft R Client](http://msdn.microsoft.com/microsoft-r/r-client-get-started) (Introducción a Microsoft R Client).
 
## <a name="more-resources"></a>Más recursos
  
 Para obtener un tutorial detallado sobre cómo conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la ejecución remota de código de R, consulte [Análisis detallado de ciencia de datos: Usar los paquetes de RevoScaleR](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md).  
 

Para empezar a usar Microsoft R Client y los paquetes de ScaleR con SQL Server, vea [ScaleR Getting Started](https://msdn.microsoft.com/microsoft-r/scaler-getting-started#) (Introducción a ScaleR).  
  
## <a name="see-also"></a>Vea también  
 [Configurar SQL Server R Services &#40;en bases de datos&#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  


---
title: "Configurar un cliente de ciencia de datos | Microsoft Docs"
ms.custom: ""
ms.date: "02/10/2017"
ms.prod: "r-server"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d15ee956-918f-40e0-b986-2bf929ef303a
caps.latest.revision: 14
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# Configurar un cliente de ciencia de datos
  Después de configurar una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para usar **R Services (en bases de datos)**, probablemente le interesará configurar un entorno de desarrollo de R que sea capaz de conectarse al servidor para la ejecución y la implementación remotas. 
  
  El entorno de cliente debe incluir Microsoft R Open, así como los paquetes de RevoScaleR adicionales que admiten la ejecución distribuida de R en SQL Server.  Hay varias maneras de instalar estos paquetes:
  
+ Instalar el [Cliente de Microsoft R](http://aka.ms/rclient/download).
+ Instalar Microsoft R Server. Puede obtener Microsoft R Server desde el programa de instalación de SQL Server o desde un instalador independiente. Para obtener más información, consulte [Crear un R Server independiente](../../advanced-analytics/r-services/create-a-standalone-r-server.md) o [Introduction to R Server](https://msdnstage.redmond.corp.microsoft.com/en-us/microsoft-r/rserver?branch=r-server-nov16-dev) (Introducción a R Server).

 Para obtener más información sobre cómo usar el Cliente de Microsoft R para conectarse a SQL Server mediante los paquetes ScaleR, consulte [ScaleR Getting Started](https://msdn.microsoft.com/microsoft-r/scaler-getting-started#) (Introducción a ScaleR).  
  
 Para obtener un tutorial detallado sobre cómo conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la ejecución remota de código de R, consulte [Análisis detallado de ciencia de datos: Usar los paquetes de RevoScaleR](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md).  
  
## <a name="see-also"></a>Vea también  
 [Configurar SQL Server R Services &#40;en bases de datos&#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  
---
title: "Introducción a Microsoft R Server (independiente) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52347d0d-ce60-4bb8-98d2-6163e87716b0
caps.latest.revision: 21
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fc7874c6900474c7c2f3d927183616b2f5e69699
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="getting-started-with-microsoft-r-server-standalone"></a>Introducción a Microsoft R Server (independiente)
  Microsoft R Server (independiente) le ayuda a implementar en la empresa el popular lenguaje de código abierto R, que le permitirá habilitar las soluciones de análisis de alto rendimiento y la integración con otras aplicaciones empresariales.  

  
## <a name="install-microsoft-r-server"></a>Instalar Microsoft R Server 

La manera de instalar Microsoft R Server depende de si es necesario usar datos de SQL Server en las aplicaciones. Si es así, se debe instalar mediante el programa de instalación de SQL Server. Si no se van a usar datos de SQL Server, o si no se necesita ejecutar código de R en bases de datos, se puede usar el programa de instalación de SQL Server o el nuevo instalador independiente.
 
 
+ Instale Microsoft R Server (independiente) desde el programa de instalación de SQL Server. Se crea una instancia independiente de los archivos binarios de R para R Server y se concede licencia a la instancia a través de la directiva de soporte técnico de SQL Server Enterprise Edition. Para más información, vea [Create a Standalone R Server](../../advanced-analytics/r-services/create-a-standalone-r-server.md) (Crear un R Server independiente).  

+ Use el nuevo instalador independiente de Windows para crear una instancia nueva de Microsoft R Server que usa la directiva de soporte técnico del ciclo de vida de software moderno de Microsoft. Para más información, vea [Run Microsoft R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows) (Ejecutar Microsoft R Server para Windows).

+ Si tiene una instancia existente de R Server (independiente) o R Services que quiere actualizar, también debe descargar y ejecutar al instalador basado en Windows para la actualización. Para más información, vea [Run Microsoft R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows) (Ejecutar Microsoft R Server para Windows).
  
## <a name="install-additional-r-tools"></a>Instalar herramientas adicionales de R  

 Se recomienda [Microsoft R Client](http://aka.ms/rclient/download) (descarga gratuita).  

 También puede usar el entorno de desarrollo de R que prefiera para desarrollar soluciones para SQL Server R Services o Microsoft R Server. Para obtener más información, vea [Setup or Configure R Tools](../../advanced-analytics/r-services/setup-or-configure-r-tools.md) (Instalar o configurar herramientas de R). 
 

### <a name="location-of-r-server-binaries"></a>Ubicación de los archivos binarios de R Server

Según el método que se use para instalar Microsoft R Server, la ubicación predeterminada es diferente. Antes de empezar a usar el entorno de desarrollo preferido, compruebe que instaló las bibliotecas de R:

+ Microsoft R Server instalado con el nuevo instalador de Windows

  `C:\Program Files\Microsoft\R Server\R_SERVER`

+ R Server (independiente) se instala mediante el programa de instalación de SQL Server

  `C:\Program Files\Microsoft SQL Server\130\R_SERVER`

+ R Services (en bases de datos)

  `C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES`
      
## <a name="start-using-r-on-microsoft-r-server"></a>Empezar a usar R en Microsoft R Server  

 Después de configurar los componentes de servidor y el IDE de R para usar los archivos binarios de R Server, puede comenzar a desarrollar la solución mediante las nuevas API, como el paquete RevoScaleR, MicrosoftML y olapR.
    
Para empezar a trabajar con R Server, vea esta guía de MSDN Library: [R Server - Getting Started](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) (R Server: Introducción)   
  
-   [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started): explore este conjunto de funciones analíticas distribuibles que proporcionan alto rendimiento y escalabilidad para soluciones de R. Incluye versiones que se pueden usar en parelelo de muchos de los paquetes de R más conocidos, como agrupación en clústeres k-means, árboles y bosques de decisión, y herramientas para la manipulación de datos. Para más información, vea [Explore R and ScaleR in 25 Functions](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started-tutorial) (Explorar R y ScaleR en 25 funciones)  
    
- [MicrosoftML](https://msdn.microsoft.com/library/mt790482.aspx): el paquete MicrosoftML es un conjunto de nuevos algoritmos de aprendizaje automático y transformaciones desarrolladas en Microsoft que son rápidas y escalables. Para más información, vea [MicrosoftML functions](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml) (Funciones de MicrosoftML).
  


  
## <a name="see-also"></a>Vea también  
 [Introducción a SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  


---
title: Redistribuir ADOMD.NET | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1d4d5f06605f68e830aa945d0b502dcb657211f2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="redistributing-adomdnet"></a>Redistribuir ADOMD.NET
  Al escribir aplicaciones que utilizan ADOMD.NET, debe redistribuir la versión adecuada de ADOMD.NET junto con su aplicación. Para redistribuir ADOMD.NET, incluya el programa de instalación de ADOMD.NET en el programa de instalación de su aplicación.  
  
 El programa de instalación de ADOMD.NET, así como la versión más reciente de ADOMD.NET, se pueden encontrar en el Centro de descarga de Microsoft como parte del Feature Pack de SQL Server.  
  
 El programa de instalación ADOMD.NET instala los archivos ADOMD.NET en \< *unidad del sistema*>: \Program Files\Microsoft.NET\ADOMD.NET\\*número de versión*.  
  
 Después de incluir el programa de instalación de ADOMD.NET, haga que el programa de instalación de su aplicación inicie el programa de instalación de ADOMD.NET e instale ADOMD.NET. Además, según el entorno, puede que necesite asegurarse de que SQL Server confía en los ensamblados relacionados.  
  
 Para obtener más información:  
  
 [Feature Pack para Microsoft SQL Server](http://go.microsoft.com/fwlink/?LinkId=389949)  
  
 [Microsoft Connect: Dependencias ADOMD.NET](http://go.microsoft.com/fwlink/?LinkId=389950)  
  
## <a name="see-also"></a>Vea también  
 [Programación del cliente ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)   
 [Programación del servidor ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
  

---
title: Redistribuir ADOMD.NET | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- ADOMD.NET, redistributing
- redistributing ADOMD.NET
ms.assetid: f8db3c99-0243-4b92-b486-0d8786c264f4
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8c87db9dd22e53f8335dcbbb4994cd0835dfafcb
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="redistributing-adomdnet"></a>Redistribuir ADOMD.NET
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Al escribir aplicaciones que utilizan ADOMD.NET, debe redistribuir la versión adecuada de ADOMD.NET junto con la aplicación. Para redistribuir ADOMD.NET, incluya el programa de instalación de ADOMD.NET en el programa de instalación de su aplicación.  
  
 El programa de instalación de ADOMD.NET, así como la versión más reciente de ADOMD.NET, se pueden encontrar en el Centro de descarga de Microsoft como parte del Feature Pack de SQL Server.  
  
 El programa de instalación ADOMD.NET instala los archivos ADOMD.NET en \< *unidad del sistema*>: \Program Files\Microsoft.NET\ADOMD.NET\\*número de versión*.  
  
 Después de incluir el programa de instalación de ADOMD.NET, haga que el programa de instalación de su aplicación inicie el programa de instalación de ADOMD.NET e instale ADOMD.NET. Además, según el entorno, puede que necesite asegurarse de que SQL Server confía en los ensamblados relacionados.  
  
 Para obtener más información:  
  
 [Feature Pack para Microsoft SQL Server](http://go.microsoft.com/fwlink/?LinkId=389949)  
  
 [Microsoft Connect: Dependencias ADOMD.NET](http://go.microsoft.com/fwlink/?LinkId=389950)  
  
## <a name="see-also"></a>Vea también  
 [Programación del cliente ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)   
 [Programación del servidor ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
  

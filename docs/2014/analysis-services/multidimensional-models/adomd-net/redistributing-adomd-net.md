---
title: Redistribuir ADOMD.NET | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ADOMD.NET, redistributing
- redistributing ADOMD.NET
ms.assetid: f8db3c99-0243-4b92-b486-0d8786c264f4
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0451623dd44f5730a62e26232916a6c093155f3d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198788"
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
 [Programación del cliente ADOMD.NET](../../multidimensional-models-adomd-net-client/adomd-net-client-programming.md)   
 [Programación del servidor ADOMD.NET](../../multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
  
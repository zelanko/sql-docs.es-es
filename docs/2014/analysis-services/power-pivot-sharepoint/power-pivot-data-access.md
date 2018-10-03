---
title: Acceso a datos PowerPivot | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 83dc82da-91fb-4e47-91a8-0e0db67339b8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 75da2776f867ae89da049ba31a9180d21922cd84
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48164095"
---
# <a name="powerpivot-data-access"></a>Acceso a datos PowerPivot
  En este tema se describen las diferentes formar de recuperar datos de un libro PowerPivot publicado en una biblioteca de SharePoint.  
  
 Un libro PowerPivot se almacena dentro de un libro de Excel. La cadena de conexión es una dirección URL de un libro en un sitio de SharePoint.  
  
 Los datos PowerPivot los utiliza frecuentemente el libro que los contiene, como los datos detrás de tablas dinámicas y los gráficos dinámicos. De forma alternativa, los datos de PowerPivot se pueden utilizar como origen de datos externo, donde un libro, un panel, o un informe se conectan a un archivo independiente de Excel (.xlsx) en SharePoint y recuperan los datos para su uso posterior. Las herramientas cliente que utilizan normalmente datos PowerPivot son Excel, [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], otros informes de Reporting Services, y PerformancePoint.  
  
 En el escritorio, el complemento PowerPivot utiliza AMO y ADOMD.NET para crear, procesar y consultar los datos PowerPivot en el área de trabajo cliente.  
  
 En una granja de servidores de SharePoint, Excel Services utiliza el proveedor OLE DB MSOLAP local para conectarse a datos PowerPivot. El proveedor envía la solicitud de conexión a un servidor PowerPivot para SharePoint en la granja. Ese servidor carga los datos, ejecuta la consulta y devuelve el conjunto de resultados.  
  
##  <a name="queryproc"></a> Consultar datos PowerPivot en SharePoint  
 Al ver un libro PowerPivot de una biblioteca de SharePoint, los datos PowerPivot que están dentro del libro se detectan, extraen y procesan de forma independiente en las instancias de servidor de Analysis Services dentro de la granja, mientras Excel Services representa el nivel de presentación. Puede ver el libro procesado totalmente en una ventana del explorador o en una aplicación de escritorio de Excel 2010 que tenga el complemento de PowerPivot.  
  
 El siguiente diagrama muestra cómo se mueve a través de la granja una solicitud para el procesamiento de las consultas. Dado que los datos PowerPivot forman parte de un libro de Excel 2010, cuando un usuario abre un libro de Excel de una biblioteca de SharePoint e interactúa con una tabla dinámica o con un gráfico dinámico que contiene datos PowerPivot, se produce una solicitud para el procesamiento de consultas.  
  
 ![GMNI_DataProcReq](../media/gmni-dataprocreq.gif "GMNI_DataProcReq")  
  
 Los componentes Excel Services y PowerPivot para SharePoint procesan partes diferentes del mismo archivo de libro (.xlsx). Excel Services detecta los datos PowerPivot y solicita el procesamiento de un servidor de PowerPivot en la granja. El servidor de PowerPivot asigna la solicitud a una instancia de [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] , que extrae los datos del libro en la biblioteca de contenido y los carga. Los datos que están almacenados en memoria se combinan en el libro representado y se devuelven a Excel Web Access para presentarse en una ventana del explorador.  
  
 No todos los datos de un libro PowerPivot se administran en PowerPivot para SharePoint. Excel Services procesa las tablas y los datos de la celda en una hoja de cálculo. El servicio PowerPivot administra únicamente las tablas dinámicas, los gráficos dinámicos y las segmentaciones que tienen que ver con los datos PowerPivot para SharePoint.  
  
## <a name="see-also"></a>Vea también  
 [Conectarse a Analysis Services](../instances/connect-to-analysis-services.md)   
 [Acceso a datos de modelos tabulares](../tabular-models/tabular-model-data-access.md)  
  
  

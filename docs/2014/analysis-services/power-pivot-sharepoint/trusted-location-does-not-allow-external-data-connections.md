---
title: 'La ubicación de confianza donde el libro está almacenado no permite las conexiones de datos externos. No se pudieron actualizar las siguientes conexiones: datos PowerPivot | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: dc0cedfd-a7d0-40ef-bdd6-ea508130640a
author: minewiskan
ms.author: owend
ms.openlocfilehash: 30838d33cc6d4d71eaaaf820cd929a57f60f6e34
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547737"
---
# <a name="the-trusted-location-where-the-workbook-is-stored-does-not-allow-external-data-connections-the-following-connections-failed-to-refresh-powerpivot-data"></a>La ubicación de confianza donde el libro está almacenado no permite las conexiones de datos externos. No se pudieron actualizar las siguientes conexiones: datos PowerPivot
  En los libros de Excel que contienen los datos PowerPivot, Excel Services devuelve este error si no puede conectarse a orígenes de datos incrustados.  
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Se aplica a|PowerPivot para SharePoint|  
|Versión del producto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Excel Services se configura para denegar el acceso a datos externos.|  
|Texto del mensaje|La ubicación de confianza donde el libro está almacenado no permite las conexiones de datos externos. No se pudieron actualizar las siguientes conexiones: datos PowerPivot|  
  
## <a name="explanation"></a>Explicación  
 Los libros PowerPivot contienen conexiones de datos incrustados. Para admitir la interacción de los libros a través de segmentaciones y filtros, Servicios de Excel se debe configurar para permitir el acceso de datos externos a través de la información de las conexiones incrustadas. Se requiere acceso a los datos externos para recuperar los datos PowerPivot que se cargan en los servidores de PowerPivot de la granja.  
  
## <a name="user-action"></a>Acción del usuario  
 Cambie la configuración para permitir los orígenes de datos incrustados.  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Haga clic en **Aplicación de Servicios de Excel**.  
  
3.  Haga clic en **Ubicación de archivo de confianza**.  
  
4.  Haga clic en **http://** o en la ubicación que quiera configurar.  
  
5.  En Datos externos, en Permitir datos externos, haga clic en **Bibliotecas de conexiones de datos de confianza e incrustadas**.  
  
6.  Haga clic en **OK**.  
  
 O bien, puede crear una nueva ubicación de confianza para los sitios que contienen los libros PowerPivot y, a continuación, modificar la configuración solo para ese sitio. Para obtener más información, consulte [Create a trusted location for PowerPivot sites in Central Administration](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
  

---
title: Instalar ADO.NET Data Services para admitir datos fuente exportaciones de listas de SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: f32527ae-f623-4e08-adfb-6d3262f5c2ac
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 622d729e0b86a210bbdaaedf29818a49e81ed2ce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094662"
---
# <a name="install-adonet-data-services-to-support-data-feed-exports-of-sharepoint-lists"></a>Instalar ADO.NET Data Services para admitir las exportaciones de fuentes de distribución de datos de las listas de SharePoint
  ADO.NET Data Services se requiere para exportar fuentes de distribución de datos de las listas de SharePoint. SharePoint 2010 no incluye este componente en el programa instalador de requisitos previos de SharePoint, de modo que debe instalarlo manualmente.  
  
 Sin este requisito previo, obtendrá el siguiente error al intentar usar una lista de SharePoint que se exporta como una fuente de datos: "Por motivos de seguridad DTD está prohibida en este documento XML. Para habilitar el procesamiento DTD, establezca la propiedad ProhibitDtd de XmlReaderSettings en false y pase los ajustes al método XmlReader.Create".  
  
 Use las siguientes instrucciones para instalar ADO.NET Data Services en cada servidor de SharePoint para el que desee permitir que las listas se exporten como fuentes de distribución de datos.  
  
### <a name="download-and-install-adonet-data-services"></a>Descargar e instalar ADO.NET Data Services  
  
1.  Vaya a la documentación de los requisitos de hardware y software para SharePoint 2010, [requisitos de Hardware y Software (SharePoint 2010)](https://go.microsoft.com/fwlink/?LinkId=169734)  
  
2.  En **acceso a software aplicable**, busque el vínculo de ADO.NET Data Services 3.5 que corresponda al sistema operativo que están usando (ya sea Windows Server 2008 SP2 o Windows Server 2008 R2).  
  
3.  Haga clic en el vínculo y ejecute el programa de instalación que instala el servicio.  
  
## <a name="see-also"></a>Vea también  
 [Instalación de PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  

---
title: Instale ADO.NET Data Services para admitir las exportaciones de fuentes de distribución de datos de las listas de SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: f32527ae-f623-4e08-adfb-6d3262f5c2ac
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: b9b3ec2d8b7459f9d66313c6a40b1cbc26450e0d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952163"
---
# <a name="install-adonet-data-services-to-support-data-feed-exports-of-sharepoint-lists"></a>Instalar ADO.NET Data Services para admitir las exportaciones de fuentes de distribución de datos de las listas de SharePoint
  ADO.NET Data Services se requiere para exportar fuentes de distribución de datos de las listas de SharePoint. SharePoint 2010 no incluye este componente en el programa instalador de requisitos previos de SharePoint, de modo que debe instalarlo manualmente.  
  
 Sin este requisito previo, obtendrá el siguiente error cuando intente usar una lista de SharePoint exportada como fuente de distribución de datos: "Por motivos de seguridad, DTD se prohíbe en este documento XML. Para habilitar el procesamiento DTD, establezca la propiedad ProhibitDtd de XmlReaderSettings en false y pase los ajustes al método XmlReader.Create".  
  
 Use las siguientes instrucciones para instalar ADO.NET Data Services en cada servidor de SharePoint para el que desee permitir que las listas se exporten como fuentes de distribución de datos.  
  
### <a name="download-and-install-adonet-data-services"></a>Descargar e instalar ADO.NET Data Services  
  
1.  Vaya a la documentación de los requisitos de hardware y software para SharePoint 2010, [requisitos de hardware y software (SharePoint 2010)](https://go.microsoft.com/fwlink/?LinkId=169734)  
  
2.  En **acceso a software aplicable**, busque el vínculo de ADO.NET Data Services 3,5 que corresponda al sistema operativo que usa (windows Server 2008 SP2 o windows Server 2008 R2).  
  
3.  Haga clic en el vínculo y ejecute el programa de instalación que instala el servicio.  
  
## <a name="see-also"></a>Consulte también  
 [Instalación de PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  

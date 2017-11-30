---
title: "Quitar una extensión de procesamiento de datos | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- deleting data processing extensions
- data processing extensions [Reporting Services], removing
- removing data processing extensions
ms.assetid: 1d89e32b-0631-44f6-8178-a57fb791d26d
caps.latest.revision: "34"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 39443e97e7167bfa86b9e946232bca44acae53e5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="removing-a-data-processing-extension"></a>Quitar una extensión de procesamiento de datos
  Para quitar una extensión de procesamiento de datos, basta con quitar el elemento **Extension** de la extensión de procesamiento de datos del archivo de configuración. Si ha realizado entradas para un servidor de informes así como para el Diseñador de informes, quite el elemento **Extension** de los archivos RSReportServer.config y RSReportDesigner.config. Después de quitar la información de configuración, la extensión de procesamiento de datos ya no estará disponible en el componente.  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementar una extensión de procesamiento de datos](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Biblioteca de extensiones de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

---
title: Quitar una extensión de representación | Microsoft Docs
ms.date: 03/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- deleting rendering extensions
- removing rendering extensions
- rendering extensions [Reporting Services], removing
ms.assetid: 2abfebfb-065f-45cc-a904-c914394cf900
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0ee3563074e2379061006b72f55dab99f80094cd
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "63193453"
---
# <a name="removing-a-rendering-extension"></a>Quitar una extensión de representación
  Para quitar una extensión de representación de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], basta con quitar el elemento **Extension** de la extensión de representación del archivo rsreportserver.config, situado en la carpeta **%Archivos de programa%\Microsoft SQL Server\MSRS10_50.\<Nombre de la instancia>\Reporting Services\ReportServer**. Si efectuó entradas para un Diseñador de informes y para un servidor de informes, quite el elemento **Extension** también del [archivo de configuración RSReportDesigner](../../../reporting-services/report-server/rsreportdesigner-configuration-file.md). Después de quitar la información de configuración, la extensión de representación de datos ya no estará disponible en el componente.  
  
## <a name="see-also"></a>Consulte también  
 [Archivos de configuración de Reporting Services](../../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Implementar una extensión de representación](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [Información general de las extensiones de representación](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)   
 [Implementar la interfaz IRenderingExtension](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)   
 [Consideraciones de seguridad para las extensiones](../../../reporting-services/extensions/security-considerations-for-extensions.md)   
 [Implementación de una extensión de representación](../../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
  

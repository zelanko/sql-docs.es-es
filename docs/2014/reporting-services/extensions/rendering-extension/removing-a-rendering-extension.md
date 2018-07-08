---
title: Quitar una extensión de representación | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- deleting rendering extensions
- removing rendering extensions
- rendering extensions [Reporting Services], removing
ms.assetid: 2abfebfb-065f-45cc-a904-c914394cf900
caps.latest.revision: 37
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: dd559679afa7575f285737f289f66201fd06671e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37153036"
---
# <a name="removing-a-rendering-extension"></a>Quitar una extensión de representación
  Para quitar un [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] extensión de representación, basta con quitar el `Extension` (elemento) para la extensión de representación del archivo rsreportserver.config, situado en **%ProgramFiles%\Microsoft SQL Server\MSRS10_50.\< Nombre de instancia > \Reporting** carpeta. Si efectuó entradas para un diseñador de informes, así como un servidor de informes, quite el `Extension` elemento desde el [RSReportDesigner Configuration File](../../report-server/rsreportdesigner-configuration-file.md) también. Después de quitar la información de configuración, la extensión de representación de datos ya no estará disponible en el componente.  
  
## <a name="see-also"></a>Vea también  
 [Archivos de configuración de Reporting Services](../../report-server/reporting-services-configuration-files.md)   
 [Implementar una extensión de representación](implementing-a-rendering-extension.md)   
 [Información general de las extensiones de representación](rendering-extensions-overview.md)   
 [Implementar la interfaz IRenderingExtension](implementing-the-irenderingextension-interface.md)   
 [Consideraciones de seguridad para las extensiones](../security-considerations-for-extensions.md)   
 [Implementación de una extensión de representación](deploying-a-rendering-extension.md)  
  
  

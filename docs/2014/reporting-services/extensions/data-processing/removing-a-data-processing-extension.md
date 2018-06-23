---
title: Quitar una extensión de procesamiento de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- deleting data processing extensions
- data processing extensions [Reporting Services], removing
- removing data processing extensions
ms.assetid: 1d89e32b-0631-44f6-8178-a57fb791d26d
caps.latest.revision: 33
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 0ea72edfcea9935b858631a639ec51f67a3feeac
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199078"
---
# <a name="removing-a-data-processing-extension"></a>Quitar una extensión de procesamiento de datos
  Para quitar una extensión de procesamiento de datos, basta con quitar el elemento **Extension** de la extensión de procesamiento de datos del archivo de configuración. Si ha realizado entradas para un servidor de informes así como para el Diseñador de informes, quite el elemento **Extension** de los archivos RSReportServer.config y RSReportDesigner.config. Después de quitar la información de configuración, la extensión de procesamiento de datos ya no estará disponible en el componente.  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de Reporting Services](../reporting-services-extensions.md)   
 [Implementar una extensión de procesamiento de datos](implementing-a-data-processing-extension.md)   
 [Biblioteca de extensiones de Reporting Services](../reporting-services-extension-library.md)  
  
  
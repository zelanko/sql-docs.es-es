---
title: Exportar un informe mediante el acceso URL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- formats [Reporting Services], URL rendering
- URL access [Reporting Services], rendering formats
ms.assetid: 6a3b7fc3-3d91-4d12-8371-42ea12e74517
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 69f340855e37ffde49aec0af096c094a142659d1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109190"
---
# <a name="export-a-report-using-url-access"></a>Exportar un informe mediante el acceso URL
  Opcionalmente, puede especificar el formato en el que se va a representar un informe de utilizando el *rs: Format* parámetro. Por ejemplo, para obtener una copia PDF de un informe directamente desde un servidor de informes en modo nativo:  
  
```  
http://myrshost/ReportServer?/myreport&rs:Format=PDF  
```  
  
 Y desde un servidor de informes en el modo integrado de SharePoint:  
  
```  
http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/myrereport.rdl&rs:Format=PDF  
```  
  
 Los valores válidos para este parámetro están basados en las extensiones de representación del informe instaladas en el servidor de informes al que se está obteniendo acceso. Las extensiones comunes son HTML4.0, MHTML, IMAGE, EXCEL, WORD, CSV, PDF, XML y NULL. Si una extensión de representación especificada no se instala en el servidor de informes, no se representa el informe y se genera un error que se muestra en el explorador.  
  
 Si no incluye el parámetro *Format* como parte de la dirección URL, el servidor de informes detecta el explorador y representa el informe en el formato HTML adecuado.  
  
## <a name="see-also"></a>Vea también  
 [Acceso URL &#40;SSRS&#41;](url-access-ssrs.md)   
 [Referencia de parámetros de acceso URL](url-access-parameter-reference.md)  
  
  

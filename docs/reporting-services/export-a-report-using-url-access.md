---
title: Exportar un informe mediante el acceso URL | Microsoft Docs
description: Obtenga información sobre cómo exportar un informe mediante el acceso URL si especifica el formato en el que se va a representar un informe mediante el parámetro de URL rs:Format.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- formats [Reporting Services], URL rendering
- URL access [Reporting Services], rendering formats
ms.assetid: 6a3b7fc3-3d91-4d12-8371-42ea12e74517
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d61f509fa07528b71cd7cbb23488bc14f33959ae
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472496"
---
# <a name="export-a-report-using-url-access"></a>Exportar un informe mediante el acceso URL
  Opcionalmente, puede especificar el formato en el que se representará un informe mediante el parámetro de dirección URL *rs:Format* .  Los formatos HTML4.0 y HTM5 (extensión de representación) se representarán en el explorador y en otros formatos; el explorador le solicitará que guarde la salida del informe en un archivo local.  
  
 Por ejemplo, para obtener una copia PDF de un informe directamente desde un servidor de informes en modo nativo:  
  
```  
https://myrshost/ReportServer?/myreport&rs:Format=PDF  
```  

::: moniker range="=sql-server-2016"
  
 Y desde un servidor de informes en el modo integrado de SharePoint:  
  
```  
https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/myrereport.rdl&rs:Format=PDF  
```  
 
::: moniker-end
 
 Por ejemplo, el siguiente comando de dirección URL del explorador exporta un informe PPTX desde una instancia con nombre del servidor de informes:  
  
```  
https://servername/ReportServer_THESQLINSTANCE/Pages/ReportViewer.aspx?%2freportfolder%2freport+name+with+spaces&rs:Format=pptx  
```  
  
 Los valores válidos para este parámetro están basados en las extensiones de representación del informe instaladas en el servidor de informes al que se está obteniendo acceso. Las extensiones comunes son HTML4.0, MHTML, IMAGE, EXCELOPENXML (xlsx), WORDOPENXML (docx), CSV, PDF, XML y NULL. Si una extensión de representación especificada no se instala en el servidor de informes, no se representa el informe y se genera un error que se muestra en el explorador.  
  
 Si no incluye el parámetro *Format* como parte de la dirección URL, el servidor de informes detecta el explorador y representa el informe en el formato HTML adecuado.  
  
## <a name="see-also"></a>Consulte también  
 [Acceso URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [Referencia de parámetros de acceso URL](../reporting-services/url-access-parameter-reference.md)  
  
  

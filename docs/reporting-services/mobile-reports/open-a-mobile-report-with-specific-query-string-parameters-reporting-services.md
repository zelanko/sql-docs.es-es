---
title: Abrir un informe móvil con determinados parámetros de cadena de consulta | Microsoft Docs
ms.date: 10/25/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 4eeb3204-e207-4ac0-aff3-bfc4926e5754
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7204574d10b674c7cea4e08fb570c3550fe33e03
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62500019"
---
# <a name="open-a-mobile-report-with-specific-query-string-parameters--reporting-services"></a>Abrir un informe móvil con determinados parámetros de cadena de consulta | Reporting Services
Si tiene un informe móvil de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] con parámetros y un origen de datos de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)], puede incluir parámetros de cadena de consulta en la dirección URL del informe para que se abra automáticamente con los valores especificados. 
1.  Cree un [informe móvil con parámetros](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md).

2. Abra el informe en Publicador de informes móviles y seleccione la pestaña Datos. 

2. Busque el nombre del conjunto de datos en la pestaña que se encuentra en la parte inferior de la tabla y el nombre de campo que desee. 
    
    ![mobile-report-publisher-parameter-data-view](../../reporting-services/mobile-reports/media/mobile-report-publisher-parameter-data-view.png)
    
2.  La sintaxis de la dirección URL depende de su origen de datos. 

     **Para un origen de datos de SQL Server Analysis Services**: cree una dirección URL con un parámetro de cadena de consulta en este formato:

    `https://<servername>/reports/<report-folder-name>/<report-name>?<dataset-name>.<field-name>=<parameter-value>`

    Por ejemplo:
    
    `https://sampleserver/reports/adventureworks-reports/adventureworks-load-on-demand?TimeChartLoD.category=Clothing` 
    
     **Para un origen de datos de SQL Server**: el parámetro de cadena de consulta es prácticamente el mismo, pero tiene el símbolo \@ delante del nombre de campo:

    `https://<servername>/reports/<report-folder-name>/<report-name>?<dataset-name>.@<field-name>=<parameter-value>`

    Por ejemplo:
    
      `https://sampleserver/reports/adventureworks-reports/adventureworks-load-on-demand?TimeChartLoD.@category=Clothing` 

    
3.  Esta dirección URL abrirá el informe en el servidor, el que se filtrará automáticamente según el valor de parámetro que especificó.

    ![mobile-report-publisher-parameter-web-portal-view](../../reporting-services/mobile-reports/media/mobile-report-publisher-parameter-web-portal-view.png)

### <a name="see-also"></a>Vea también

[Agregar parámetros a un informe para dispositivos móviles](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)


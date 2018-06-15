---
title: Conservar el formato de fecha para Analysis Services en los informes para dispositivos móviles | Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: mobile-reports
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e9a9a199-40e3-4381-b250-1b99fb83aa62
caps.latest.revision: 3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 440a2b60469019c2dc2692df40090f8f887936cc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33019162"
---
# <a name="retain-date-formatting-for-analysis-services-in-mobile-reports"></a>Conservar el formato de fecha para Analysis Services en los informes para dispositivos móviles
Agregue una medida a un conjunto de datos compartido en el Generador de informes para que las fechas de los orígenes de datos de [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] conserven su tipo de datos en el [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)].

El tipo de valor devuelto predeterminado de las consultas de [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] es una cadena.  Cuando se genera un conjunto de datos en el Generador de informes de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , el tipo de cadena se respeta y se guarda en el servidor. 

Pero cuando el representador de tablas JSON procesa el conjunto de datos, lee el valor de la columna como una cadena y, como tal, muestra cadenas.  De ahí que luego, cuando el [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)] capture la tabla, solo verá cadenas.

Para solucionar esto, agregue un miembro calculado al crear un conjunto de datos compartido en el Generador de informes. Esto funciona para modelos tanto multidimensionales como tabulares de [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] .

## <a name="create-a-measure-to-retain-a-date-field-data-type"></a>Crear una medida para conservar un tipo de datos del campo de fecha

1. Cree una medida que contenga el valor del campo de fecha en cuestión y, en el campo de expresión, elija el nivel o la jerarquía de la fecha y anexe **.CurrentMember.MemberValue**. Por ejemplo:
 
   [Internet Sales].[Ship Date].CurrentMember.MemberValue
   
   ![ssas-calculated-member-report-builder](../../reporting-services/mobile-reports/media/ssas-calculated-member-report-builder.png)
   
2. Ahora puede anexar este miembro calculado al conjunto de columnas; para ello, arrástrelo desde la lista de miembros calculados en la parte inferior izquierda y colóquelo en la cuadrícula de columnas de la derecha.  

   ![ssas-query-designer-calculated-member-report-builder](../../reporting-services/mobile-reports/media/ssas-query-designer-calculated-member-report-builder.png) 
   
### <a name="see-also"></a>Vea también

-  [Datos para informes para dispositivos móviles de Reporting Services](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)
-  [Preparar datos para informes para dispositivos móviles de Reporting Services](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)

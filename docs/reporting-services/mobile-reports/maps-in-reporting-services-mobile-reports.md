---
title: "Mapas en informes para dispositivos móviles de Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 50658295-a71c-441e-8eba-e1ef066629c0
caps.latest.revision: "10"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 975ad199788370f01686c50d5dcc05f093c31f50
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="maps-in-reporting-services-mobile-reports"></a>Mapas en informes para dispositivos móviles de Reporting Services
Los mapas constituyen una forma excelente de visualizar datos geográficos. [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)] ofrece tres tipos distintos de visualización en mapas, así como mapas integrados para continentes y diversos países individuales. También puede [cargar y usar mapas personalizados](../../reporting-services/mobile-reports/custom-maps-in-reporting-services-mobile-reports.md).   
  
## <a name="types-of-maps"></a>Tipos de mapas  
  
Los informes móviles de SQL Server ofrecen tres tipos distintos de mapas, que resultan útiles para diferentes circunstancias.  
  
![SSMRP_MapsGallery](../../reporting-services/mobile-reports/media/ssmrp-mapsgallery.png)  
  
**Mapas térmicos de degradado** . El campo de la propiedad Valores se muestra como tonalidades de un solo color con las que se rellena cada región del mapa. Puede establecer si los valores superiores o inferiores son más oscuros en el cuadro **Value Direction** (Dirección del valor).  
  
**Mapa de burbujas** . La propiedad Valores determina el radio de una visualización de burbujas mostrada sobre la región asociada. Puede establecer si todas las burbujas presentan el mismo color o uno distinto.   
  
**Mapas térmicos de umbrales de rangos** . Estos muestran un valor en relación con un objetivo. La propiedad **Destinos** determina la diferencia entre los campos Comparación y Valores. La diferencia resultante determina el color que rellena la región asociada del mapa, de verde a rojo, pasando por amarillo. Puede establecer si los valores superiores o inferiores son verdes en el cuadro **Value Direction** (Dirección del valor).  
  
## <a name="select-the-map-type-and-region"></a>Selección del tipo de mapa y la región  
  
1. En la pestaña **Diseño**, seleccione un tipo de mapa, arrástrelo a la superficie de diseño y modifique su tamaño hasta que se ajuste a sus requisitos.  
  
2. En la vista **Diseño** > panel **Visual Properties** (Propiedades visuales) > **Mapa**, seleccione el mapa de la región concreta que necesite.  
  
   ![SSMRP_SelectMap](../../reporting-services/mobile-reports/media/ssmrp-selectmaps.png)  
  
3. Para los mapas térmicos de umbrales de rangos y degradado, establezca si los valores superiores o inferiores son mejores en el cuadro **Value Direction** (Dirección del valor) situado bajo **Visual Properties**(Propiedades visuales).  
  
7. Para los mapas de burbujas, en **Visual Properties** (Propiedades visuales), establezca **Use Different Colors** (Utilizar colores distintos) en **Activado** o **Desactivado** para teñir a las burbujas del mismo color o de distintos.  
  
## <a name="select-the-map-data"></a>Selección de los datos del mapa  
Cuando agregue un mapa a su informe por primera vez, [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] lo rellena con datos geográficos simulados.  
  
![SSMRP_MapsData](../../reporting-services/mobile-reports/media/ssmrp-mapsdata.png)  
  
Para mostrar los datos reales en el mapa, debe establecer los valores de, como mínimo, dos de las propiedades de datos este:   
* La propiedad **Claves** conecta los datos para regiones específicas del mapa (por ejemplo, estados de los EE. UU. o países de África).  
* La propiedad **Valores** es un campo numérico situado en la misma tabla que el campo Claves seleccionado. Estos valores se representan de forma diferente en distintos mapas. En el **mapa de degradado** , se utilizan estos valores para dar color a cada región, que presentarán distintas tonalidades en función del intervalo de valores. En el **mapa de burbujas** , el tamaño de las burbujas mostradas sobre cada región se basa en la propiedad de valor.   
* En cuanto a los mapas térmicos de umbrales de rangos, tendrá que establecer un valor para la propiedad **Destinos** .  
  
### <a name="set-map-data-properties"></a>Configuración de las propiedades de datos del mapa  
  
1. Seleccione la pestaña **Datos** , situada en la esquina superior izquierda.  
  
2. Seleccione **Agregar datos**y, después, **Local Excel** (Excel local) o **SSRS Server**(Servidor de SSRS).  
  
   > **Sugerencia**: asegúrese de que [los datos están en un formato apto para informes para dispositivos móviles](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md).  
  
3. Elija las hojas de cálculo que desee y seleccione **Importar**.  
   Verá los datos en el [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)].  
  
4. En esta vista **Datos** > panel **Propiedades de datos** > **Claves**, en el cuadro izquierdo, seleccione la tabla que contenga los datos del mapa y, en el cuadro de la derecha, seleccione el campo de clave que coincida con las regiones del mapa.  
  
5. En **Valores**, la misma tabla ya se encontrará en el cuadro izquierdo. Seleccione el campo numérico cuyos valores desee mostrar en el mapa.   
  
6. Si se trata de un mapa térmico de umbrales de rangos, en el cuadro **Destinos** la misma tabla se encuentra en el cuadro izquierdo. En el cuadro de la derecha, seleccione el campo numérico cuyos valores desea que sea el destino.   
  
   ![SSMRP_MapRangeHeatData](../../reporting-services/mobile-reports/media/ssmrp-maprangeheatdata.png)  
  
7. Seleccione **Vista previa** en la esquina superior izquierda.  
  
   ![SSMRP_MapRangeHeatPreview](../../reporting-services/mobile-reports/media/ssmrp-maprangeheatpreview.png)  
     
8. Seleccione el icono de **Guardar** , situado en la esquina superior izquierda, y elija entre **guardar el mapa localmente** en su equipo o **guardarlo en el servidor**.  
  
### <a name="see-also"></a>Vea también  
-  [Mapas personalizados en informes para dispositivos móviles de Reporting Services](../../reporting-services/mobile-reports/custom-maps-in-reporting-services-mobile-reports.md)  
- [Create and publish mobile reports with SQL Server Mobile Report Publisher (Creación y publicación de informes móviles con el Publicador de informes de SQL Server Mobile)](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
  
  

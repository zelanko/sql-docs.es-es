---
title: Implementar una solución de minería de datos en versiones anteriores de SQL Server | Documentos de Microsoft
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1065afdc558defa467c440f8a767078ace97d5cc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="deploy-a-data-mining-solution-to-previous-versions-of-sql-server"></a>Implementar soluciones de minería de datos para versiones anteriores de SQL Server
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  En esta sección se describen problemas conocidos de compatibilidad que pueden surgir al intentar implementar un modelo o estructura de minería de datos que se creó en una instancia de [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] en una base de datos que utiliza SQL Server 2005 Analysis Services, o al implementar modelos creados en SQL Server 2005 en una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 No se admite la implementación en una instancia de SQL Server 2000 Analysis Services.  
  
 [Implementar modelos de serie temporal](#bkmk_TimeSeries)  
  
 [Implementar modelos con exclusión](#bkmk_Holdout)  
  
 [Implementar modelos con filtros](#bkmk_Filter)  
  
 [Restaurar a partir de copias de seguridad de base de datos](#bkmk_Backup)  
  
 [Usar la sincronización de bases de datos](#bkmk_Synch)  
  
##  <a name="bkmk_TimeSeries"></a> Implementar modelos de serie temporal  
 El algoritmo de serie temporal de Microsoft se mejoró en SQL Server 2008 mediante la adición de un segundo algoritmo complementario: ARIMA. Para obtener más información sobre los cambios en el algoritmo de serie temporal, vea [Algoritmo de serie temporal de Microsoft](../../analysis-services/data-mining/microsoft-time-series-algorithm.md).  
  
 Por consiguiente, los modelos de minería de datos de serie temporal que utilizan el nuevo algoritmo ARIMA pueden comportarse de manera diferente cuando se implementan en una instancia de SQL Server 2005 Analysis Services.  
  
 Si ha establecido explícitamente el parámetro PREDICTION_SMOOTHING para controlar la combinación de los modelos ARIMA y ARTXP en la predicción, al implementar este modelo en una instancia de SQL Server 2005, Analysis Services generará un error que indica que el parámetro no es válido. Para evitar este error, debe eliminar el parámetro PREDICTION_SMOOTHING y convertir los modelos en un modelo ARTXP puro.  
  
 Por el contrario, si implementa un modelo de serie temporal que se creó mediante SQL Server 2005 Analysis Services en una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], al abrir el modelo de minería de datos en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], los archivos de definición se convierten primero al nuevo formato y se agregan dos parámetros nuevos de forma predeterminada a todos los modelos de serie temporal. El parámetro FORECAST_METHOD se agrega con el valor predeterminado MIXED y el parámetro PREDICTION_SMOOTHING se agrega con el valor predeterminado 0,5. Sin embargo, el modelo continuará utilizando únicamente ARTXP para la predicción hasta que se vuelva a procesar el modelo. En cuanto se vuelva a procesar el modelo, la predicción cambia para utilizar ARIMA y ARTXP.  
  
 Por consiguiente, si desea evitar cambiar el modelo, únicamente debería examinar el modelo y nunca procesarlo. O bien, podría establecer explícitamente los parámetros PREDICTION_SMOOTHING o FORECAST_METHOD.  
  
 Para obtener información detallada sobre cómo configurar los modelos mixtos, vea [Referencia técnica del algoritmo de serie temporal de Microsoft](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md).  
  
 Si el proveedor que se utiliza para el origen de datos del modelo es SQL Client Data Provider 10, también debe modificar la definición del origen de datos para especificar la versión anterior de SQL Server Native Client. De lo contrario, [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] genera un error que indica que el proveedor no está registrado.  
  
##  <a name="bkmk_Holdout"></a> Implementar modelos con exclusión  
 Si crea una estructura de minería de datos que contiene una partición de exclusión que se usa para probar los modelos de minería de datos, la estructura de minería de datos se puede implementar en una instancia de SQL Server 2005, pero la información de partición se perderá.  
  
 Al abrir la estructura de minería de datos en SQL Server 2005 Analysis Services, [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] produce un error y, a continuación, vuelve a generar la estructura para quitar la partición de datos de exclusión.  
  
 Después de que se ha vuelto a generar la estructura, el tamaño de la partición de exclusión ya no está disponible en la ventana Propiedades; Sin embargo, el valor \<ddl100_100: holdoutmaxpercent > 30\</ddl100_100:HoldoutMaxPercent >) pueden estar aún presentes en el archivo de script ASSL.  
  
##  <a name="bkmk_Filter"></a> Implementar modelos con filtros  
 Si aplica un filtro a un modelo de minería de datos, se puede implementar el modelo a una instancia de SQL Server 2005, pero no se aplicará el filtro.  
  
 Al abrir el modelo de minería de datos, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] produce un error y, a continuación, vuelve a generar el modelo para quitar el filtro.  
  
##  <a name="bkmk_Backup"></a> Restaurar a partir de copias de seguridad de base de datos  
 No puede restaurar una copia de seguridad de base de datos que haya creado en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] a una instancia de SQL Server 2005. Si lo hace, SQL Server Management Studio genera un error.  
  
 Si crea una copia de seguridad de una base de datos de SQL Server 2005 Analysis Services y la restaura en una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], todos los modelos de serie temporal se modifican según se describe en la sección anterior.  
  
##  <a name="bkmk_Synch"></a> Usar la sincronización de bases de datos  
 La sincronización de bases de datos no se admite entre [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y SQL Server 2005.  
  
 Si intenta sincronizar una base de datos de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , el servidor devuelve un error de sincronización de base de datos.  
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad con versiones anteriores de Analysis Services](../../analysis-services/analysis-services-backward-compatibility.md)  
  
  

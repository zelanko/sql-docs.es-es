---
title: Preparación de los datos de Excel para informes móviles de Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: ''
ms.component: mobile-reports
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 16698f8d-bfc7-4eca-9e97-82c99d8bc08e
caps.latest.revision: ''
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 57440dd767e421cb1448d8d365ebf894edbd065a
ms.sourcegitcommit: 6b1618aa3b24bf6759b00a820e09c52c4996ca10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/15/2018
---
# <a name="prepare-excel-data-for-reporting-services-mobile-reports"></a>Preparación de los datos de Excel para informes móviles de Reporting Services
  
A continuación se exponen algunos aspectos que debe tener en cuenta a la hora de preparar un archivo y hojas de cálculo de Excel para utilizarlos con un informe móvil:  
  
## <a name="do"></a>Lo que es necesario hacer:  
  
- Contar con una hoja de cálculo para cada conjunto de datos.  
- Tener encabezados de columna en la primera fila.  
- Mantener la coherencia de los tipos de datos dentro de cada columna.  
- Dar formato a las celdas con los tipos pertinentes en Excel.  
- Tener los datos en hojas de cálculo, no en el modelo de datos en Excel.  
- Asegurarse de que toda la columna se calcula utilizando la misma fórmula (en el caso de que se utilice alguna).  
- Utilizar Excel 2007 o posterior.  
- Guardar los archivos de Excel con la extensión XLSX.  
          
## <a name="dont"></a>Lo que debe evitar:  
  
- Incluir imágenes, gráficos, tablas dinámicas u otros objetos incrustados en las hojas de cálculo del conjunto de datos.  
- Incluir filas totales o calculadas.  
- Mantener el archivo abierto en Excel al importar.  
- Dar formato a números manualmente mediante la adición de símbolos de moneda o de otro tipo.  
- Utilizar un libro con los datos almacenados en el modelo de datos.  
  
## <a name="worksheets"></a>Hojas de cálculo  
          
Al preparar un archivo de Excel como un conjunto de datos para un informe móvil, asegúrese de que tiene un único conjunto de datos por hoja de cálculo. Cada hoja de cálculo individual se importa en el [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] como una tabla independiente. Si hay hojas de cálculo que se llamen igual y que procedan de varios orígenes de Excel, sus nombres se cambian al realizar la importación anexando números en sucesión creciente. Por ejemplo, si un libro tiene tres hojas de cálculo denominadas "MiHojaDeCálculo", se cambia el nombre de la segunda y la tercera a "MiHojaDeCálculo0" y "MiHojaDeCálculo1", respectivamente. En la captura de pantalla siguiente se muestran las primeras filas de una hoja de cálculo de Excel ideal lista para su importación.  
  
![SS_MRP_ExcelDataSheet](../../reporting-services/mobile-reports/media/ss-mrp-exceldatasheet.png)  
          
## <a name="column-headers"></a>Encabezados de columna  
  
Como puede ver en el ejemplo anterior, la primera fila contiene el nombre de la métrica de esa columna. [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] conserva estos encabezados de columna para que resulte más fácil hacer referencia a las columnas en la configuración del elemento de la galería. Sin embargo, los encabezados de columna no tienen un carácter obligatorio. Si faltan, el [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] genera encabezados utilizando la convención A, B, C..., AA, BB... (y así sucesivamente) de Excel.  
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] detecta automáticamente los encabezados de la primera fila al importar hojas de cálculo de Excel con la comparación de los tipos de datos de las dos primeras celdas en cada columna. Si no coinciden los tipos de datos de las dos primeras celdas de cualquier columna, se determina que la primera fila contiene encabezados de columna. Por lo tanto, si una tabla tiene encabezados de columna numéricos, escriba una cadena antes de los nombres de los encabezados para que se detecten como tales en el proceso de importación.  
  
## <a name="cells"></a>Celdas  
  
Los datos de las celdas de cada columna de un conjunto de datos en una hoja de cálculo deben ser coherentes. Cuando se efectúa la importación, se asigna un tipo de datos a cada columna. [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] detecta automáticamente los tipos de datos como cadena, doble (numérico), booleano (verdadero/falso) o datetime. Si hay varios tipos de datos en la misma columna, es posible que la detección sea imprecisa o no se realice en absoluto. Esta detección tiene en cuenta posibles encabezados de columna con el tipo de cadena. Se debe aplicar el formato del tipo correcto a las celdas en Excel para garantizar que el [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] detecta los tipos deseados. En el ejemplo anterior, las seis columnas se identificarían con los siguientes tipos:  
*  Una columna datetime  
*  Una columna de cadena  
*  Cuatro columnas dobles  
  
Si una hoja de cálculo contiene celdas calculadas o fórmulas, solo se importa en el [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]el valor mostrado resultante.  
  
## <a name="file-location-and-refreshing-excel-data"></a>Ubicación del archivo y actualización de los datos de Excel  
  
No existen restricciones en lo relativo a la ubicación donde puede almacenar los archivos de Excel que importe en el [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]. Sin embargo, si mueve el archivo o cambia su nombre después de importarlo, no podrá actualizar los datos con el comando **Actualizar todos los datos** que se encuentra en la vista de datos.   
  
>**Nota**: el [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] no actualiza automáticamente los datos de Excel. Puede actualizar los datos mediante el comando [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] **refresh** command, but only if the file hasn't moved.  
  
## <a name="dates"></a>Fechas  
  
Los campos de fecha resultan esenciales para muchos informes móviles, por lo que deberá asegurarse de que las celdas pertinentes tienen el formato de fecha adecuado en Excel. En algunos casos, esto significa que se debe efectuar una conversión. A continuación se muestran ejemplos de fórmulas para convertir las celdas de texto en fechas en Excel.  
  
    Week 24-2013=DATE(MID(A2,9,4),1,-2)-WEEKDAY(DATE(MID(A2,9,4),1,3))+MID(A2,6,2)*7  
  
    2013/03/21=DATEVALUE(A1)  
  
    2013-mar-12=DATEVALUE(RIGHT(A1,2)&"-"&MID(A1,6,3)&"-"&LEFT(A1,4))  
  
Después de convertir las celdas, tiene que darles el formato de fecha; para hacerlo, seleccione las celdas o toda la columna y siga estos pasos: **menú contextual** > **Formato de celdas** > **Fecha** en la lista **Categoría**. También puede utilizar al Asistente para convertir texto en columnas a fin de transformar las celdas de texto en fechas con el formato correcto.  
  
## <a name="unsupported"></a>No compatible  
  
Los datos de hojas de cálculo con formatos distintos a los descritos anteriormente podrían conllevar resultados imprevisibles cuando se realice la importación. Se recomienda restringir las hojas de cálculo de un archivo de Excel a únicamente aquellas con el formato correcto para su uso con un informe móvil.  
  
Los objetos personalizados de hojas de cálculo de Excel, como tablas dinámicas, visualizaciones e imágenes, no se importan en el [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)].  
  
### <a name="see-also"></a>Vea también  
- [Preparar datos para informes de Reporting Services móviles](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)  
- [Create and publish mobile reports with SQL Server Mobile Report Publisher (Creación y publicación de informes móviles con el Publicador de informes de SQL Server Mobile)](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  Ver [informes móviles y KPI de SQL Server en la aplicación de iPad](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  (Power BI para iOS)  
-  Ver [informes móviles y KPI de SQL Server en la aplicación de iPhone](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-iphone-kpis-mobile-reports) (Power BI para iOS)  
  
  
  
  
  
  
  


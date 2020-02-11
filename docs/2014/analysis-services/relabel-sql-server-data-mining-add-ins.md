---
title: Cambiar etiquetas (SQL Server complementos de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data preparation
- relabel
- data cleaning
ms.assetid: af041b39-fdd1-4cb5-a5ef-2f3ddab84614
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5471720cbd3084c661dec93d9c7f4f680e066b86
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66070400"
---
# <a name="relabel-sql-server-data-mining-add-ins"></a>Cambiar etiquetas (Complementos de minería de datos de SQL Server)
  ![Icono de Office 13 para la herramienta Relabel](media/dm13-relabel.gif "Icono de Office 13 para la herramienta Relabel")  
  
 El Cliente de minería de datos para Excel le permite crear nuevas etiquetas para los datos con el fin de simplificar la comprensión de los resultados del análisis.  
  
 Algunos motivos para cambiar las etiquetas son:  
  
-   Los datos incluyen los resultados que se codificaron, como 1 para Hombre y 2 para Mujer.  
  
-   Va a crear depósitos con los valores numéricos y desea proporcionar a los intervalos un nombre descriptivo.  
  
-   Desea simplificar los nombres largos.  
  
## <a name="using-the-relabel-wizard"></a>Usar el Asistente para cambiar etiquetas  
  
1.  En la cinta de opciones **minería de datos** , haga clic en **limpiar** y seleccione **cambiar etiqueta**.  
  
2.  Seleccione la tabla o el intervalo de datos que tenga los datos que desee corregir.  
  
3.  En la página **cambiar etiqueta** del asistente, seleccione una sola columna; para ello, elija la columna en la lista desplegable o haga clic en la columna en el panel **muestras de datos** .  
  
     En el panel de **ejemplos de datos** solo se muestran aproximadamente 50 filas de datos, pero se muestrean para asegurarse de que ve una buena distribución de valores.  
  
     Haga clic en el encabezado de columna de **recuento** para ordenar por el recuento de cada valor.  
  
     También puede ordenar por **etiquetas originales**, lo que resulta útil si desea volver a etiquetar primero todos los valores más altos o más bajos.  
  
4.  En la página **cambiar etiquetas** de datos del asistente, revise los valores de la columna **etiquetas originales** y decida cómo desea agruparlos o editarlos.  
  
5.  Escriba un nuevo valor en la fila bajo **etiquetas nuevas**. También puede elegir un valor de la lista de valores existentes. A medida que escribe nuevos valores, estos están disponibles inmediatamente para su reutilización.  
  
6.  Cuando haya especificado suficientes filas, haga clic en **siguiente**y, en la página **Seleccionar destino** , elija dónde guardará los datos cambiados de etiqueta.  
  
    -   **Agregar a la hoja de cálculo actual como una nueva columna**  
  
         Haga clic en esta opción para agregar una columna nueva a la tabla que contiene los valores nuevos.  
  
    -   **Copiar datos de hoja con cambios a una nueva hoja de cálculo**  
  
         Haga clic en esta opción para crear una hoja de cálculo nueva que contenga los datos actualizados.  
  
    -   **Cambiar datos en su lugar**  
  
         Haga clic en esta opción para sustituir los datos originales por los valores nuevos.  
  
## <a name="see-also"></a>Consulte también  
 [Explorar y limpiar datos](exploring-and-cleaning-data.md)  
  
  

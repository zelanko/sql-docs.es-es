---
title: Cambiar etiquetas (datos de SQL Server a los complementos de minería de datos) | Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070400"
---
# <a name="relabel-sql-server-data-mining-add-ins"></a>Cambiar etiquetas (Complementos de minería de datos de SQL Server)
  ![Icono de Office 13 para la herramienta Relabel](media/dm13-relabel.gif "icono de Office 13 para la herramienta Relabel")  
  
 El Cliente de minería de datos para Excel le permite crear nuevas etiquetas para los datos con el fin de simplificar la comprensión de los resultados del análisis.  
  
 Algunos motivos para cambiar las etiquetas son:  
  
-   Los datos incluyen los resultados que se codificaron, como 1 para Hombre y 2 para Mujer.  
  
-   Va a crear depósitos con los valores numéricos y desea proporcionar a los intervalos un nombre descriptivo.  
  
-   Desea simplificar los nombres largos.  
  
## <a name="using-the-relabel-wizard"></a>Usar el Asistente para cambiar etiquetas  
  
1.  En el **minería de datos** la cinta de opciones, haga clic en **Clean** y, a continuación, seleccione **cambiar etiquetas**.  
  
2.  Seleccione la tabla o el intervalo de datos que tenga los datos que desee corregir.  
  
3.  En el **cambiar etiquetas** página del asistente, seleccione una sola columna, seleccionando la columna en la lista desplegable o haciendo clic en la columna en la **muestras de datos** panel.  
  
     El **muestras de datos** panel solo muestra aproximadamente 50 filas de datos, pero están muestreadas para asegurarse de que ve una amplia representación de valores.  
  
     Haga clic en el encabezado de columna para **recuento** para ordenar por recuento de cada valor.  
  
     También puede ordenar por **etiquetas originales**, que es útil si desea cambiar etiquetas de primero todos los valores mayores o menores.  
  
4.  En el **cambiar etiquetas** página de datos del asistente, revise los valores de la **etiquetas originales** columna y decidir cómo desea agruparlos o modificarlos.  
  
5.  Escriba un nuevo valor en la fila bajo **nuevas etiquetas**. También puede elegir un valor de la lista de valores existentes. A medida que escribe nuevos valores, estos están disponibles inmediatamente para su reutilización.  
  
6.  Cuando haya especificado suficientes filas, haga clic en **siguiente**y en el **Seleccionar destino** página, elija dónde guardará los datos con.  
  
    -   **Agregar como una nueva columna a la hoja de cálculo actual**  
  
         Haga clic en esta opción para agregar una columna nueva a la tabla que contiene los valores nuevos.  
  
    -   **Copiar datos de la hoja con cambios en una nueva hoja de cálculo**  
  
         Haga clic en esta opción para crear una hoja de cálculo nueva que contenga los datos actualizados.  
  
    -   **Cambiar los datos en su lugar**  
  
         Haga clic en esta opción para sustituir los datos originales por los valores nuevos.  
  
## <a name="see-also"></a>Vea también  
 [Exploración y limpieza de datos](exploring-and-cleaning-data.md)  
  
  

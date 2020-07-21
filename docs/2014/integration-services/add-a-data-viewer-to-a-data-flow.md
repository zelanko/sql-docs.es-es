---
title: Agregar un visor de datos a un flujo de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data viewers [Integration Services]
- data flow [Integration Services], data viewers
- adding data viewers
ms.assetid: 5e573274-a170-4132-bfc8-a8ff3a8411e4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e04e678dfb2b98e5304f9f7c9f0cfe2a858b6485
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439772"
---
# <a name="add-a-data-viewer-to-a-data-flow"></a>agregar un visor de datos a un flujo de datos
  En este tema se describe cómo agregar y configurar un visor de datos en un flujo de datos. Un visor de datos muestra los datos que se mueven entre dos componentes de flujo de datos. Por ejemplo, un visor de datos puede mostrar los datos que se extraen de un origen de datos antes de que una transformación en el flujo de datos los modifique.  
  
 Una ruta de acceso conecta componentes de un flujo de datos conectando la salida de un componente de flujo de datos con la entrada de otro componente.  
  
 Para poder agregar visores de datos a un paquete, éste debe incluir una tarea Flujo de datos y al menos dos componentes de flujo de datos conectados.  
  
### <a name="to-add-a-data-viewer-to-a-data-flow"></a>Para agregar un visor de datos a un flujo de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** , si aún no está activo.  
  
4.  Haga clic en la tarea Flujo de datos que contiene el flujo de datos al que desee adjuntar un visor de datos y, a continuación, haga clic en la pestaña **Flujo de datos** .  
  
5.  Haga clic con el botón derecho en una ruta entre dos componentes de flujo de datos y, después, haga clic en **Editar**.  
  
6.  En la página **General** puede ver y editar propiedades de ruta. Por ejemplo, en la lista desplegable **PathAnnotation** puede seleccionar la anotación que aparece junto a la ruta de acceso.  
  
7.  En la página **Metadatos** puede ver los metadatos de columna y copiar los metadatos al Portapapeles.  
  
8.  En la página **Visor de datos** , haga clic en **Habilitar visor de datos**.  
  
9. En el área Columnas que se mostrarán, seleccione las columnas que desee mostrar en el visor de datos. De forma predeterminada, todas las columnas disponibles aparecen seleccionadas y en la lista **Columnas mostradas** . Mueva las columnas que no desee utilizar a la lista **Columnas sin usar** , seleccionándolas y haciendo clic en la flecha hacia la izquierda.  
  
    > [!NOTE]  
    >  En la cuadrícula, los valores que representan los tipos de datos DT_DATE, DT_DBTIME2, DT_FILETIME, DT_DBTIMESTAMP, DT_DBTIMESTAMP2 y DT_DBTIMESTAMPOFFSET aparecen como cadenas con formato ISO 8601 y un espacio separador reemplaza el separador `T`. Los valores que representan los tipos de datos DT_DATE y DT_FILETIME incluyen siete dígitos para las fracciones de segundo. Dado que el tipo de datos DT_FILETIME almacena solamente tres dígitos de fracciones de segundo, la cuadrícula muestra ceros para los cuatro dígitos restantes. Los valores que representan el tipo de datos DT_DBTIMESTAMP incluyen tres dígitos para las fracciones de segundo. Para los valores que representan los tipos de datos DT_DBTIME2, DT_DBTIMESTAMP2 y DT_DBTIMESTAMPOFFSET, el número de dígitos de las fracciones de segundo corresponde a la escala especificada para el tipo de datos de la columna. Para obtener más información acerca de los formatos ISO 8601, vea [Date and Time Formats](../../2014/integration-services/date-and-time-formats.md). Para obtener más información sobre los tipos de datos, vea [Integration Services tipos de datos](data-flow/integration-services-data-types.md).  
  
10. Haga clic en **OK**.  
  
## <a name="see-also"></a>Consulte también  
 [Integration Services transformaciones](data-flow/transformations/integration-services-transformations.md)   
 [Integration Services trazados](data-flow/integration-services-paths.md)   
 [Flujo de datos](data-flow/data-flow.md)   
 [Depurar el flujo de datos](troubleshooting/debugging-data-flow.md)  
  
  

---
title: 'Paso 5: Agregar y configurar el origen de archivo plano | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5c95ce51-e0fe-4fc5-95eb-2945929f2b13
caps.latest.revision: 20
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: a48d451248e28f8c9e0fd623c96022f558b80ca8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112724"
---
# <a name="step-5-adding-and-configuring-the-flat-file-source"></a>Paso 5: Agregar y configurar el origen de archivo plano
  En esta tarea, agregará un origen de archivo plano al paquete y configurará dicho origen. Un origen de archivo plano es un componente de flujo de datos que utiliza metadatos definidos por un administrador de conexiones de archivo plano para especificar el formato y la estructura de los datos que deben extraerse del archivo plano mediante un proceso de transformación. El origen de archivo plano puede configurarse para extraer datos de un único archivo plano utilizando la definición de formato de archivo proporcionada por el administrador de conexiones de archivo plano.  
  
 Para este tutorial, configurará el origen de archivo sin formato para utilizar el `Sample Flat File Source Data` Administrador de conexiones que creó anteriormente.  
  
### <a name="to-add-a-flat-file-source-component"></a>Para agregar un componente de origen de archivo plano  
  
1.  Abra la **flujo de datos** diseñador haciendo doble clic en el `Extract Sample Currency Data` tarea flujo de datos o haciendo clic en el **pestaña flujo de datos**.  
  
2.  En el **cuadro de herramientas de SSIS**, expanda **Otros orígenes**y, después, arrastre un **Origen de archivo plano** a la superficie de diseño de la pestaña **Flujo de datos** .  
  
3.  En el **de flujo de datos** superficie de diseño, haga clic en el recién agregado **origen de archivo plano**, haga clic en **cambiar el nombre de**y cambie el nombre a `Extract Sample Currency Data`.  
  
4.  Haga doble clic en el origen del archivo plano para abrir el cuadro de diálogo Editor de origen de archivos planos.  
  
5.  En el **Administrador de conexiones de archivos planos** cuadro, seleccione `Sample Flat File Source Data`.  
  
6.  Haga clic en **Columnas** y compruebe que los nombres de las columnas son correctos.  
  
7.  Haga clic en **Aceptar**.  
  
8.  Haga clic con el botón derecho en el origen del archivo plano y haga clic en **Propiedades**.  
  
9. En la ventana Propiedades, compruebe que la `LocaleID` propiedad está establecida en **inglés (Estados Unidos)**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Paso 6: Agregar y configurar transformaciones de búsqueda](lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
## <a name="see-also"></a>Vea también  
 [Origen de archivo plano](data-flow/flat-file-source.md)   
 [Editor del administrador de conexiones de archivos planos &#40;página General&#41;](general-page-of-integration-services-designers-options.md)  
  
  
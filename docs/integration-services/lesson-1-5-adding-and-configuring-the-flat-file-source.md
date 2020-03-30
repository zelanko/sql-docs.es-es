---
title: 'Paso 5: Adición y configuración del origen de archivo plano | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5c95ce51-e0fe-4fc5-95eb-2945929f2b13
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e95b86d2d29bb3883f6fd76db29f17e5936d1b53
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "71283690"
---
# <a name="lesson-1-5-add-and-configure-the-flat-file-source"></a>Lección 1-5: Adición y configuración del origen de archivo plano

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


En esta tarea, agregará un origen de archivo plano al paquete y lo configurará. Un origen de archivo plano es un componente de flujo de datos que usa los metadatos definidos por un administrador de conexiones de archivos planos. Estos metadatos especifican el formato y la estructura de los datos que se van a extraer del archivo plano mediante un proceso de transformación. El origen de archivo plano extrae los datos de un único archivo plano, mediante las definiciones de formato de archivo del administrador de conexiones de archivo plano.  
  
Para esta tarea, configurará el origen de archivo plano para que use el administrador de conexiones **Sample Flat File Source Data** creado antes.  
  
## <a name="add-a-flat-file-source-component"></a>Adición de un componente de origen de archivo plano  
  
1.  Para abrir el diseñador **Flujo de datos**, haga doble clic en la tarea de flujo de datos **Extract Sample Currency Data**, o bien haga clic en la pestaña **Flujo de datos**.  
  
2.  En el **cuadro de herramientas de SSIS**, expanda **Otros orígenes**y, después, arrastre un **Origen de archivo plano** a la superficie de diseño de la pestaña **Flujo de datos** .  
  
3.  En la superficie de diseño **Flujo de datos**, haga clic con el botón derecho en el **Origen de archivo plano** recién agredo, haga clic en **Cambiar nombre** y cambie el nombre por **Extract Sample Currency Data**.  
  
4.  Haga doble clic en el origen del archivo plano para abrir el cuadro de diálogo **Editor de origen de archivos planos**.  
  
5.  En el campo **Administrador de conexiones de archivos planos**, seleccione **Sample Flat File Source Data**.  
  
6.  Haga clic en **Columnas** y compruebe que los nombres de las columnas son correctos.  
  
7.  Seleccione **Aceptar**.  
  
8.  Haga clic con el botón derecho en el origen del archivo plano y seleccione **Propiedades**.  
  
9. En la ventana **Propiedades**, compruebe que la propiedad **LocaleID** esté establecida en **Inglés (Estados Unidos)** .  
  
## <a name="go-to-next-task"></a>Ir a la tarea siguiente
[Paso 6: Adición y configuración de las transformaciones Lookup](../integration-services/lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
## <a name="see-also"></a>Consulte también  
[Origen de archivo plano](../integration-services/data-flow/flat-file-source.md)  
[Administrador de conexiones de archivos planos](../integration-services/connection-manager/flat-file-connection-manager.md)  
  
  
  

---
title: 'Paso 8: Anotación y formato del paquete de la lección 1 | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: e3751e53-77c7-47d0-8fe8-73ed1a53413a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3a67d7593ca63a2271fc94fc7203e9bb55d6efcc
ms.sourcegitcommit: 445842da7c7d216b94a9576e382164c67f54e19a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/30/2019
ms.locfileid: "71680977"
---
# <a name="lesson-1-8-annotate-and-format-the-lesson-1-package"></a>Lección 1-8: Anotación y formato del paquete de la lección 1 

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Ahora que ha terminado la configuración del paquete de la lección 1, probablemente sea el momento de ordenar el diseño del paquete. Si las formas en los diseños de flujo de datos y control tienen tamaños diferentes o bien no se distribuyen de manera uniforme, es posible que sea más difícil entender el paquete.  
  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools proporciona herramientas para aplicar formato fácilmente al diseño del paquete. Las características de formato incluyen la capacidad de hacer que las formas tengan el mismo tamaño, de alinearlas y de cambiar el espaciado horizontal y vertical entre las formas.  
  
Otra forma de mejorar la comprensión de la funcionalidad de un paquete es agregar anotaciones que la describan.  
  
En esta tarea, se usan las características de formato de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools para mejorar el diseño del flujo de datos y también se agrega una anotación.  
  
## <a name="format-the-layout-of-the-data-flow"></a>Formato del diseño del flujo de datos  
  
1.  Si el paquete de la lección 1 todavía no está abierto, haga doble clic en **Lesson 1.dtsx** en el **Explorador de soluciones**.  
  
2.  Haga clic en la pestaña **Flujo de datos**.  
  
3.  Para seleccionar todos los componentes de flujo de datos a la vez, use **Editar** > **Seleccionar todo**.
  
4.  En el menú **Formato**, seleccione **Igualar tamaño** y después haga clic en **Ambos**.  
  
5.  Con los objetos del flujo de datos seleccionados, en el menú **Formato**, seleccione **Alinear** y haga clic en **Centros**.  

6.  Con los objetos del flujo de datos seleccionados, en el menú **Formato**, seleccione **Espaciado vertical** y haga clic en **Igualar**.  
  
## <a name="add-an-annotation-to-the-data-flow"></a>Adición de una anotación al flujo de datos  
  
1.  Haga clic con el botón derecho en cualquier parte de la superficie de diseño del flujo de datos y después seleccione **Agregar anotación**.  
  
2.  Escriba o pegue el texto siguiente en el cuadro de anotación.  
  
        The data flow extracts data from a file, looks up values in the CurrencyKey column in the DimCurrency table and the DateKey column in the DimDate table, and writes the data to the NewFactCurrencyRate table.
  
    Para ajustar el texto en el cuadro de anotación, coloque el cursor donde quiera empezar una nueva línea y presione **Intro**.  
  
    Si no agrega texto al cuadro de anotación, desaparecerá al hacer clic fuera del cuadro.  Debido a este comportamiento, si quiere pegar texto en el cuadro de anotación, cópielo al Portapapeles antes de seleccionar Agregar anotación. 
  
## <a name="go-to-next-task"></a>Ir a la tarea siguiente
[Paso 9: Prueba del paquete de la lección 1](../integration-services/lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
  
  

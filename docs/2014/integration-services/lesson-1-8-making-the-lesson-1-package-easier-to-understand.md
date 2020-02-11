---
title: 'Paso 8: Facilitar la comprensión del paquete de la lección 1 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e3751e53-77c7-47d0-8fe8-73ed1a53413a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 390fb10287ff88ec5f7a0220dea6dd677e8e36cd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62767597"
---
# <a name="step-8-making-the-lesson-1-package-easier-to-understand"></a>Paso 8: Facilitar la comprensión del paquete de la lección 1
  Ahora que ha terminado la configuración del paquete de la lección 1, es una buena idea ordenar el diseño del paquete. Si las formas de los diseños de los flujos de datos y de control tienen tamaños aleatorios o no están alineadas o agrupadas, la funcionalidad del paquete puede resultar más difícil de comprender.  
  
 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools proporciona herramientas que permiten aplicar formato al diseño del paquete de forma rápida y sencilla. Las características de formato incluyen la capacidad de hacer que las formas tengan el mismo tamaño, de alinearlas y de manipular el espaciado horizontal y vertical entre las formas.  
  
 Otra forma de mejorar la comprensión de la funcionalidad de un paquete es agregar anotaciones que la describan.  
  
 En esta tarea usará las características de formato de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools para mejorar el diseño del flujo de datos y agregará una anotación al flujo de datos.  
  
### <a name="to-format-the-layout-of-the-data-flow"></a>Para aplicar formato al diseño del flujo de datos  
  
1.  Si el paquete de la lección 1 no está abierto todavía, haga doble clic en Lesson 1.dtsx en el Explorador de soluciones.  
  
2.  Haga clic en la pestaña **Flujo de datos** .  
  
3.  Coloque el cursor en la parte superior derecha de la transformación Extract Sample Currency, haga clic y, a continuación, arrastre el cursor por todos los componentes de flujo de datos.  
  
4.  En el menú **Formato** , seleccione **Igualar tamaño**y, a continuación, haga clic en **Ambos**.  
  
5.  Con los objetos del flujo de datos seleccionados, en el menú **Formato** , seleccione **Alinear**y haga clic en **Lados izquierdos**.  
  
### <a name="to-add-an-annotation-to-the-data-flow"></a>Para agregar una anotación al flujo de datos  
  
1.  Haga clic con el botón derecho en cualquier parte de la superficie de diseño del flujo de datos y haga clic en **Agregar anotación**.  
  
2.  Escriba o pegue el texto siguiente en el cuadro de anotación.  
  
     **El flujo de datos extrae datos de un archivo, busca valores en la columna CurrencyKey de la tabla DimCurrency y la columna DateKey de la tabla DimDate, y escribe los datos en la tabla NewFactCurrencyRate.**  
  
     Para ajustar el texto en el cuadro de anotación, coloque el cursor donde desee empezar una nueva línea y presione la tecla Intro.  
  
     Si no agrega texto al cuadro de anotación, desaparecerá al hacer clic fuera del cuadro.  
  
## <a name="next-steps"></a>Pasos siguientes  
 [Paso 9: Probar el paquete del tutorial de la lección 1](../integration-services/lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
  

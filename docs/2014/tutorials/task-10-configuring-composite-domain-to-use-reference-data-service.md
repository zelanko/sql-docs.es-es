---
title: 'Tarea 10: Configurar un dominio compuesto para usar el servicio de datos de referencia | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 752eefde-8b87-4f54-878e-9963ccbadc8e
caps.latest.revision: 8
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5abc5bc02b2c7ee365886ba54a603890c4b2aa0f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37228355"
---
# <a name="task-10-configuring-composite-domain-to-use-reference-data-service"></a>Tarea 10: configurar un dominio compuesto para que use un servicio de datos de referencia
  En esta tarea, configurará la **validación de direcciones** un dominio compuesto a usar el **Melissa Data – Address Check** service. En tiempo de ejecución, durante la actividad de limpieza, DQS pasa los valores de dominios del dominio Validación de direcciones al servicio para su limpieza. Consulte [mapa de dominio o un dominio compuesto a datos de referencia](http://msdn.microsoft.com/library/hh213030.aspx) para obtener más detalles.  
  
1.  En la página principal de **cliente DQS**, haga clic en **proveedores (administración de dominios)** en **base de conocimiento reciente** para iniciar el **Domain Management**página.  
  
2.  Seleccione el **validación de direcciones** dominio compuesto en el **lista de dominios**.  
  
3.  En el panel derecho, cambie a la **datos de referencia** ficha.  
  
     ![Pestaña datos de referencia](../../2014/tutorials/media/et-configuringcdtouserds-01.jpg "pestaña datos de referencia")  
  
4.  Haga clic en **examinar** en la barra de herramientas.  
  
5.  En el **catálogo de proveedores de datos de referencia en línea** cuadro de diálogo, seleccione **casilla** junto a **Melissa Data – Address Check**.  
  
     ![Seleccionar Melissa Data - Address Check](../../2014/tutorials/media/et-configuringcdtouserds-02.jpg "seleccionar Melissa Data - Address Check")  
  
6.  En el panel derecho, en el **esquema** sección, asigne **Address Line** dominio para el **Address Line (M)** elemento de esquema mediante el uso de la lista desplegable.  
  
     ![Asignación del elemento de esquema RDS a dominio](../../2014/tutorials/media/et-configuringcdtouserds-03.jpg "asignación del elemento de esquema RDS a dominio")  
  
7.  Haga clic en **Agregar entrada de esquema (+)** en la barra de herramientas para crear una entrada en la lista.  
  
     ![Agregar botón de barra de herramientas de entrada de esquema](../../2014/tutorials/media/et-configuringcdtouserds-04.jpg "Agregar botón de barra de herramientas de entrada de esquema")  
  
8.  Asigne los dominios siguientes de DQS mediante las listas desplegables según se muestra en la ilustración siguiente.  
  
     ![Asignar elementos de esquema RDS a dominios](../../2014/tutorials/media/et-configuringcdtouserds-05.jpg "asignar elementos de esquema RDS a dominios")  
  
9. Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 11: Publicar la base de conocimiento](../../2014/tutorials/task-11-publishing-the-knowledge-base.md)  
  
  

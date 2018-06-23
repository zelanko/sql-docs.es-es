---
title: 'Tarea 10: Configurar un dominio compuesto para usar el servicio de datos de referencia | Documentos de Microsoft'
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
ms.topic: article
ms.assetid: 752eefde-8b87-4f54-878e-9963ccbadc8e
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 2a5d37578ac8336b67201161ef4de59baf90649c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107771"
---
# <a name="task-10-configuring-composite-domain-to-use-reference-data-service"></a>Tarea 10: configurar un dominio compuesto para que use un servicio de datos de referencia
  En esta tarea, configurará la **validación de direcciones** dominio compuesto que se utiliza la **Melissa Data – Address Check** servicio. En tiempo de ejecución, durante la actividad de limpieza, DQS pasa los valores de dominios del dominio Validación de direcciones al servicio para su limpieza. Vea [mapa de dominio o un dominio compuesto a datos de referencia](http://msdn.microsoft.com/library/hh213030.aspx) para obtener más detalles.  
  
1.  En la página principal de **cliente DQS**, haga clic en **proveedores (administración de dominios)** en **base de conocimiento reciente** para iniciar el **Domain Management**página.  
  
2.  Seleccione el **validación de direcciones** dominio compuesto en la **lista de dominios**.  
  
3.  En el panel derecho, cambie a la **datos de referencia** ficha.  
  
     ![Hacer referencia a datos (pestaña)](../../2014/tutorials/media/et-configuringcdtouserds-01.jpg "hacen referencia a datos (pestaña)")  
  
4.  Haga clic en **examinar** botón en la barra de herramientas.  
  
5.  En el **catálogo de proveedores de datos de referencia en línea** cuadro de diálogo, seleccione **casilla de verificación** junto a **Melissa Data – Address Check**.  
  
     ![Seleccionar Melissa Data - Address Check](../../2014/tutorials/media/et-configuringcdtouserds-02.jpg "seleccionar Melissa Data - Address Check")  
  
6.  En el panel derecho, en la **esquema** sección, asigne **Address Line** dominio para la **Address Line (M)** elemento de esquema mediante la lista desplegable.  
  
     ![Asignar el elemento de esquema RDS a dominio](../../2014/tutorials/media/et-configuringcdtouserds-03.jpg "asignar elemento de esquema RDS a dominio")  
  
7.  Haga clic en **Agregar entrada de esquema (+)** botón en la barra de herramientas para crear una entrada en la lista.  
  
     ![Agregar botón de barra de herramientas de entrada de esquema](../../2014/tutorials/media/et-configuringcdtouserds-04.jpg "Agregar botón de barra de herramientas de entrada de esquema")  
  
8.  Asigne los dominios siguientes de DQS mediante las listas desplegables según se muestra en la ilustración siguiente.  
  
     ![Asignar elementos de esquema RDS a dominios](../../2014/tutorials/media/et-configuringcdtouserds-05.jpg "asignar elementos de esquema RDS a dominios")  
  
9. Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 11: Publicar la Base de conocimiento](../../2014/tutorials/task-11-publishing-the-knowledge-base.md)  
  
  
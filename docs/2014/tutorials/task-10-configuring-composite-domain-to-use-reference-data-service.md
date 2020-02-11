---
title: 'Tarea 10: configuración de un dominio compuesto para usar el servicio de datos de referencia | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 752eefde-8b87-4f54-878e-9963ccbadc8e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 525e0286d8d82f501981c9e936caca581886b9b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65481237"
---
# <a name="task-10-configuring-composite-domain-to-use-reference-data-service"></a>Tarea 10: configurar un dominio compuesto para que use un servicio de datos de referencia
  En esta tarea, configurará el dominio compuesto **validación de direcciones** para que use el servicio **Melissa Data-Address check** . En tiempo de ejecución, durante la actividad de limpieza, DQS pasa los valores de dominios del dominio Validación de direcciones al servicio para su limpieza. Para obtener más información [, vea asignar dominio o compuesto de dominio a datos de referencia](https://msdn.microsoft.com/library/hh213030.aspx) .  
  
1.  En la Página principal del **cliente DQS**, haga clic en **proveedores (administración de dominios)** en **bases de conocimiento recientes** para iniciar la página **Administración de dominios** .  
  
2.  Seleccione el dominio compuesto **validación de direcciones** en la **lista de dominios**.  
  
3.  En el panel derecho, cambie a la pestaña **datos de referencia** .  
  
     ![Pestaña de datos de referencia](../../2014/tutorials/media/et-configuringcdtouserds-01.jpg "Pestaña de datos de referencia")  
  
4.  Haga clic en el botón **examinar** de la barra de herramientas.  
  
5.  En el cuadro de diálogo **Catálogo de proveedores de datos de referencia en línea** **, active la casilla situada** junto a **Melissa Data-Address check**.  
  
     ![Seleccionar Melissa Data - Address Check](../../2014/tutorials/media/et-configuringcdtouserds-02.jpg "Seleccionar Melissa Data - Address Check")  
  
6.  En el panel derecho, en la sección **esquema** , asigne dominio de **línea de dirección** al elemento de esquema de línea de **dirección (M)** mediante la lista desplegable.  
  
     ![Asignar elemento de esquema RDS a dominio](../../2014/tutorials/media/et-configuringcdtouserds-03.jpg "Asignar elemento de esquema RDS a dominio")  
  
7.  Haga clic en el botón **Agregar entrada de esquema (+)** de la barra de herramientas para crear una entrada en la lista.  
  
     ![Botón de barra de herramientas Agregar entrada de esquema](../../2014/tutorials/media/et-configuringcdtouserds-04.jpg "Botón de barra de herramientas Agregar entrada de esquema")  
  
8.  Asigne los dominios siguientes de DQS mediante las listas desplegables según se muestra en la ilustración siguiente.  
  
     ![Asignar elementos de esquema RDS a dominios](../../2014/tutorials/media/et-configuringcdtouserds-05.jpg "Asignar elementos de esquema RDS a dominios")  
  
9. Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 11: publicar la base de conocimiento](../../2014/tutorials/task-11-publishing-the-knowledge-base.md)  
  
  

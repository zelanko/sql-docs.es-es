---
description: 'Lección 2-3: Modificación del Administrador de conexiones de archivos planos'
title: 'Paso 3: Modificación del Administrador de conexiones de archivos planos | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 459e3995-2116-4f15-aaa2-32f26113869c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bbe7698c4b97a11fd9b2b4dba581fbad5a8be8df
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/26/2020
ms.locfileid: "88484115"
---
# <a name="lesson-2-3-modify-the-flat-file-connection-manager"></a>Lección 2-3: Modificación del Administrador de conexiones de archivos planos

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]

En esta tarea, modificará el Administrador de conexiones de archivos planos de la lección 1. El administrador de conexiones de archivos planos se ha configurado para cargar un único archivo de forma estática. Para permitir que el Administrador de conexiones de archivos planos cargue archivos de forma iterativa, modifique la propiedad ConnectionString del administrador de conexiones de modo que use la variable `User::varFileName`, definida por el usuario, que contiene la ruta de acceso del archivo que se va a cargar en tiempo de ejecución.  
  
Al modificar el administrador de conexiones para que use el valor de la variable definida por el usuario para cambiar la propiedad ConnectionString, el administrador de conexiones se conecta a otros archivos planos. En tiempo de ejecución, cada iteración del contenedor de bucles Foreach actualiza de forma dinámica la variable `User::varFileName`. A su vez, actualizar esta variable da lugar a que el administrador de conexiones se conecte a un archivo plano distinto, y que la tarea de flujo de datos procese un conjunto de datos distinto.  
  
## <a name="configure-the-flat-file-connection-manager-to-use-a-variable"></a>Configuración del Administrador de conexiones de archivos planos para usar una variable  
  
1.  En el panel **Administradores de conexión** , haga clic con el botón derecho en **Sample Flat File Source Data** y, después, seleccione **Propiedades**.  

2.  En la ventana **Propiedades**, asegúrese de que **PackagePath** comienza con **\Package.Connections**. Si no, en el panel **Administradores de conexión**, haga clic con el botón derecho en **Sample Flat File Source Data** (Datos de origen de archivos planos de ejemplo) y seleccione **Convertir en conexión de paquete**.
  
3.  En la ventana **Propiedades**, para **Expresiones**, seleccione la celda vacía y, después, haga clic en el botón de puntos suspensivos **(...)**.  
  
4.  En el cuadro de diálogo **Editor de expresiones de propiedad**, en la columna **Propiedad**, seleccione **ConnectionString**.  
  
5.  En la columna **Expresión**, haga clic en el botón de puntos suspensivos **(…)** para abrir el cuadro de diálogo **Generador de expresiones**.  
  
6.  En el cuadro de diálogo **Generador de expresiones**, expanda el nodo **Variables**.  
  
7.  Arrastre la variable **User::varFileName** hasta el cuadro **Expresión**.  
  
8.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Generador de expresiones**.  
  
9.  Haga clic en **Aceptar** de nuevo para cerrar el cuadro de diálogo **Editor de expresiones de propiedad**.  
  
## <a name="go-to-next-task"></a>Ir a la tarea siguiente  
[Paso 4: Prueba del paquete del tutorial de la lección 2](../integration-services/lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
  
  

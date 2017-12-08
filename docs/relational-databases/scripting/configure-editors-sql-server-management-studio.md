---
title: Configurar editores (SQL Server Management Studio) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: ssms
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e7c7a8ef-f561-4258-a7b6-c445dba69f87
caps.latest.revision: "6"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1a6b2127ade3299cab4ae71a42f9601c4742f9d6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="configure-editors-sql-server-management-studio"></a>Configurar editores (SQL Server Management Studio)
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] El funcionamiento de los editores de [!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] puede personalizarse configurando las opciones de cada editor.  
  
## <a name="settng-editor-options"></a>Configurar las opciones del editor  
 La mayoría de las opciones del editor se establecen a través del menú **Herramientas** , donde se selecciona **Opciones…** para mostrar un cuadro de diálogo **Opciones** . En el cuadro de diálogo **Opciones** , abra el nodo de **Editor de texto** en el panel izquierdo para configurar las opciones de edición de texto y código. Los nodos situados bajo Editor de texto se corresponden con editores concretos:  
  
1.  **Todos los lenguajes** : las opciones que se establecen a través de este nodo se aplican a todos los editores de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] . Puede invalidar estos valores estableciendo opciones distintas para un editor concreto en los demás nodos.  
  
2.  **Texto sin formato** : las opciones que se establecen a través de este nodo se aplican a editores MDX, DMX y de texto.  
  
3.  **Transact-SQL:** las opciones que se establecen a través de este nodo se aplican al editor de consultas del motor de base de datos.  
  
4.  **XML** : las opciones que se establecen a través de este nodo se aplican al editor de XML for Analysis.  
  
 Abra los nodos **Ejecución de la consulta** o **Resultados de la consulta** para personalizar la ejecución de consultas y el modo en que se muestran los resultados.  
  
## <a name="editor-configuration-tasks"></a>Tareas de configuración del editor  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe cómo se especifica que un editor debe abrirse haciendo doble clic en un archivo con la extensión especificada en el Explorador de Windows.|[Asociar extensiones de archivo a un editor de código](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md)|  
|Describe cómo se personalizan las fuentes para mejorar la legibilidad del código y del texto.|[Cambiar el color, el tamaño y el estilo de la fuente](../../relational-databases/scripting/change-font-color-size-and-style.md)|  
|Describe cómo se consultan las propiedades.|[Utilizar la ventana Propiedades en Management Studio](../../relational-databases/scripting/use-the-properties-window-in-management-studio.md)|  
|Ubicación de las páginas de Ayuda F1 de los cuadros de diálogo de opciones de editores.|[Páginas de Opciones de consulta (Ayuda F1)](http://msdn.microsoft.com/library/fad98caa-8a29-4b88-8464-f60a5c4fc00e)|  
  
  

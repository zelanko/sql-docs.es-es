---
title: 'Tarea 7: Crear un dominio compuesto | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ae778647-1df0-4952-9a69-0ef6177eea9c
caps.latest.revision: 7
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e6f1ee787a51b8417ad3de37b74075df8782c722
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37153296"
---
# <a name="task-7-creating-a-composite-domain"></a>Tarea 7: crear una regla de dominio compuesto
  En esta tarea, creará un dominio compuesto, **validación de direcciones**, que consta de **Address Line**, **Ciudad**, **estado**y  **Código postal** dominios. Un dominio compuesto permite definir una regla entre dominios que afecta a varias dominios de una regla. Un dominio compuesto presenta otras ventajas como la posibilidad de analizar un valor de campo en varios dominios.  Por ejemplo, un valor de un campo Nombre completo se puede analizar en distintos dominios Nombre, Segundo nombre y Apellidos. En este tutorial, solo definirá una regla entre dominios. Consulte [administrar un dominio compuesto](http://msdn.microsoft.com/library/hh510399.aspx) para obtener más detalles.  
  
1.  En el panel izquierdo, haga clic en **crear un dominio compuesto** en la barra de herramientas.  
  
     ![Crear un botón de barra de herramientas del dominio compuesto](../../2014/tutorials/media/et-creatingacompositedomain-01.jpg "crear un botón de barra de herramientas del dominio compuesto")  
  
2.  Escriba **validación de direcciones** para el **nombre de dominio compuesto**.  
  
     ![Dominio compuesto validación de direcciones](../../2014/tutorials/media/et-creatingacompositedomain-02.jpg "dominio compuesto validación de direcciones")  
  
3.  En la lista de dominios seleccione **Address Line**, **Ciudad**, **estado**, y **Zip** y haga clic en **flecha derecha** para agregarlos a la **dominios del dominio compuesto** lista.  
  
4.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 8: Crear una regla de dominio compuesto](../../2014/tutorials/task-8-creating-a-composite-domain-rule.md)  
  
  

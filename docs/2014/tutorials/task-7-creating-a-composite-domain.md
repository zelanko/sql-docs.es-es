---
title: 'Tarea 7: Crear un dominio compuesto | Documentos de Microsoft'
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
ms.topic: article
ms.assetid: ae778647-1df0-4952-9a69-0ef6177eea9c
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e88fa44fb4457a979dfa1236531ed8bfa61f88fb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200834"
---
# <a name="task-7-creating-a-composite-domain"></a>Tarea 7: crear una regla de dominio compuesto
  En esta tarea, creará un dominio compuesto, **validación de direcciones**, formada por **Address Line**, **City**, **estado**y  **Código postal** dominios. Un dominio compuesto permite definir una regla entre dominios que afecta a varias dominios de una regla. Un dominio compuesto presenta otras ventajas como la posibilidad de analizar un valor de campo en varios dominios.  Por ejemplo, un valor de un campo Nombre completo se puede analizar en distintos dominios Nombre, Segundo nombre y Apellidos. En este tutorial, solo definirá una regla entre dominios. Vea [administrar un dominio compuesto](http://msdn.microsoft.com/library/hh510399.aspx) para obtener más detalles.  
  
1.  En el panel izquierdo, haga clic en **crear un dominio compuesto** botón en la barra de herramientas.  
  
     ![Crear un botón de barra de herramientas de dominio compuesto](../../2014/tutorials/media/et-creatingacompositedomain-01.jpg "crear un botón de barra de herramientas de dominio compuesto")  
  
2.  Escriba **validación de direcciones** para el **nombre de dominio compuesto**.  
  
     ![Dominio compuesto validación de direcciones](../../2014/tutorials/media/et-creatingacompositedomain-02.jpg "dominio compuesto validación de direcciones")  
  
3.  En la lista de dominios seleccione **Address Line**, **City**, **estado**, y **código postal** y haga clic en **flecha derecha** para agregarlos a la **dominios del dominio compuesto** lista.  
  
4.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 8: Crear una regla de dominio compuesto](../../2014/tutorials/task-8-creating-a-composite-domain-rule.md)  
  
  
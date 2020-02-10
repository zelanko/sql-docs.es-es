---
title: 'Tarea 7: crear un dominio compuesto | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ae778647-1df0-4952-9a69-0ef6177eea9c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: bbc00117e10e48adbde37b9f0561610feff8f87e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65488964"
---
# <a name="task-7-creating-a-composite-domain"></a>Tarea 7: crear una regla de dominio compuesto
  En esta tarea, creará un dominio compuesto, **la validación de direcciones**, que comprende los dominios de línea de **Dirección**, **ciudad**, **Estado**y **código postal** . Un dominio compuesto permite definir una regla entre dominios que afecta a varias dominios de una regla. Un dominio compuesto presenta otras ventajas como la posibilidad de analizar un valor de campo en varios dominios.  Por ejemplo, un valor de un campo Nombre completo se puede analizar en distintos dominios Nombre, Segundo nombre y Apellidos. En este tutorial, solo definirá una regla entre dominios. Vea [administrar un dominio compuesto](https://msdn.microsoft.com/library/hh510399.aspx) para obtener más detalles.  
  
1.  En el panel izquierdo, haga clic en el botón **crear un dominio compuesto** en la barra de herramientas.  
  
     ![Botón de barra de herramientas Crear un dominio compuesto](../../2014/tutorials/media/et-creatingacompositedomain-01.jpg "Botón de barra de herramientas Crear un dominio compuesto")  
  
2.  Escriba la **validación de direcciones** para el nombre de **dominio compuesto**.  
  
     ![Dominio compuesto de validación de direcciones](../../2014/tutorials/media/et-creatingacompositedomain-02.jpg "Dominio compuesto de validación de direcciones")  
  
3.  En la lista de dominios, seleccione **línea de dirección**, **ciudad**, **Estado**y **código postal** y haga clic en la **flecha derecha** para agregarlos a la lista **dominios en el dominio compuesto** .  
  
4.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 8: crear una regla de dominio compuesto](../../2014/tutorials/task-8-creating-a-composite-domain-rule.md)  
  
  

---
title: 'Tarea 8: crear una regla de dominio compuesto | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: cff3b662-7876-4445-9bdd-96be35b3ca0c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 7e40ec982a9b2c43c3d55ec60179ac9a0b80e8a1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489626"
---
# <a name="task-8-creating-a-composite-domain-rule"></a>Tarea 8: crear una regla de dominio compuesto
  En esta tarea, creará una regla para el dominio compuesto **validación de direcciones** . Defina una regla entre dominios: Si **City** es los **Ángeles**, el **Estado** debe ser **CA** , donde la **ciudad** y el **Estado** son dos dominios.  
  
1.  En el panel derecho, cambie a la pestaña **reglas de CD** .  
  
2.  Haga clic en **Agregar una nueva regla de dominio** en la barra de herramientas.  
  
3.  Escriba **City: regla de estado** para **nombre** y presione **entrar**.  
  
4.  En el panel **generar una regla** , seleccione **ciudad** en la lista de dominios y seleccione el valor de la condición **es igual a** y escriba los **Ángeles** para el valor.  
  
5.  En el panel **then** , seleccione **Estado** en la lista de dominios y seleccione el **valor es igual a**, escriba **CA** como valor y presione **Tab**.  
  
     ![Regla de dominio compuesto](../../2014/tutorials/media/et-creatingacompositedomainrule.jpg "Regla de dominio compuesto")  
  
6.  Haga clic en el botón **cerrar** situado en la parte inferior de la página para cambiar a la Página principal del cliente DQS. Publicará la base de conocimiento en la próxima lección. Observe que la base de conocimiento está en estado bloqueado (icono de candado).  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 9: configurar un servicio de datos de referencia](../../2014/tutorials/task-9-configuring-a-reference-data-service.md)  
  
  

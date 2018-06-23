---
title: 'Tarea 8: Crear una regla de dominio compuesto | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cff3b662-7876-4445-9bdd-96be35b3ca0c
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 18461e889e56f647b869d2b60cae49d662786160
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202633"
---
# <a name="task-8-creating-a-composite-domain-rule"></a>Tarea 8: crear una regla de dominio compuesto
  En esta tarea, crear una regla para la **validación de direcciones** dominio compuesto. Definir una regla entre dominios: si **City** es **Los Ángeles**, **estado** debe ser **CA** donde **City** y **estado** son dos dominios.  
  
1.  En el panel derecho, cambie a la **reglas de CD** ficha.  
  
2.  Haga clic en **agregar una nueva regla de dominio** desde la barra de herramientas.  
  
3.  Tipo de **regla ciudad-estado** para **nombre** y presione **ENTRAR**.  
  
4.  En el **una regla de generación** panel, seleccione **City** en la lista de dominios y seleccione la condición **es igual al valor** y tipo **Los Ángeles** para el valor.  
  
5.  En el **, a continuación,** panel, seleccione **estado** en la lista de dominios y seleccione **es igual al valor**, tipo **CA** del valor y presione **Ficha**.  
  
     ![Regla de dominio compuesto](../../2014/tutorials/media/et-creatingacompositedomainrule.jpg "regla de dominio compuesto")  
  
6.  Haga clic en **cerrar** situado en la parte inferior de la página para cambiar a la página principal del cliente DQS. Publicará la base de conocimiento en la próxima lección. Observe que la base de conocimiento está en estado bloqueado (icono de candado).  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 9: Configurar un servicio de datos de referencia](../../2014/tutorials/task-9-configuring-a-reference-data-service.md)  
  
  
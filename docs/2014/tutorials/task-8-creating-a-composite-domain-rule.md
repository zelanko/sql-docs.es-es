---
title: 'Tarea 8: Crear una regla de dominio compuesto | Microsoft Docs'
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
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65489626"
---
# <a name="task-8-creating-a-composite-domain-rule"></a>Tarea 8: Creación de una regla de dominio compuesto
  En esta tarea, creará una regla para el **validación de direcciones** dominio compuesto. Definir una regla entre dominios: si **Ciudad** es **Los Ángeles**, **estado** debe ser **CA** donde **Ciudad** y **estado** son dos dominios.  
  
1.  En el panel derecho, cambie a la **reglas de CD** ficha.  
  
2.  Haga clic en **agregar una nueva regla de dominio** desde la barra de herramientas.  
  
3.  Tipo **regla ciudad-estado** para **nombre** y presione **ENTRAR**.  
  
4.  En el **una regla de generación** panel, seleccione **Ciudad** en la lista de dominios y seleccione la condición **es igual al valor** y tipo **Los Ángeles** para el valor.  
  
5.  En el **, a continuación,** panel, seleccione **estado** en la lista de dominios y seleccione **es igual al valor**, tipo **CA** para el valor y presione **Ficha**.  
  
     ![Regla de dominio compuesto](../../2014/tutorials/media/et-creatingacompositedomainrule.jpg "regla de dominio compuesto")  
  
6.  Haga clic en **cerrar** situado en la parte inferior de la página para cambiar a la página principal del cliente DQS. Publicará la base de conocimiento en la próxima lección. Observe que la base de conocimiento está en estado bloqueado (icono de candado).  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 9: Configurar un servicio de datos de referencia](../../2014/tutorials/task-9-configuring-a-reference-data-service.md)  
  
  

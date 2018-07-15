---
title: 'Tarea 6: Establecer sinónimos | Microsoft Docs'
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
ms.topic: conceptual
ms.assetid: b7d35ee9-d1c9-41d9-bbc5-0ca7db93e54d
caps.latest.revision: 8
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 11be818da421f02ec07b13c632c4fcda87652442
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37323875"
---
# <a name="task-6-setting-synonyms"></a>Tarea 6: establecer sinónimos
  En esta tarea, establecerá dos valores de dominio, **USA** y **United States**, del dominio **País** como sinónimos, siendo **United States** el valor inicial. Como se seleccionó la opción **Usar valores iniciales** al crear el dominio **País** , todos los valores **USA** del dominio **País** se mostrarán como **United States** (ya que United States es el valor inicial). Vea el tema [Cambiar valores de dominio](http://msdn.microsoft.com/library/hh510408.aspx) para obtener más detalles.  
  
1.  Seleccione **País** en la lista de dominios.  
  
2.  Cambie a la pestaña **Valores del dominio** .  
  
3.  Haga clic en el botón **Agregar un nuevo valor de dominio** de la barra de herramientas.  
  
4.  Escriba **USA** como valor y presione **ENTRAR**.  
  
5.  Realice una selección múltiple de **United States** y **USA** mediante las teclas CTRL o MAYÚS, haga clic con el botón secundario en los elementos seleccionados y, a continuación, haga clic en **Establecer como sinónimos**. DQS agrupa estos valores y designa uno de ellos como el valor inicial por el que se reemplazan los demás valores.  
  
     ![Menú establecer como sinónimos](../../2014/tutorials/media/et-settingsynonyms-01.jpg "menú establecer como sinónimos")  
  
6.  Observe que **United States** se establece como valor inicial. Si desea que USA sea el valor inicial, puede hacer clic con el botón secundario en USA y seleccionar la opción **Establecer como principal** . En este tutorial, usamos **United States** como valor inicial.  
  
     ![Estados Unidos y EE. UU. como sinónimos](../../2014/tutorials/media/et-settingsynonyms-02.jpg "Estados Unidos y EE. UU. como sinónimos")  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 7: Crear una regla de dominio compuesto](../../2014/tutorials/task-7-creating-a-composite-domain.md)  
  
  

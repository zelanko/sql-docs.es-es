---
title: 'Paso 1: Configurar el proyecto de Visual Basic | Documentos de Microsoft'
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 77d3bfa5-fc9f-4a72-93b4-790c7d227988
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 22dc4636b248be498317edccfb89f13b235ab525
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="step-1-set-up-the-visual-basic-project"></a>Paso 1: Configurar el proyecto de Visual Basic
En este escenario, se supone que tiene Microsoft Visual Basic 6.0, ADO 2.5 o posterior y el proveedor Microsoft OLE DB para Internet Publishing instalados en el sistema. Se crea primero un nuevo proyecto y, a continuación, agregar algunos controles al formulario predeterminado en el proyecto.  
  
### <a name="to-create-an-ado-project"></a>Para crear un proyecto de ADO:  
  
1.  En Microsoft Visual Basic, cree un nuevo proyecto EXE estándar.  
  
2.  En el menú proyecto, elija referencias.  
  
3.  Seleccione "Biblioteca Microsoft ActiveX Data Objects 2.5" y haga clic en Aceptar.  
  
### <a name="to-insert-controls-on-the-main-form"></a>Para insertar controles en el formulario principal:  
  
1.  Agregue un control ListBox a Form1. Establezca su propiedad Name en **lstMain**.  
  
2.  Agregue otro control ListBox a Form1. Establezca su propiedad Name en **lstDetails**.  
  
3.  Agregue un control de cuadro de texto a Form1. Establezca su propiedad Name en **txtDetails**.  
  
## <a name="see-also"></a>Vea también  
 [Escenario de publicación en Internet](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Paso 2: Inicializar el cuadro de lista principal](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)

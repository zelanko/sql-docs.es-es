---
title: 'Paso 1: Configurar el proyecto de Visual Basic | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 77d3bfa5-fc9f-4a72-93b4-790c7d227988
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ce9e337a1ea45db851bafd32e0af476ae33fd3c0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47798803"
---
# <a name="step-1-set-up-the-visual-basic-project"></a>Paso 1: Configurar el proyecto de Visual Basic
En este escenario, se supone que tiene Microsoft Visual Basic 6.0, ADO 2.5 o posterior y el proveedor Microsoft OLE DB para la publicación en Internet instalada en el sistema. Se cree primero un nuevo proyecto y, a continuación, agregue algunos controles al formulario predeterminado en el proyecto.  
  
### <a name="to-create-an-ado-project"></a>Para crear un proyecto de ADO:  
  
1.  En Microsoft Visual Basic, cree un nuevo proyecto EXE estándar.  
  
2.  En el menú proyecto, elija referencias.  
  
3.  Seleccione "Biblioteca Microsoft ActiveX Data Objects 2.5" y haga clic en Aceptar.  
  
### <a name="to-insert-controls-on-the-main-form"></a>Insertar controles en el formulario principal:  
  
1.  Agregue un control ListBox a Form1. Establezca su propiedad Name en **lstMain**.  
  
2.  Agregue otro control ListBox a Form1. Establezca su propiedad Name en **lstDetails**.  
  
3.  Agregue un control TextBox a Form1. Establezca su propiedad Name en **txtDetails**.  
  
## <a name="see-also"></a>Vea también  
 [Escenario de publicación en Internet](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Paso 2: Inicializar el cuadro de lista principal](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)

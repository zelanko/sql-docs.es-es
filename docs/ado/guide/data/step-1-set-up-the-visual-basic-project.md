---
title: 'Paso 1: configurar el proyecto de Visual Basic | Microsoft Docs'
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
ms.openlocfilehash: bd44990c38a30f26e682fbb7f1f6aef642043215
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924071"
---
# <a name="step-1-set-up-the-visual-basic-project"></a>Paso 1: Configurar el proyecto de Visual Basic
En este escenario, se supone que tiene Microsoft Visual Basic 6,0, ADO 2,5 o posterior y el proveedor de Microsoft OLE DB para la publicación en Internet instalado en el sistema. Primero creará un nuevo proyecto y, a continuación, agregará algunos controles al formulario predeterminado en el proyecto.  
  
### <a name="to-create-an-ado-project"></a>Para crear un proyecto de ADO:  
  
1.  En Microsoft Visual Basic, cree un nuevo proyecto EXE estándar.  
  
2.  En el menú proyecto, elija referencias.  
  
3.  Seleccione "biblioteca de Microsoft Objetos de datos ActiveX 2,5" y haga clic en Aceptar.  
  
### <a name="to-insert-controls-on-the-main-form"></a>Para insertar controles en el formulario principal:  
  
1.  Agregue un control ListBox a Form1. Establezca su propiedad nombre en **lstMain**.  
  
2.  Agregue otro control ListBox a Form1. Establezca su propiedad nombre en **lstDetails**.  
  
3.  Agregue un control TextBox a Form1. Establezca su propiedad nombre en **txtDetails**.  
  
## <a name="see-also"></a>Consulte también  
 [Escenario de publicación en Internet](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Paso 2: Inicializar el cuadro de lista principal](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)

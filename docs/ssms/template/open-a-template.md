---
title: Abrir una plantilla | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- templates [Transact-SQL], opening
- opening templates
ms.assetid: 605b0f4c-5ba1-4249-ad1c-6341df77cd7a
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bfa128c7a1510b2f20eb9fa86d8a960aa4b13dd9
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="open-a-template"></a>Abrir una plantilla
Puede abrir una plantilla desde el Explorador de plantillas.  
  
## <a name="to-open-a-template-from-template-explorer"></a>Para abrir una plantilla desde el Explorador de plantillas  
Puede abrir plantillas desde el Explorador de plantillas.  
  
1.  Para abrir el Explorador de plantillas, en el menú **Ver** , haga clic en **Explorador de plantillas**.  
  
2.  En la lista de categorías de plantilla, expanda la categoría que contiene la plantilla que desea abrir.  
  
3.  Hay tres formas de abrir la plantilla:  
  
    1.  Haga doble clic en la plantilla para abrirla en una ventana del editor de código.  
  
    2.  Haga clic con el botón derecho en la plantilla y seleccione **Abrir** para abrirla en una ventana del editor de código.  
  
    3.  Arrastre la plantilla a una ventana del editor de código para agregar el código de plantilla al contenido de la ventana del editor.  
  
Una vez abierta la plantilla, use el cuadro de diálogo **Reemplazar parámetros de plantilla** para reemplazar los parámetros de la plantilla por sus valores.  
  
Si la apertura de una plantilla inicia una nueva ventana del editor, la ventana se abrirá con las credenciales de la conexión activa actual. Por ejemplo, si se centra en una instancia de [!INCLUDE[ssDE](../../includes/ssde_md.md)] en el Explorador de objetos al abrir la plantilla CREATE DATABASE, se abrirá una nueva ventana del editor mediante una conexión a dicha instancia. Si no hay ninguna conexión activa, [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] presentará un cuadro de diálogo de inicio de sesión.  
  
## <a name="see-also"></a>Vea también  
[Explorador de plantillas](../../ssms/template/template-explorer.md)  
[Reemplazar parámetros de plantilla](../../ssms/template/replace-template-parameters.md)  
  

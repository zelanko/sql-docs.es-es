---
description: Abrir una plantilla
title: Abrir una plantilla
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- templates [Transact-SQL], opening
- opening templates
ms.assetid: 605b0f4c-5ba1-4249-ad1c-6341df77cd7a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 730963488d34750ead61fe2662eb8201f91b30e1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417861"
---
# <a name="open-a-template"></a>Abrir una plantilla
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
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
  
Si la apertura de una plantilla inicia una nueva ventana del editor, la ventana se abrirá con las credenciales de la conexión activa actual. Por ejemplo, si se centra en una instancia de [!INCLUDE[ssDE](../../includes/ssde_md.md)] en el Explorador de objetos al abrir la plantilla CREATE DATABASE, se abrirá una nueva ventana del editor mediante una conexión a dicha instancia. Si no hay ninguna conexión activa, [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] presentará un cuadro de diálogo de inicio de sesión.  
  
## <a name="see-also"></a>Consulte también  
[Template Explorer](../../ssms/template/template-explorer.md)  
[Reemplazar parámetros de plantilla](../../ssms/template/replace-template-parameters.md)  
  

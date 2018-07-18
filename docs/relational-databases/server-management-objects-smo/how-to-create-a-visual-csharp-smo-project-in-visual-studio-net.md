---
title: Crear un proyecto de Visual C# SMO en Visual Studio .NET | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Visual C# [SMO]
ms.assetid: 1e7abb16-23a0-4a18-91ad-253261e6bf84
caps.latest.revision: 43
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 25e06aa3493b10e5a282fc5a709605eae18cb5fd
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37974195"
---
# <a name="how-to-create-a-visual-c-smo-project-in-visual-studio-net"></a>Cómo crear un proyecto de Visual C# SMO en Visual Studio .NET
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  En esta sección se describe cómo generar una aplicación de consola SMO simple.  
  
 En este ejemplo se importan espacios de nombres, lo que habilita al programa para que haga referencia a los tipos SMO. La importación de la **agente** espacio de nombres es opcional. Usarlo cuando se escribe un programa que usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente. El **común** espacio de nombres es necesario para establecer una conexión segura a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El **SqlClient** espacio de nombres se utiliza para procesar los errores de excepción de SQL.  
  
### <a name="creating-a-visual-c-smo-project-in-visual-studionet"></a>Crear un proyecto de Visual C# SMO en Visual Studio.NET  
  
1. Inicie Visual Studio
  
2. En el **archivo** menú, haga clic en **New** y, a continuación, **proyecto**.  Aparecerá el cuadro de diálogo **Nuevo proyecto** .   
  
3. En el [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **instalado** panel, vaya a **plantillas**\\**Visual C#**\\**Windows** y seleccione **aplicación de consola**.  
  
4. (Opcional) En el **nombre** texto, escriba el nombre de la nueva aplicación.  

5. Haga clic en **Aceptar** para cargar la plantilla de aplicación de consola.  

6. Siga las instrucciones de [instalar SMO](installing-smo.md) para instalar el paquete para el proyecto para hacer referencia a.
  
7. En el menú **Ver** , haga clic en **Código**.
    
8. En el código, antes de la instrucción de espacio de nombres, escriba lo siguiente **mediante** instrucciones para certificar los tipos del espacio de nombres de SMO:
  
    ```  
    using Microsoft.SqlServer.Management.Smo;  
    using Microsoft.SqlServer.Management.Common;  
    ```  
  
15. SMO cuenta con varios espacios de nombres bajo Microsoft.SqlServer.Management.Smo, como Microsoft.SqlServer.Management.Smo.Agent. Agregue los espacios de nombres que sean necesarios.  
  
16. Ahora puede agregar su código SMO.  
  
  

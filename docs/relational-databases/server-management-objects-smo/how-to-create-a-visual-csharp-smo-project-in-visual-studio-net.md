---
title: Crear un proyecto de Visual C# SMO en Visual Studio .NET | Documentos de Microsoft
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: Visual C# [SMO]
ms.assetid: 1e7abb16-23a0-4a18-91ad-253261e6bf84
caps.latest.revision: "43"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2fb8a8bd7527a14df4447fd4c7a49e92647b9e09
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="how-to-create-a-visual-c-smo-project-in-visual-studio-net"></a>Cómo crear un proyecto de Visual C# SMO en Visual Studio .NET
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Esta sección describe cómo crear una aplicación de consola SMO simple.  
  
 En este ejemplo se importan espacios de nombres, lo que habilita al programa para que haga referencia a los tipos SMO. La importación de la **agente** espacio de nombres es opcional. Utilícela cuando esté escribiendo un programa que usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente. El **común** espacio de nombres es necesaria para establecer una conexión segura a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El **SqlClient** espacio de nombres se utiliza para procesar los errores de excepción de SQL.  
  
### <a name="creating-a-visual-c-smo-project-in-visual-studionet"></a>Crear un proyecto de Visual C# SMO en Visual Studio.NET  
  
1. Inicie Visual Studio
  
2. En el **archivo** menú, haga clic en **New** y, a continuación, **proyecto**.  Aparecerá el cuadro de diálogo **Nuevo proyecto** .   
  
3. En el [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **instalado** panel, navegue hasta **plantillas**\\**Visual C#**\\**Windows** y seleccione **aplicación de consola**.  
  
4. (Opcional) En el **nombre** texto, escriba el nombre de la nueva aplicación.  

5. Haga clic en **Aceptar** para cargar la plantilla de aplicación de consola.  

6. Siga las instrucciones de [instalar SMO](installing-smo.md) para instalar el paquete para el proyecto de referencia.
  
7. En el menú **Ver** , haga clic en **Código**.
    
8. En el código, antes de la instrucción de espacio de nombres, escriba el siguiente **con** instrucciones para certificar los tipos en el espacio de nombres SMO:
  
    ```  
    using Microsoft.SqlServer.Management.Smo;  
    using Microsoft.SqlServer.Management.Common;  
    ```  
  
15. SMO cuenta con varios espacios de nombres bajo Microsoft.SqlServer.Management.Smo, como Microsoft.SqlServer.Management.Smo.Agent. Agregue los espacios de nombres que sean necesarios.  
  
16. Ahora puede agregar su código SMO.  
  
  

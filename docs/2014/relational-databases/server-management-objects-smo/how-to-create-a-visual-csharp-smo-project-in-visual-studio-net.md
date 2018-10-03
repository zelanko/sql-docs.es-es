---
title: Crear un proyecto de Visual C# SMO en Visual Studio .NET | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- Visual C# [SMO]
ms.assetid: 1e7abb16-23a0-4a18-91ad-253261e6bf84
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8abffe99e34df0aa4387651775eb2a3159da8bd7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48121535"
---
# <a name="create-a-visual-c-smo-project-in-visual-studio-net"></a>Crear un proyecto de Visual C# SMO en Visual Studio .NET
  En esta sección se describe cómo generar una aplicación de consola SMO simple.  
  
 En este ejemplo se importan espacios de nombres, lo que habilita al programa para que haga referencia a los tipos SMO. La importación del espacio de nombres `Agent` es opcional. Usarlo cuando se escribe un programa que usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente. El espacio de nombres `Common` se requiere para establecer una conexión segura a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El espacio de nombres `SqlClient` se utiliza para procesar los errores de excepción de SQL.  
  
### <a name="creating-a-visual-c-smo-project-in-visual-studionet"></a>Crear un proyecto de Visual C# SMO en Visual Studio.NET  
  
1.  Inicie [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] (o [!INCLUDE[vsprvslong](../../includes/vsprvslong-md.md)]).  
  
2.  En el menú **Archivo**, haga clic en **Nuevo proyecto**. Aparecerá el cuadro de diálogo **Nuevo proyecto** .  
  
3.  En **tipos de proyecto** cuadro de diálogo, seleccione **Visual C#** y, a continuación, seleccione **Windows**. En el [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] panel Plantillas instaladas, seleccione **aplicación Windows**.  
  
4.  (Opcional) En el **nombre** , escriba el nombre de la nueva aplicación  
  
5.  Seleccione el tipo de aplicación de Visual C#. Los ejemplos que siguen, seleccione **aplicación de consola**.  
  
6.  En el menú **Proyecto**, seleccione **Agregar referencia**. Aparecerá el cuadro de diálogo **Agregar referencia**.  
  
7.  Haga clic en **examinar**, busque los ensamblados SMO en los [!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)] carpeta y, a continuación, seleccione los siguientes archivos. Son los archivos mínimos necesarios para generar una aplicación SMO:  
  
     Microsoft.SqlServer.ConnectionInfo.dll  
  
     Microsoft.SqlServer.Smo.dll  
  
     Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
     Microsoft.SqlServer.SqlEnum.dll  
  
    > [!NOTE]  
    >  Utilice la tecla `Ctrl` para seleccionar más de un archivo.  
  
8.  Agregue cualquier ensamblado SMO adicional que sea necesario. Por ejemplo, si está programando específicamente [!INCLUDE[ssSB](../../includes/sssb-md.md)], agregue los ensamblados siguientes:  
  
     Microsoft.SqlServer.ServiceBrokerEmum.dll  
  
9. Haga clic en **Abrir**.  
  
10. En el **vista** menú, haga clic en **código**. - o bien seleccione el Windows Program1.cs [Diseño] y haga doble clic en el formulario windows Forms para mostrar la ventana de código.  
  
11. En el código, antes de la instrucción de espacio de nombres, escriba las instrucciones `using` siguientes para certificar los tipos en el espacio de nombres de SMO:  
  
    ```  
    using Microsoft.SqlServer.Management.Smo;  
    using Microsoft.SqlServer.Management.Common;  
    ```  
  
12. SMO cuenta con varios espacios de nombres bajo Microsoft.SqlServer.Management.Smo, como Microsoft.SqlServer.Management.Smo.Agent. Agregue los espacios de nombres que sean necesarios.  
  
13. Ahora puede agregar su código SMO.  
  
  

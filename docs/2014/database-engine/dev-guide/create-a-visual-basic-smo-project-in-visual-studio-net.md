---
title: Creación de un proyecto de Visual Basic SMO en Visual Studio .NET | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Visual Basic [SMO]
ms.assetid: d7a3892c-0f1c-4c4d-8480-b58dce3720bc
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 662916720b9953e0374bedb29890a36ced0cfac0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62753358"
---
# <a name="create-a-visual-basic-smo-project-in-visual-studio-net"></a>Crear un proyecto de Visual Basic SMO en Visual Studio .NET
  En esta sección se describe cómo generar una aplicación de consola SMO simple.  
  
 En este ejemplo se importan espacios de nombres, lo que habilita al programa para que haga referencia a los tipos SMO. La importación del espacio de nombres `Agent` es opcional. Úselo cuando esté escribiendo un programa que use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el agente. El espacio de nombres `Common` se requiere para establecer una conexión segura a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El espacio de nombres `SqlClient` se utiliza para procesar los errores de excepción de SQL.  
  
### <a name="creating-a-visual-basic-smo-project-in-visual-studionet"></a>Crear un proyecto de Visual Basic SMO en Visual Studio.NET  
  
1.  Inicie [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] (o [!INCLUDE[vsprvslong](../../includes/vsprvslong-md.md)]).  
  
2.  En el menú **Archivo**, haga clic en **Nuevo proyecto**. Aparecerá el cuadro de diálogo **Nuevo proyecto** .  
  
3.  En el cuadro de diálogo **tipos de proyecto** , seleccione **Visual Basic**y, a continuación, seleccione **Windows**. En el [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] panel Plantillas instaladas, seleccione **aplicación de consola.**  
  
4.  Opta En el campo **nombre** , escriba el nombre de la nueva aplicación.  
  
5.  Haga clic en **Aceptar** para [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] cargar la plantilla de aplicación de consola.  
  
6.  En el menú **Proyecto**, seleccione **Agregar referencia**. Aparecerá el cuadro de diálogo **Agregar referencia**.  
  
7.  Haga clic en **examinar**, busque los ensamblados SMO en la carpeta C:\Archivos de Programa\microsoft SQL Server\120\SDK\Assemblies y, a continuación, seleccione los archivos siguientes. Son los archivos mínimos necesarios para generar una aplicación SMO:  
  
     Microsoft.SqlServer.ConnectionInfo.dll  
  
     Microsoft.SqlServer.SqlEnum.dll  
  
     Microsoft.SqlServer.Smo.dll  
  
     Microsoft.SqlServer.Management.Sdk.Sfc  
  
    > [!NOTE]  
    >  Utilice la tecla `Ctrl` para seleccionar más de un archivo.  
  
8.  Agregue cualquier ensamblado SMO adicional que sea necesario. Por ejemplo, si está programando específicamente [!INCLUDE[ssSB](../../includes/sssb-md.md)], agregue los ensamblados siguientes:  
  
     Microsoft.SqlServer.ServiceBrokerEmum.dll  
  
9. Haga clic en **Abrir**.  
  
10. En el menú **Ver** , haga clic en **código**. o bien seleccione la ventana Module1. VB para mostrar la ventana de código.  
  
11. En el código, antes de cualquier declaración, escriba las instrucciones **Imports** siguientes para certificar los tipos en el espacio de nombres de SMO.  
  
    ```  
    Imports Microsoft.SqlServer.Management.Smo  
    Imports Microsoft.SqlServer.Management.Common  
    ```  
  
12. SMO cuenta con varios espacios de nombres bajo Microsoft.SqlServer.Management.Smo, como Microsoft.SqlServer.Management.Smo.Agent. Agregue los espacios de nombres que sean necesarios.  
  
13. Ahora puede agregar su código SMO.  
  
  

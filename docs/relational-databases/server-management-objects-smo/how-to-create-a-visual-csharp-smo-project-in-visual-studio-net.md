---
description: Cómo crear un proyecto de Visual C# SMO en Visual Studio .NET
title: Crear un proyecto de Visual C# SMO en Visual Studio .NET
ms.custom: seo-dt-2019
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Visual C# [SMO]
ms.assetid: 1e7abb16-23a0-4a18-91ad-253261e6bf84
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 943cfd787cccff42973862b12f0f52feae24410c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467196"
---
# <a name="how-to-create-a-visual-c-smo-project-in-visual-studio-net"></a>Cómo crear un proyecto de Visual C# SMO en Visual Studio .NET
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  En esta sección se describe cómo generar una aplicación de consola SMO simple.  
  
 En este ejemplo se importan espacios de nombres, lo que habilita al programa para que haga referencia a los tipos SMO. La importación del espacio de nombres del **agente** es opcional. Úselo cuando esté escribiendo un programa que use el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente. El espacio de nombres **común** es necesario para establecer una conexión segura con la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El espacio de nombres **SqlClient** se usa para procesar errores de excepción de SQL.  
  
### <a name="creating-a-visual-c-smo-project-in-visual-studionet"></a>Crear un proyecto de Visual C# SMO en Visual Studio.NET  
  
1. Inicio de Visual Studio
  
2. En el menú **archivo** , haga clic en **nuevo** y luego en **proyecto**.  Aparecerá el cuadro de diálogo **Nuevo proyecto** .   
  
3. En el [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] panel **instalado** , vaya a **plantillas** \\ **Visual C#** \\ **Windows** y seleccione **aplicación de consola**.  
  
4. Opta En el cuadro de texto **nombre** , escriba el nombre de la nueva aplicación.  

5. Haga clic en **Aceptar** para cargar la plantilla de aplicación de consola.  

6. Siga las instrucciones de [instalación de SMO](installing-smo.md) para instalar el paquete para que el proyecto haga referencia.
  
7. En el menú **Ver** , haga clic en **Código**.
    
8. En el código, antes de la instrucción de espacio de nombres, escriba las siguientes instrucciones **using** para certificar los tipos en el espacio de nombres de SMO:
  
    ```  
    using Microsoft.SqlServer.Management.Smo;  
    using Microsoft.SqlServer.Management.Common;  
    ```  
  
15. SMO cuenta con varios espacios de nombres bajo Microsoft.SqlServer.Management.Smo, como Microsoft.SqlServer.Management.Smo.Agent. Agregue los espacios de nombres que sean necesarios.  
  
16. Ahora puede agregar su código SMO.  


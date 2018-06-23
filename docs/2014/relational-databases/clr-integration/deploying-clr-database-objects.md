---
title: Implementar objetos de base de datos CLR | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- deployment script [CLR integration]
- common language runtime [SQL Server], deploying
- deploying assemblies [CLR integration]
- deploying [CLR integration]
ms.assetid: 00752573-3367-41a7-af98-7b7a29e8e2f2
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 724a0782d1d97296797a58070addf568858473e1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112788"
---
# <a name="deploying-clr-database-objects"></a>Implementar objetos de base de datos de CLR
  La implementación es el proceso mediante el cual se distribuye una aplicación o módulo finalizados para su instalación y ejecución en otro equipo. Con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio, puede desarrollar objetos de base de datos de Common Language Runtime (CLR) e implementarlos en un servidor de prueba. Los objetos de base de datos administrados también pueden compilarse con los archivos de redistribución de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework en lugar de Visual Studio. Una vez compilados, los ensamblados que contienen objetos de base de datos de CLR pueden implementarse en un servidor de prueba mediante instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)] o Visual Studio. Tenga en cuenta que Visual Studio .NET 2003 no puede utilizarse para programar o implementar la integración CLR. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] incluye .NET Framework preinstalado y Visual Studio .NET 2003 no puede utilizar los ensamblados de .NET Framework 2.0.  
  
 Una vez que los métodos CLR se han probado y comprobado en el servidor de prueba, pueden distribuirse a los servidores de producción a través de un script de implementación. El script de implementación puede generarse manualmente o utilizando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] (vea el procedimiento posteriormente en este tema).  
  
 La característica de integración con CLR está desactivada de forma predeterminada en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y debe habilitarse para poder usar ensamblados CLR. Para más información, consulte [Enabling CLR Integration](clr-integration-enabling.md).  
  
## <a name="deploying-the-assembly-to-the-test-server"></a>Implementar el ensamblado en el servidor de prueba  
 Con Visual Studio, puede desarrollar funciones, procedimientos, desencadenadores, tipos definidos por el usuario (UDT) o agregados definidos por el usuario (UDA) de CLR e implementarlos en un servidor de prueba. Estos objetos de base de datos administrados también pueden compilarse con los compiladores de línea de comandos que se incluyen con los archivos de redistribución de .NET Framework, como csc.exe y vbc.exe. No es necesario usar el entorno de desarrollo integrado de Visual Studio para desarrollar objetos de base de datos administrados para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Asegúrese de resolver todos los errores y advertencias del compilador. Los ensamblados que contienen las rutinas CLR pueden registrarse en una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)] o Visual Studio.  
  
> [!NOTE]  
>  El protocolo de red TCP/IP debe habilitarse en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a fin de utilizar [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio para el desarrollo remoto, la depuración y el desarrollo. Para obtener más información acerca de cómo habilitar el protocolo TCP/IP en el servidor, consulte [configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md).  
  
#### <a name="to-deploy-the-assembly-using-visual-studio"></a>Para implementar el ensamblado mediante Visual Studio  
  
1.  Compile el proyecto seleccionando **generar** \<nombre del proyecto > desde la **generar** menú.  
  
2.  Resuelva todos los errores y advertencias de generación antes de implementar el ensamblado en el servidor de prueba.  
  
3.  Seleccione **implementar** desde el **generar** menú. El ensamblado se registrará en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y la base de datos especificada cuando el proyecto de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se creó por primera vez en Visual Studio.  
  
#### <a name="to-deploy-the-assembly-using-transact-sql"></a>Para implementar el ensamblado mediante Transact-SQL  
  
1.  Compile el ensamblado del archivo de código fuente utilizando los compiladores de línea de comandos que se incluyen con .NET Framework.  
  
2.  Para los archivos de código fuente de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#:  
  
3.  `csc /target:library C:\helloworld.cs`  
  
4.  Para los archivos de código fuente de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic:  
  
 `vbc /target:library C:\helloworld.vb`  
  
 Estos comandos inician el compilador de Visual C# o Visual Basic utilizando la opción `/target` para especificar la creación de un archivo DLL de biblioteca.  
  
1.  Resuelva todos los errores y advertencias de generación antes de implementar el ensamblado en el servidor de prueba.  
  
2.  Abra [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] en el servidor de prueba. Cree una nueva consulta conectada a una base de datos de prueba apropiada (como AdventureWorks).  
  
3.  Cree el ensamblado en el servidor agregando el siguiente código [!INCLUDE[tsql](../../../includes/tsql-md.md)] a la consulta.  
  
 `CREATE ASSEMBLY HelloWorld from 'c:\helloworld.dll' WITH PERMISSION_SET = SAFE;`  
  
1.  Después, debe crear el procedimiento, función, agregado, tipo definido por el usuario o desencadenador en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si el ensamblado `HelloWorld` contiene un método denominado `HelloWorld` en la clase `Procedures`, puede agregarse el siguiente código [!INCLUDE[tsql](../../../includes/tsql-md.md)] a la consulta para crear un procedimiento denominado `hello` en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 `CREATE PROCEDURE hello`  
  
 `AS`  
  
 `EXTERNAL NAME HelloWorld.Procedures.HelloWorld`  
  
 Para obtener más información acerca de cómo crear los distintos tipos de objetos de base de datos administrados en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [funciones definidos](../clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md), [agregados definidos](../clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md), [CLR Tipos definidos por el usuario](../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md), [procedimientos almacenados de CLR](../../database-engine/dev-guide/clr-stored-procedures.md), y [desencadenadores CLR](../../database-engine/dev-guide/clr-triggers.md).  
  
## <a name="deploying-the-assembly-to-production-servers"></a>Implementar el ensamblado en servidores de producción  
 Una vez probados y comprobados los objetos de base de datos de CLR en el servidor de prueba, pueden distribuirse a los servidores de producción. Para obtener más información sobre la depuración de objetos de base de datos administrados, vea [depurar objetos de base de datos de CLR](debugging-clr-database-objects.md).  
  
 La implementación de objetos de base de datos administrados es similar a la de los objetos de base de datos normales (tablas, rutinas [!INCLUDE[tsql](../../../includes/tsql-md.md)], etc.) Los ensamblados que contienen los objetos de base de datos de CLR pueden implementarse en otros servidores utilizando un script de implementación. El script de implementación puede generarse utilizando la funcionalidad "Generar scripts" de [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]. El script de implementación también puede generarse manualmente o puede generarse utilizando "Generar scripts" y modificarse manualmente. Una vez generado el script de implementación, puede ejecutarse en otras instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para implementar los objetos de base de datos administrados.  
  
#### <a name="to-generate-a-deployment-script-using-generate-scripts"></a>Para generar un script de implementación utilizando la funcionalidad de generación de scripts  
  
1.  Abra [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] y conéctese a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] donde esté registrado el ensamblado administrado o el objeto de base de datos que va a implementarse.  
  
2.  En el **Explorador de objetos**, expanda la  **\<nombre del servidor >** y **bases de datos** árboles. Haga clic en la base de datos donde el objeto de base de datos administrado está registrado, seleccione **tareas**y, a continuación, seleccione **generar secuencias de comandos**. Se abrirá el Asistente para script.  
  
3.  Seleccione la base de datos en el cuadro de lista y haga clic en **siguiente**.  
  
4.  En el **elegir opciones de Script** panel, haga clic en **siguiente**, o cambiar las opciones y, a continuación, haga clic en **siguiente**.  
  
5.  En el **elegir tipos de objeto** panel, elija el tipo de objeto de base de datos para su implementación. Haga clic en **Siguiente**.  
  
6.  Para cada tipo de objeto seleccionado en el **elegir tipos de objeto** panel, un **elegir \<tipo >** se presenta el panel. En este panel, puede elegir entre todas las instancias de ese tipo de objeto de base de datos registradas en la base de datos especificada. Seleccione uno o más objetos y haga clic en **siguiente**.  
  
7.  El **opciones de salida** panel aparece cuando todos los de la base de datos deseada se han seleccionado tipos de objetos. Seleccione **generar Script en archivo** y especifique una ruta de acceso de la secuencia de comandos. Seleccione **Siguiente**. Revise sus selecciones y haga clic en **finalizar**. El script de implementación se guardará en la ruta de acceso de archivo especificada.  
  
## <a name="post-deployment-scripts"></a>Scripts posteriores a la implementación  
 Puede ejecutar un script posterior a la implementación.  
  
 Para agregar un script posterior a la implementación, agregue un archivo denominado postdeployscript.sql a su directorio de proyecto de Visual Studio. Por ejemplo, haga clic con el proyecto en **el Explorador de soluciones** y seleccione **Agregar elemento existente**. Agregue el archivo a la raíz del proyecto, en lugar de agregarlo a la carpeta de scripts de prueba.  
  
 Cuando haga clic en Implementar, Visual Studio ejecutará este script tras la implementación del proyecto.  
  
## <a name="see-also"></a>Vea también  
 [Conceptos de programación en el ámbito de la integración de Common Language Runtime &#40;CLR&#41;](common-language-runtime-clr-integration-programming-concepts.md)  
  
  
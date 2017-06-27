---
title: Iniciar SQL Server Management Studio | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 25ffaea6-0eee-4169-8dd0-1da417c28fc6
caps.latest.revision: 45
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 5db067d5a2fe5bbf9953484c9a999ed7b1fcddae
ms.openlocfilehash: c472ec73a5b0b24f47b5bc59121eda206e285ac9
ms.contentlocale: es-es
ms.lasthandoff: 06/23/2017

---
# <a name="lesson-1-1---start-sql-server-management-studio"></a>Lección 1.1: Iniciar SQL Server Management Studio
Para empezar este tutorial, veamos [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="opening-sql-server-management-studio"></a>Abrir SQL Server Management Studio  
  
#### <a name="to-open-sql-server-management-studio"></a>Para abrir SQL Server Management Studio  
  
1.  Cómo inicia [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] (SSMS) depende de su sistema operativo.  
* Para las versiones más recientes de Windows con una **página de inicio**, en la **página de inicio**, escriba **[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]** y aparecerá el programa. Haga clic en el programa para abrir SSMS. Puede que quiera hacer clic con el botón derecho en el programa y anclarlo a la **página de inicio**.   
* Para versiones anteriores de Windows, en el menú **Inicio** , seleccione **Todos los programas**, señale [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]y, luego, haga clic en **SQL Server Management Studio**. De manera alternativa, desde el cuadro de diálogo **Ejecutar** , escriba **SSMS.exe** y, después, haga clic en **Aceptar**.  
  
    > [!NOTE]  
    >  Si SSMS no aparece, puede que no lo haya instalado correctamente. Instale SSMS desde el [Centro de descarga](https://msdn.microsoft.com/library/mt238290.aspx). SSMS no se instala automáticamente con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016. Use la última versión para tener acceso a todas las características.  
  
2.  En el siguiente paso, conéctese a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante el componente del **Explorador de objetos** de SSMS. Si el panel del Explorador de objetos no está visible, en el menú **Ver** , haga clic en **Explorador de objetos**. En el menú del Explorador de objetos, haga clic en el botón **Conectar** y, después, en **Motor de base de datos**. Debe aparecer el cuadro de diálogo **Conectar al servidor** . (Si ha instalado anteriormente SSMS, la configuración de usuario puede estar provocando que el cuadro de diálogo **Conectar al servidor** aparezca automáticamente).  
  
3.  En el cuadro de diálogo **Conectar al servidor** , complete el cuadro **Nombre de servidor** . Puede conectarse a uno de los tres tipos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada tipo tiene un formato ligeramente diferente del cuadro **Nombre de servidor** . Seleccione uno de los formatos siguientes:  
--  **Instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:** cuando instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un equipo, puede especificar que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sea una instancia con nombre o una instancia predeterminada (instancia sin nombre). Si se está conectando a una instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], inserte el nombre del equipo. Por ejemplo, si está ejecutando SSMS en un equipo denominado Contabilidad y se está conectando a una instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  instalada en ese equipo, escriba **Contabilidad** en el cuadro **Nombre de servidor** .  
--  **Instancia con nombre de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:** al configurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede especificar un nombre para la instancia; por ejemplo, en un equipo denominado Contabilidad, puede especificar una instancia con nombre denominada **Cobros**. Para conectarse a una instancia con nombre, en el cuadro **Nombre de servidor** , escriba el nombre del equipo, barra diagonal inversa, nombre de instancia; por ejemplo, **Contabilidad\Cobros**.  
--  **Azure SQL Database:** el formato del nombre del servidor de SQL Database es Nombre_servidor_SQL.database.windows.net, por ejemplo, **mydb2.database.windows.net**. Si tiene problemas para determinar el nombre del servidor, visite Azure Portal para obtener ayuda para crear una cadena de conexión.  
  
4. En el área **Autenticación**  
  
## <a name="management-studio-components"></a>Componentes de Management Studio  
[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] presenta la información en ventanas dedicadas a tipos de información específicos. La información de la base de datos se muestra en las ventanas de documentos y en el Explorador de objetos.  
  
-   El Explorador de objetos es una vista de árbol de todos los objetos de base de datos que contiene un servidor. Puede incluir las bases de datos de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]e [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. El Explorador de objetos incluye información de todos los servidores a los que está conectado. Al abrir [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], se le solicita que se conecte al Explorador de objetos aplicando la última configuración utilizada. Para conectarse a un servidor, no es necesario que lo registre. Solo tiene que hacer doble clic en cualquier servidor del componente Servidores registrados.  
  
-   La ventana de documento es el área de mayor tamaño de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Esta ventana puede contener editores de consulta y ventanas de explorador. De forma predeterminada, se muestra la página Resumen, conectada a la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] del equipo actual.  
  
## <a name="showing-additional-windows"></a>Mostrar ventanas adicionales  
  
#### <a name="to-show-the-registered-servers-window"></a>Para mostrar la ventana Servidores registrados  
  
1.  En el menú **Ver** , haga clic en **Servidores registrados**.  
  
    La ventana Servidores registrados aparece encima o adyacente al Explorador de objetos. Puede arrastrarla y acoplarla en varias ubicaciones. Servidores registrados enumera los servidores que el usuario administra habitualmente. Puede agregar y quitar los servidores de esta lista. Solo aparecerán en la lista los servidores de las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se encuentren en el equipo donde se ejecuta [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  Si no aparece su servidor, en Servidores registrados, haga clic con el botón derecho en **Motor de base de datos**, en **Tareas**y, después, en **Update Local Server Registration**(Actualizar registro de servidor local). Para agregar servidores SQL Server o una SQL Database adicional, haga clic con el botón derecho en una ubicación de Servidores registrados y, después, haga clic en **Nuevo registro de servidor**. Complete el área **Inicio de sesión** como ha completado el cuadro de diálogo **Conectar al servidor** .  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Conectar con el Explorador de objetos y Servidores registrados](../../tools/sql-server-management-studio/lesson-1-2-connect-with-registered-servers-and-object-explorer.md)  
  


---
title: Herramientas externas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- External Tools dialog box
ms.assetid: d7dae88f-0781-4162-96cd-d3a3a4d82035
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 17e385913c362a2921d715607ca590d66ed69a48
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262814"
---
# <a name="external-tools"></a>Herramientas externas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Utilice este cuadro de diálogo para agregar herramientas externas, como el Administrador de configuración de SQL Server o el Bloc de notas, al menú **Herramientas** . La adición de herramientas externas facilita el inicio de otras aplicaciones mientras se trabaja con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Cuando inicie la herramienta, podrá especificar argumentos y un directorio de trabajo. Además, los resultados de algunas herramientas pueden mostrarse en la ventana Resultados. El cuadro de diálogo **Herramientas externas** está disponible en el menú **Herramientas** .  
  
## <a name="options"></a>Opciones  
**Contenido del menú**  
Enumera los títulos de los elementos agregados actualmente al menú **Herramientas** . Use las flechas **Subir** y **Bajar** para cambiar el orden de los elementos que aparecen en el menú. Use el botón **Eliminar** para quitar un elemento del menú.  
  
**Subir**  
Mueva la herramienta seleccionada a una posición superior en la lista de herramientas que aparece en el menú **Herramientas** .  
  
**Bajar**  
Mueva la herramienta seleccionada a una posición inferior en la lista de herramientas que aparece en el menú **Herramientas** .  
  
**Agregar**  
Borra los cuadros de texto de modo que se pueda especificar una herramienta nueva.  
  
**Eliminar**  
Quite la herramienta o el comando de la lista **Contenido del menú** y del menú **Herramientas** .  
  
**Title**  
Nombre de la herramienta o del comando que aparecerá en el submenú **Herramientas externas** del menú **Herramientas** . Coloque una "y" comercial (&) antes de una letra del nombre de la herramienta para utilizar dicha letra como tecla de aceleración de la herramienta. Por ejemplo, `&Spy++` aparecería como **Spy++** en el menú **Herramientas** .  
  
**Command**  
Especifica la ruta de acceso al archivo .exe, .com, .pif, .bat, .cmd u otro que se intente iniciar. Si activa la casilla `.bat`Usar la ventana de resultados `.com`, podrá ver el resultado de los archivos **,** y de otros archivos en la ventana Resultados.  
  
**Argumentos**  
Especifica las variables que pasan a la herramienta cuando ésta se selecciona en el menú. Los argumentos pueden especificar valores que pasan a la herramienta o el comando cuando estos se inician. Por ejemplo, un valor puede especificar un nombre de archivo o un directorio. Use el botón de **flecha** para seleccionar entre una lista de argumentos predefinidos. Es posible agregar más de uno. Para obtener una lista completa de los argumentos predefinidos y sus definiciones, vea [Arguments for External Tools](../../ssms/use-of-sql-server-features-and-capabilities-wwi-oltp.md). También puede escribir argumentos personalizados (modificadores de la línea de comandos, por ejemplo) en función del comando o la herramienta que utilice.  
  
**Directorio inicial**  
Especifica el directorio de trabajo de la herramienta. Use el botón de **flecha** para seleccionar directorios. Es posible seleccionar más de uno.  
  
**Use output Window**  
Especifique si los resultados de la herramienta se muestran en la ventana Resultados. Esta opción solo está disponible para archivos que generalmente muestran los resultados en la ventana de la línea de comandos, como los archivos .bat y .com. Si está habilitada, esta ventana facilita la administración de ventanas cuando se sigue el progreso de una herramienta.  
  
**Solicitar argumentos**  
Muestra el cuadro de diálogo **Argumentos** , que le permite especificar y modificar valores para los argumentos cada vez que se inicia la herramienta externa.  
  
**Tratar resultado como Unicode**  
Permite que la ventana de resultados acepte Unicode.  
  
**Cerrar al salir**  
Cierra la ventana abierta por la herramienta cuando ésta se cierra.  
  
## <a name="example"></a>Ejemplo  
  
#### <a name="to-add-sql-server-configuration-manager-to-the-tools-menu"></a>Para agregar Administrador de configuración de SQL Server al menú Herramientas  
  
1.  En el menú **Herramientas** , haga clic en **Herramientas externas**.  
  
2.  En el cuadro **Título** , escriba **Administrador de configuración de SQL Server**.  
  
3.  En el cuadro **Comando** , escriba la ruta de acceso al archivo ejecutable de [!INCLUDE[msCoName](../../includes/msconame_md.md)] Management Console, por ejemplo, **C:\WINNT\system32\mmc.exe**  
  
4.  En el cuadro **Argumentos** , escriba la ruta de acceso al archivo .msc, por ejemplo, **"C:\WINNT\system32\SQLServerManager.msc"**  
  
> [!NOTE]  
> Vea las propiedades del acceso directo de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] en el menú **Inicio** para confirmar la ubicación de los archivos en el equipo.  

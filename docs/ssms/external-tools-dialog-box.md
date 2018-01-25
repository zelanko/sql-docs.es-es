---
title: "Herramientas externas (cuadro de diálogo) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- adding external tools
- external tools [SQL Server Management Studio]
- SQL Server Management Studio [SQL Server], external tools
ms.assetid: ba797203-24d0-4922-9b97-8ab483f1db14
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eee32bf86aca8d55ca8ebddceb3f46e635f11ad8
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2018
---
# <a name="external-tools-dialog-box"></a>Cuadro de diálogo Herramientas externas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Use el cuadro de diálogo **Herramientas externas** para agregar herramientas externas como SQLCMD o el Bloc de notas al menú **Herramientas**. La adición de herramientas externas permite iniciar fácilmente otras aplicaciones mientras se trabaja en el entorno de [!INCLUDE[msCoName](../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] . Cuando inicie la herramienta, podrá especificar argumentos y un directorio de trabajo. Además, el resultado de algunas herramientas puede verse en la **Ventana de resultados** . El cuadro de diálogo **Herramientas externas** está disponible en el menú **Herramientas** .  
  
## <a name="options"></a>.  
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
Especifique el nombre de la herramienta o el comando que aparecerá en el submenú **Herramientas externas** del menú **Herramientas** . Coloque una y comercial (&) antes de una letra del nombre de la herramienta para que esa letra sea un método abreviado de teclado. Por ejemplo, "&SQLCMD" mostraría SQLCMD en el menú **Herramientas**.  
  
**Command**  
Especifique la ruta de acceso al archivo que se va a iniciar.  
  
**Argumentos**  
Especifica las variables que pasan a la herramienta cuando ésta se selecciona en el menú. Los argumentos pueden especificar valores que pasan a la herramienta o el comando cuando estos se inician. Por ejemplo, un valor puede especificar un nombre de archivo o un directorio. Utilice el botón de flecha para seleccionar entre una lista de argumentos predefinidos. Es posible agregar más de uno. Para obtener una lista completa de los argumentos predefinidos y sus definiciones, vea [Arguments for External Tools](../ssms/use-of-sql-server-features-and-capabilities-wwi-oltp.md). También puede especificar argumentos personalizados (por ejemplo, modificadores de la línea de comandos) según el comando o la herramienta que utilice.  
  
**Usar la ventana de resultados**  
Abra la ventana de resultados de [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] para mostrar el resultado del comando que se está ejecutando. No todas las herramientas presentan el resultado en un formato que puede verse en la ventana de resultados. Para más información, consulte [Ventana Resultados](http://msdn.microsoft.com/en-us/9808e00c-c8f6-45cc-896e-192b8420f747).  
  
**Tratar resultado como Unicode**  
Interpreta el resultado como Unicode.  
  
**Directorio inicial**  
Especifica el directorio de trabajo de la herramienta. Utilice el botón de flecha para seleccionar directorios. Es posible seleccionar más de uno.  
  
**Solicitar argumentos**  
Muestra el cuadro de diálogo **Argumentos** , que permite especificar y modificar valores para los argumentos cada vez que se inicia la herramienta externa.  
  
**Cerrar al salir**  
Cierra la ventana abierta por la herramienta cuando ésta se cierra.  
  
## <a name="example"></a>Ejemplo  
Al especificar los siguientes valores en el cuadro de diálogo **Herramientas externas** se creará un elemento de menú denominado "DAC" que, cuando se selecciona, abre un símbolo del sistema y ejecuta la utilidad **sqlcmd** con la conexión de administrador dedicada.  
  
|Cuadro|Valor|  
|-------|---------|  
|**Title**|DAC|  
|**Command**|[!INCLUDE[ssInstallPath](../includes/ssinstallpath_md.md)]Tools\Binn\SQLCMD.exe|  
|**Argumentos**|-A|  
  
## <a name="see-also"></a>Ver también  
[Argumentos de las herramientas externas](../ssms/use-of-sql-server-features-and-capabilities-wwi-oltp.md)  
[Elementos generales de la interfaz de usuario](../ssms/general-user-interface-elements.md)  
  

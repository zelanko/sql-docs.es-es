---
title: Crear procedimientos almacenados | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- registering assemblies
- database assemblies [Analysis Services]
- server assemblies [Analysis Services]
- stored procedures [Analysis Services], creating
- assemblies [Analysis Services]
ms.assetid: a12ff02f-6d0b-4488-9846-3609fc0d0554
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7beb77adf595b055a6c1e4a7543b428a06ce7640
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62703093"
---
# <a name="creating-stored-procedures"></a>Creación de procedimientos almacenados
  Todos los procedimientos almacenados deben asociarse a una clase de Common Language Runtime (CLR) o Modelo de objetos componentes (COM) para poder usarse. La clase debe instalarse en el servidor (normalmente en forma de una [!INCLUDE[msCoName](../../includes/msconame-md.md)] biblioteca de vínculos dinámicos (dll) de ActiveX® y registrada como un ensamblado en el servidor o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en una base de datos.  
  
 Los procedimientos almacenados se registran en un servidor o en una base de datos. Se puede llamar a los procedimientos almacenados del servidor desde cualquier contexto de consulta. Solo se puede tener acceso a los procedimientos almacenados de base de datos si el contexto de base de datos es la base de datos bajo la cual se define el procedimiento almacenado. Si las funciones de un ensamblado llaman a las funciones en otro ensamblado, debe registrar ambos ensamblados en el mismo contexto (servidor o base de datos). Para un servidor o una base [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de datos implementada en un servidor, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] puede usar para registrar un ensamblado. Para un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], puede usar el Diseñador de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para registrar un ensamblado en el proyecto.  
  
> [!IMPORTANT]  
>  Los ensamblados COM pueden suponer un riesgo para la seguridad. Debido a esto y a otras consideraciones, los ensamblados COM están en desuso en [!INCLUDE[ssASversion10](../../includes/ssasversion10-md.md)]. Es posible que este tipo de ensamblados no esté disponible en versiones futuras.  
  
## <a name="registering-a-server-assembly"></a>Registro de un ensamblado de servidor  
 En el Explorador de objetos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], los ensamblados de servidor aparecen en la carpeta Ensamblados bajo una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Los ensamblados de servidor pueden contener ensamblados .NET (CLR) y bibliotecas COM.  
  
### <a name="to-create-a-server-assembly"></a>Para crear un ensamblado de servidor  
  
1.  Expanda la instancia [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de en explorador de objetos, haga clic con el botón secundario en la carpeta **ensamblados** y, a continuación, haga clic en **nuevo ensamblado**. Esto muestra el cuadro de diálogo **registrar ensamblado de servidor** .  
  
2.  En **tipo** , especifique el tipo de ensamblado:  
  
    -   Para una DLL de código administrado (CLR), especifique Ensamblado .NET.  
  
    -   Para un archivo DLL de código nativo (COM), especifique DLL de COM.  
  
3.  En **nombre de archivo**, especifique el archivo DLL que contiene los procedimientos almacenados.  
  
4.  En **nombre de ensamblado**, especifique un nombre para el ensamblado.  
  
5.  Si se trata de una compilación de depuración de la biblioteca que va a usar para depurar procedimientos almacenados, active la casilla **incluir información de depuración** . Para obtener más información sobre la depuración de procedimientos almacenados, vea [depurar procedimientos almacenados](debugging-stored-procedures.md).  
  
6.  Puede hacer clic en **Aceptar** para registrar el ensamblado inmediatamente, o bien, en la barra de herramientas del cuadro de diálogo, puede hacer clic en un comando del menú **script** para incluir en el script la acción de registro en una ventana de consulta, un archivo o el portapapeles.  
  
 Después de registrar un ensamblado de servidor, puede configurarlo haciendo clic con el botón secundario en el ensamblado en Explorador de objetos y, a continuación, haciendo clic en **propiedades**.  
  
## <a name="registering-a-database-assembly-on-the-server"></a>Registrar un ensamblado de base de datos en el servidor  
 En el Explorador de objetos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], los ensamblados de base de datos aparecen en la carpeta Ensamblados bajo una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Los ensamblados de base de datos pueden contener ensamblados .NET (CLR) y bibliotecas COM.  
  
### <a name="to-create-a-database-assembly-on-a-server"></a>Para crear un ensamblado de base de datos en un servidor  
  
1.  Expanda la instancia [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de la base de datos en explorador de objetos, haga clic con el botón secundario en la carpeta **ensamblados** y, a continuación, haga clic en **nuevo ensamblado**. Esto muestra el cuadro de diálogo **registrar ensamblado de base de datos** .  
  
2.  En **tipo** , especifique el tipo de ensamblado:  
  
    -   Para una DLL de código administrado (CLR), especifique Ensamblado .NET.  
  
    -   Para una DLL de código nativo (COM), especifique DLL COM.  
  
3.  En **nombre de archivo**, especifique el archivo DLL que contiene los procedimientos almacenados.  
  
4.  En **nombre de ensamblado**, especifique un nombre para el ensamblado.  
  
5.  Si se trata de una compilación de depuración de la biblioteca que va a usar para depurar procedimientos almacenados, active la casilla **incluir información de depuración** . Para obtener más información sobre la depuración de procedimientos almacenados, vea [depurar procedimientos almacenados](debugging-stored-procedures.md).  
  
6.  Puede hacer clic en **Aceptar** para registrar el ensamblado inmediatamente, o bien, en la barra de herramientas del cuadro de diálogo, puede hacer clic en un comando del menú **script** para incluir en el script la acción de registro en una ventana de consulta, un archivo o el portapapeles.  
  
 Después de registrar un ensamblado de base de datos, puede configurarlo haciendo clic con el botón secundario en el ensamblado en Explorador de objetos y, a continuación, haciendo clic en **propiedades**.  
  
## <a name="registering-a-database-assembly-in-a-project"></a>Registrar un ensamblado de base de datos en un proyecto  
 En el Explorador de soluciones de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], los ensamblados de base de datos aparecen en la carpeta Ensamblados bajo un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Los ensamblados de base de datos pueden contener ensamblados .NET (CLR) y bibliotecas COM.  
  
### <a name="to-create-a-database-assembly-in-an-analysis-service-project"></a>Para crear un ensamblado de base de datos en un proyecto de Analysis Service  
  
1.  Expanda la instancia [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de la base de datos en explorador de objetos, haga clic con el botón secundario en la carpeta **ensamblados** y haga clic en **nueva referencia de ensamblado**. Esto muestra el cuadro de diálogo **Agregar referencia** . En la pestaña **.net** del cuadro de diálogo **Agregar referencia se** enumeran los ensamblados .net (CLR) existentes, mientras que la pestaña **proyectos** enumera los proyectos.  
  
2.  Puede hacer clic en un componente o proyecto existente y, **** a continuación, hacer clic en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] agregar para agregarlo al proyecto. Para agregar una referencia a una DLL COM, haga clic en la pestaña **examinar** para buscar el archivo. La lista **proyectos y componentes seleccionados** muestra el nombre, el tipo, la versión y la ubicación de cada componente que se va a agregar al proyecto.  
  
3.  Cuando haya terminado de seleccionar los componentes que desea agregar, haga clic en **Aceptar** para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] agregarlos al proyecto.  
  
## <a name="script-format-for-an-assembly"></a>Formato de script para un ensamblado  
 Registrar un ensamblado .NET es bastante sencillo. Un ensamblado .NET se agrega a una base de datos en formato binario con el siguiente formato:  
  
```  
<Create>  
   <ObjectDefinition>  
      <Assembly>  
         <Files>  
            <File>  
               <Name>filename</Name>  
               <Type>filetype</Type>  
               <Data>  
                  <Block>binarydatablock</Block>  
                  <Block>binarydatablock</Block>  
                  ...  
               </Data>  
            </File>  
         </Files>  
         <PermissionSet>PermissionSet</PermissionSet>  
      </Assembly>  
   <ObjectDefinition>  
</Create>  
```  
  
## <a name="see-also"></a>Consulte también  
 [Administración de ensamblados de modelos multidimensionales](../multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definir procedimientos almacenados](defining-stored-procedures.md)  
  
  

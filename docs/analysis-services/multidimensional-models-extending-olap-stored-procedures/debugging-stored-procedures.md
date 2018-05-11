---
title: Depurar procedimientos almacenados | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6aecd65eb6b41b6b573bc7c4c13c3eb16b0dc2e9
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="debugging-stored-procedures"></a>Depurar procedimientos almacenados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Los procedimientos almacenados de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] son bibliotecas CLR o COM (generalmente DLL) escritas en C# (u otro lenguaje de bibliotecas CLR o COM). Por consiguiente, la depuración de un procedimiento almacenado es muy similar a la depuración de cualquier otra aplicación del entorno de depuración de Visual Studio. Los procedimientos almacenados del entorno de desarrollo de Visual Studio pueden depurarse con las funciones de depuración integradas. Con ellas podrá detenerse en ubicaciones de procedimientos, inspeccionar los valores de memoria y registro, cambiar variables, observar el tráfico de mensajes y examinar cómo funciona el código.  
  
### <a name="to-debug-a-stored-procedure"></a>Para depurar un procedimiento almacenado  
  
1.  Abra el proyecto utilizado para crear la DLL en Visual Studio.  
  
2.  Cree puntos de interrupción en el método o función correspondiente al procedimiento que desee depurar.  
  
3.  Utilice Visual Studio para crear una compilación de depuración de una DLL del procedimiento almacenado.  
  
4.  Implemente la DLL en el servidor. Para obtener más información sobre cómo implementar el archivo DLL en el servidor, consulte [crear procedimientos almacenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/creating-stored-procedures.md).  
  
5.  Se necesita una aplicación que llame al procedimiento almacenado que desee probar. Si no dispone de una, puede utilizar el Editor de consultas MDX de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para crear una consulta MDX que llame al procedimiento almacenado que desee probar.  
  
6.  En Visual Studio, adjunte al proceso de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (Msmdsrv.exe).  
  
    1.  Desde el **depurar** menú, elija **toProcess asociar**.  
  
    2.  En el **asociar toProcess** cuadro de diálogo, seleccione **Mostrar procesos de todos los usuarios**.  
  
    3.  En el **procesos disponibles** lista el **proceso** columna, haga clic en **Msmdsrv.exe**. Si se ejecutase más de una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el servidor, necesita identificar el proceso mediante el Id. de la instancia que desee utilizar.  
  
    4.  En el **adjuntar a** texto cuadro, asegúrese de que está seleccionado el tipo de programa adecuado. Para una DLL de CLR, haga clic en **seleccione**, a continuación, haga clic en **depurar estos tipos de código**, a continuación, haga clic en **administrada**, a continuación, haga clic en **Aceptar**. Para una DLL de COM, haga clic en **seleccione**, a continuación, haga clic en **depurar estos tipos de código**, a continuación, haga clic en **nativo**, a continuación, haga clic en **Aceptar**.  
  
    5.  Haga clic en **adjuntar**.  
  
7.  En [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], invoque el programa o el script MDX que llama al procedimiento almacenado. El depurador se interrumpirá al alcanzar una línea que contiene un punto de interrupción. Podrá evaluar variables en la ventana de inspección, ver variables locales y reproducir el código.  
  
 Si experimenta problemas al depurar una biblioteca, compruebe que el archivo de la base de datos del programa (PDB) correspondiente se ha copiado en la ubicación de implementación del servidor. Si no se ha copiado el archivo durante el registro o la implementación, es necesario copiarlo manualmente en la misma ubicación que la DLL. En el código nativo (DLL de COM), el archivo PDB reside en el subdirectorio \debug. En el código administrado (DLL de CLR), reside en el subdirectorio \WINDEBUG.  
  
## <a name="see-also"></a>Vea también  
 [Administración de ensamblados de modelos multidimensionales](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definir procedimientos almacenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  

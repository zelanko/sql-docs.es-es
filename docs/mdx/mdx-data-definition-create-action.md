---
title: "Instrucción CREATE ACTION (MDX) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE ACTION
- Action
- CREATE
- CREATE_ACTION
dev_langs: kbMDX
helpviewer_keywords:
- invocation types [MDX]
- dimensions [Analysis Services], actions
- CREATE ACTION statement
- cubes [Analysis Services], actions
- actions [MDX]
- hierarchies [Analysis Services], actions
ms.assetid: 0419f349-ece2-42ba-8552-a1023f268a41
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 7b2ba808abe506ddf10078e7f8dd4ae0f693c1b6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mdx-data-definition---create-action"></a>Definición de datos MDX - Crear acción
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea una acción que puede asociarse con un objeto subordinado, cubo, dimensión, o jerarquía.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE ACTION CURRENTCUBE | Cube_Name  
   .Action_Name <action body>  
<action body> ::=   
FOR   
        CUBE   
    | Hierarchy_Name [MEMBERS]   
    | Level_Name [MEMBERS]   
    | CELLS   
    | SET }   
      AS 'MDX_Expression'   
        [, TYPE = '  
              { URL   
            | HTML   
            | STATEMENT   
               | DATASET   
            | ROWSET   
            | COMMANDLINE   
               | PROPRIETARY }   
         ']  
   [ , INVOCATION = 'INTERACTIVE | ON_OPEN | BATCH ' ]  
   [ , APPLICATION = String_Expression ]  
   [ , DESCRIPTION = String_Expression ]  
   [ , CAPTION = 'MDX_Expression' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Restricciones obligatorias Cube_Name*  
 Cadena válida que proporciona un nombre de cubo.  
  
 *Nombre de Action_*  
 Cadena válida que proporciona el nombre de la acción que se va a crear.  
  
 *Nombre de Hierarchy_*  
 Cadena válida que proporciona un nombre de jerarquía.  
  
 *Nombre producirá*  
 Cadena válida que proporciona un nombre de nivel.  
  
 *Nombre de Member_*  
 Cadena válida que proporciona un nombre de miembro o una clave de miembro.  
  
 *MDX_Expression*  
 Una expresión MDX válida.  
  
 *String_Expression*  
 Expresión de cadena válida.  
  
## <a name="remarks"></a>Comentarios  
 Es posible que las aplicaciones cliente creen y ejecuten acciones que no son seguras; también es posible que las aplicaciones cliente utilicen funciones no seguras. Para evitar estas situaciones, utilice la **Safety Options** propiedad. Para obtener más información, vea el tema sobre la propiedad de opciones de seguridad.  
  
> [!NOTE]  
>  Esta instrucción se incluye por compatibilidad con versiones anteriores. Las acciones nuevas para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], como acciones de obtención de detalles o un informe, no se admiten.  
  
## <a name="action-types"></a>Tipos de acción  
 La tabla siguiente describen los diferentes tipos de acciones disponibles en [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
|Tipo de acción|Description|  
|-----------------|-----------------|  
|**Dirección URL**|La cadena de acción que se devuelve es una dirección URL que debe abrirse mediante un explorador de Internet.<br /><br /> Nota: Si esta acción no se inicia con `http://` o `https://`, la acción estará disponible para el explorador a menos que **SafetyOptions** está establecido en **DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL**.|  
|**HTML**|La cadena de acción que se devuelve es un script HTML. La cadena debe guardarse en un archivo y ese archivo debe representarse mediante un explorador de Internet. En este caso, un script completo debe ejecutarse como parte del HTML generado.|  
|**INSTRUCCIÓN**|La cadena de acción que se devuelve es una instrucción que se debe ejecutar estableciendo la **SetText** método de un objeto de comando con la cadena y la llamada la **ICommand:: Execute**método. Si el comando no ha funcionado, se muestra un error.|  
|**CONJUNTO DE DATOS**|La cadena de acción que se devuelve es una instrucción MDX que debe ejecutarse estableciendo la **SetText** método de un objeto de comando con la cadena y la llamada la **ICommand:: Execute** método. La interfaz solicitada debe ser el identificador (IID) **IDataset**. El comando tiene éxito si se ha creado un conjunto de datos. La aplicación cliente debe permitir al usuario explorar el conjunto de datos devuelto.|  
|**CONJUNTO DE FILAS**|Similar a **conjunto de datos**, pero en lugar de solicitar un IID de **IDataset**, la aplicación cliente debe solicitar un IID de **IRowset**. El comando tiene éxito si se ha creado un conjunto de filas. La aplicación cliente debe permitir al usuario explorar el conjunto de filas devuelto.|  
|**LÍNEA DE COMANDOS**|La aplicación cliente debe ejecutar la cadena de acción. La cadena es una línea de comandos.|  
|**PROPIETARIO**|Una aplicación cliente no debe mostrar, ni ejecutar la acción a menos que la aplicación tenga un conocimiento personalizado y no genérico de la acción específica. Las acciones de propietario no se devuelven a la aplicación cliente a menos que la aplicación cliente lo solicite explícitamente mediante el establecimiento de la restricción adecuada en la **$application_name**.|  
  
## <a name="invocation-types"></a>Tipos de invocación  
 En la tabla siguiente se describen los distintos tipos de invocaciones disponibles en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. La aplicación cliente solamente utiliza el tipo de invocación para ayudar a determinar cuando invocar la acción. El tipo de invocación no determina de hecho el comportamiento de invocación de la acción.  
  
|Tipo de invocación|Description|  
|---------------------|-----------------|  
|**INTERACTIVO**|La aplicación cliente debe invocar la acción mediante la interacción del usuario.|  
|**ON_OPEN**|La aplicación cliente debe invocar la acción cuando se abre el objeto de destino. Este tipo de invocación no está implementada actualmente.|  
|**PROCESO POR LOTES**|La aplicación cliente debe invocar la acción cuando el objeto de destino esté relacionado con una operación por lotes, según determine la aplicación cliente. Este tipo de invocación no está implementada actualmente.|  
  
### <a name="scope"></a>Ámbito  
 Cada acción se define para un cubo específico y tiene un nombre único en ese cubo. Uno de los ámbitos de la acción puede aparecer enumerado en la tabla siguiente.  
  
 Ámbito de cubo  
 Para las acciones con independencia de dimensiones, miembros o celdas concretos; por ejemplo: "Iniciar la emulación de terminal para el sistema de producción de AS/400."  
  
 Ámbito de dimensión  
 La acción se aplica a una dimensión específica. Estas acciones no dependen de la selección específica de niveles o miembros.  
  
 Ámbito de nivel  
 La acción se aplica a un nivel de dimensión específico. Estas acciones no dependen de la selección específica de un miembro de esa dimensión.  
  
 Ámbito de miembro  
 La acción se aplica a miembros de niveles específicos.  
  
 Ámbito de celda  
 La acción solo se aplica a celdas específicas.  
  
 Ámbito de conjunto  
 La acción solo se aplica a un conjunto. El nombre, **ActionParameterSet**, está reservado para su uso por la aplicación dentro de la expresión de la acción.  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones de definición de datos MDX &#40; MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  

---
title: Instrucción CREATE ACTION (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b723a706521b24c9aa216c46f617d8ff94997137
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098552"
---
# <a name="mdx-data-definition---create-action"></a>Definición de datos de MDX: CREATE ACTION


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
 *Cube_Name*  
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
 Es posible que las aplicaciones cliente creen y ejecuten acciones que no son seguras; también es posible que las aplicaciones cliente utilicen funciones no seguras. Para evitar estas situaciones, utilice el **Safety Options** propiedad. Para obtener más información, vea el tema sobre la propiedad de opciones de seguridad.  
  
> [!NOTE]  
>  Esta instrucción se incluye por compatibilidad con versiones anteriores. Las acciones nuevas para [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], como las acciones de obtención de detalles o informe, no se admiten.  
  
## <a name="action-types"></a>Tipos de acción  
 La tabla siguiente describen los diferentes tipos de acciones disponibles en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
|Tipo de acción|Descripción|  
|-----------------|-----------------|  
|**URL**|La cadena de acción que se devuelve es una dirección URL que debe abrirse mediante un explorador de Internet.<br /><br /> Nota: Si esta acción no se inicia con `https://` o `https://`, la acción no estará disponible en el explorador, a menos que **SafetyOptions** está establecido en **DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL**.|  
|**HTML**|La cadena de acción que se devuelve es un script HTML. La cadena debe guardarse en un archivo y ese archivo debe representarse mediante un explorador de Internet. En este caso, un script completo debe ejecutarse como parte del HTML generado.|  
|**INSTRUCCIÓN**|La cadena de acción devuelta es una instrucción que se debe ejecutar estableciendo el **SetText** método de un objeto de comando a la cadena y llamar a la **ICommand:: Execute**método. Si el comando no ha funcionado, se muestra un error.|  
|**CONJUNTO DE DATOS**|La cadena de acción devuelta es una instrucción MDX que debe ejecutarse estableciendo el **SetText** método de un objeto de comando a la cadena y llamar a la **ICommand:: Execute** método. La interfaz solicitada debe ser el identificador (IID) **IDataset**. El comando tiene éxito si se ha creado un conjunto de datos. La aplicación cliente debe permitir al usuario explorar el conjunto de datos devuelto.|  
|**ROWSET**|Similar a **DATASET**, pero en lugar de solicitar un IID de **IDataset**, la aplicación cliente debe solicitar un IID de **IRowset**. El comando tiene éxito si se ha creado un conjunto de filas. La aplicación cliente debe permitir al usuario explorar el conjunto de filas devuelto.|  
|**LÍNEA DE COMANDOS**|La aplicación cliente debe ejecutar la cadena de acción. La cadena es una línea de comandos.|  
|**PROPIETARIO**|Una aplicación cliente no debe mostrar, ni ejecutar la acción a menos que la aplicación tenga un conocimiento personalizado y no genérico de la acción específica. Las acciones de propietario no se devuelven a la aplicación cliente a menos que la aplicación cliente lo solicite explícitamente mediante el establecimiento de la restricción adecuada en el **APPLICATION_NAME**.|  
  
## <a name="invocation-types"></a>Tipos de invocación  
 En la tabla siguiente se describen los distintos tipos de invocaciones disponibles en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. La aplicación cliente solamente utiliza el tipo de invocación para ayudar a determinar cuando invocar la acción. El tipo de invocación no determina de hecho el comportamiento de invocación de la acción.  
  
|Tipo de invocación|Descripción|  
|---------------------|-----------------|  
|**INTERACTIVO**|La aplicación cliente debe invocar la acción mediante la interacción del usuario.|  
|**ON_OPEN**|La aplicación cliente debe invocar la acción cuando se abre el objeto de destino. Este tipo de invocación no está implementada actualmente.|  
|**BATCH**|La aplicación cliente debe invocar la acción cuando el objeto de destino esté relacionado con una operación por lotes, según determine la aplicación cliente. Este tipo de invocación no está implementada actualmente.|  
  
### <a name="scope"></a>Scope  
 Cada acción se define para un cubo específico y tiene un nombre único en ese cubo. Uno de los ámbitos de la acción puede aparecer enumerado en la tabla siguiente.  
  
 Ámbito de cubo  
 Para las acciones con independencia de dimensiones específicas, los miembros o celdas; Por ejemplo: "Iniciar la emulación de terminales para AS / 400 sistema de producción".  
  
 Ámbito de dimensión  
 La acción se aplica a una dimensión específica. Estas acciones no dependen de la selección específica de niveles o miembros.  
  
 Ámbito de nivel  
 La acción se aplica a un nivel de dimensión específico. Estas acciones no dependen de la selección específica de un miembro de esa dimensión.  
  
 Ámbito de miembro  
 La acción se aplica a miembros de niveles específicos.  
  
 Ámbito de celda  
 La acción solo se aplica a celdas específicas.  
  
 Ámbito de conjunto  
 La acción solo se aplica a un conjunto. El nombre, **ActionParameterSet**, está reservada para su uso por parte de la aplicación dentro de la expresión de la acción.  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones de definición de datos MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  

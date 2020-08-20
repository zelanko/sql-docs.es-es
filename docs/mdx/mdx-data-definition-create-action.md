---
description: 'Definición de datos de MDX: CREATE ACTION'
title: CREATE ACTION (instrucción, MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7132c28e93dbc11eee1c5a4e4d53126f280fa74a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494908"
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
  
 *Nombre del Action_*  
 Cadena válida que proporciona el nombre de la acción que se va a crear.  
  
 *Nombre del Hierarchy_*  
 Cadena válida que proporciona un nombre de jerarquía.  
  
 *Nombre del Level_*  
 Cadena válida que proporciona un nombre de nivel.  
  
 *Nombre del Member_*  
 Cadena válida que proporciona un nombre de miembro o una clave de miembro.  
  
 *MDX_Expression*  
 Una expresión MDX válida.  
  
 *String_Expression*  
 Expresión de cadena válida.  
  
## <a name="remarks"></a>Observaciones  
 Es posible que las aplicaciones cliente creen y ejecuten acciones que no son seguras; también es posible que las aplicaciones cliente utilicen funciones no seguras. Para evitar estas situaciones, utilice la propiedad **Opciones de seguridad** . Para obtener más información, vea el tema sobre la propiedad de opciones de seguridad.  
  
> [!NOTE]  
>  Esta instrucción se incluye por compatibilidad con versiones anteriores. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]No se admiten las acciones nuevas en, como las acciones de obtención de detalles o de informe.  
  
## <a name="action-types"></a>Tipos de acción  
 En la tabla siguiente se describen los distintos tipos de acciones disponibles en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
|Tipo de acción|Descripción|  
|-----------------|-----------------|  
|**URL**|La cadena de acción que se devuelve es una dirección URL que debe abrirse mediante un explorador de Internet.<br /><br /> Nota: Si esta acción no se inicia con `https://` o `https://` , la acción no estará disponible en el explorador a menos que **SafetyOptions** se establezca en **DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL**.|  
|**HTML**|La cadena de acción que se devuelve es un script HTML. La cadena debe guardarse en un archivo y ese archivo debe representarse mediante un explorador de Internet. En este caso, un script completo debe ejecutarse como parte del HTML generado.|  
|**PRIVACIDAD**|La cadena de acción devuelta es una instrucción que debe ejecutarse estableciendo el método **ICommand:: setText** de un objeto de comando en la cadena y llamando al método **ICommand:: Execute**. Si el comando no ha funcionado, se muestra un error.|  
|**AUTHORS1**|La cadena de acción devuelta es una instrucción MDX que debe ejecutarse estableciendo el método **ICommand:: setText** de un objeto Command en la cadena y llamando al método **ICommand:: Execute** . El identificador de interfaz (IID) solicitado debe ser **IDataset**. El comando tiene éxito si se ha creado un conjunto de datos. La aplicación cliente debe permitir al usuario explorar el conjunto de datos devuelto.|  
|**MULTIROW**|De forma similar a **DATASET**, pero en lugar de solicitar un IID de **IDataset**, la aplicación cliente debe solicitar un IID de **IRowset**. El comando tiene éxito si se ha creado un conjunto de filas. La aplicación cliente debe permitir al usuario explorar el conjunto de filas devuelto.|  
|**COMMANDLINE**|La aplicación cliente debe ejecutar la cadena de acción. La cadena es una línea de comandos.|  
|**COMPLEMENTARIA**|Una aplicación cliente no debe mostrar, ni ejecutar la acción a menos que la aplicación tenga un conocimiento personalizado y no genérico de la acción específica. Las acciones de propietario no se devuelven a la aplicación cliente a menos que la aplicación cliente las solicite explícitamente estableciendo la restricción adecuada en el **APPLICATION_NAME**.|  
  
## <a name="invocation-types"></a>Tipos de invocación  
 En la tabla siguiente se describen los distintos tipos de invocaciones disponibles en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. La aplicación cliente solamente utiliza el tipo de invocación para ayudar a determinar cuando invocar la acción. El tipo de invocación no determina de hecho el comportamiento de invocación de la acción.  
  
|Tipo de invocación|Descripción|  
|---------------------|-----------------|  
|**DICHO**|La aplicación cliente debe invocar la acción mediante la interacción del usuario.|  
|**ON_OPEN**|La aplicación cliente debe invocar la acción cuando se abre el objeto de destino. Este tipo de invocación no está implementada actualmente.|  
|**PROCESAMIENTO**|La aplicación cliente debe invocar la acción cuando el objeto de destino esté relacionado con una operación por lotes, según determine la aplicación cliente. Este tipo de invocación no está implementada actualmente.|  
  
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
 La acción solo se aplica a un conjunto. El nombre, **ActionParameterSet**, está reservado para su uso por parte de la aplicación dentro de la expresión de la acción.  
  
## <a name="see-also"></a>Consulte también  
 [Instrucciones de definición de datos de MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  

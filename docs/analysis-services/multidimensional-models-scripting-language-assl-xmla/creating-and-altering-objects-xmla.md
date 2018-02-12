---
title: Crear y modificar objetos (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- objects [XML for Analysis]
- subordinate objects [XML for Analysis]
- XML for Analysis, objects
- modifying objects
- removing objects
- deleting objects
- XMLA, objects
ms.assetid: a2080867-e130-440c-92eb-f768869f34a8
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6906c6dbab99923983cbfa4e75c35c6f3c0f5073
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2018
---
# <a name="creating-and-altering-objects-xmla"></a>Crear y modificar objetos (XMLA)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Los objetos principales se pueden crear, modificar y eliminar de forma independiente. Entre los objetos principales se incluyen los siguientes:  
  
-   Servidores  
  
-   Bases de datos  
  
-   Dimensiones  
  
-   Cubos  
  
-   Grupos de medida  
  
-   Particiones  
  
-   Perspectivas  
  
-   Modelos de minería de datos  
  
-   Roles  
  
-   Comandos asociados a un servidor o base de datos  
  
-   Orígenes de datos  
  
 Usa el [crear](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md) comando para crear un objeto principal en una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]y el [Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md) comando para modificar un objeto principal existente en una instancia. Ambos comandos se ejecutan utilizando el [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) método.  
  
## <a name="creating-objects"></a>Creación de objetos  
 Al crear objetos mediante el uso de la **crear** método, primero debe identificar el objeto primario que contiene el [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objeto que se va a crear. Para identificar el objeto primario, proporcione una referencia de objeto en el [ParentObject](../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md) propiedad de la **crear** comando. Cada referencia de objeto contiene los identificadores de objeto necesarios para identificar de forma única el objeto primario para el **crear** comando. Para obtener más información acerca de las referencias de objeto, vea [definir y la identificación de objetos &#40; XMLA &#41; ](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md).  
  
 Por ejemplo, debe proporcionar una referencia de objeto a un cubo para crear un nuevo grupo de medida para el cubo. La referencia de objeto para el cubo en el **ParentObject** propiedad contiene un identificador de base de datos y un identificador de cubo, como el mismo identificador de cubo podría utilizarse en otra base de datos.  
  
 El [ObjectDefinition](../../analysis-services/xmla/xml-elements-properties/objectdefinition-element-xmla.md) elemento contiene elementos de Analysis Services Scripting Language (ASSL) que definen el objeto principal que se va a crear. Para obtener más información acerca de ASSL, vea [desarrollar con Analysis Services Scripting Language &#40; ASSL &#41; ](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
 Si establece la **AllowOverwrite** atributo de la **crear** comando en true, se puede sobrescribir un objeto principal existente que tiene el identificador especificado. De lo contrario, si ya existe un objeto principal con el identificador especificado en el objeto primario, se produce un error.  
  
 Para obtener más información sobre la **crear** command, consulte [crear elemento &#40; XMLA &#41; ](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md).  
  
### <a name="creating-session-objects"></a>Crear objetos de sesión  
 Los objetos de sesión son objetos temporales que solo están disponibles para la sesión explícita o implícita utilizada por una aplicación cliente y que se eliminan cuando finaliza la sesión. Puede crear objetos de sesión estableciendo la **ámbito** atributo de la **crear** comando *sesión*.  
  
> [!NOTE]  
>  Cuando se usa el *sesión* establecer, el **ObjectDefinition** solo puede contener el elemento [dimensión](../../analysis-services/scripting/objects/dimension-element-assl.md), [cubo](../../analysis-services/scripting/objects/cube-element-assl.md), o [ MiningModel](../../analysis-services/scripting/objects/miningmodel-element-assl.md) elementos ASSL.  
  
## <a name="altering-objects"></a>Modificar objetos  
 Cuando se modifican objetos mediante el uso de la **Alter** método, primero debe identificar el objeto que se va a modificarse proporcionando una referencia de objeto en el [objeto](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) propiedad de la **Alter**comando. Cada referencia de objeto contiene los identificadores de objeto necesarios para identificar de forma única el objeto para el **Alter** comando. Para obtener más información acerca de las referencias de objeto, vea [definir y la identificación de objetos &#40; XMLA &#41; ](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md).  
  
 Por ejemplo, debe proporcionar una referencia de objeto a un cubo para modificar la estructura de un cubo. La referencia de objeto para el cubo en el **objeto** propiedad contiene un identificador de base de datos y un identificador de cubo, como el mismo identificador de cubo podría utilizarse en otra base de datos.  
  
 El **ObjectDefinition** elemento contiene elementos ASSL que definen el objeto principal que se va a modificarse. Para obtener más información acerca de ASSL, vea [desarrollar con Analysis Services Scripting Language &#40; ASSL &#41; ](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
 Si establece la **AllowCreate** atributo de la **Alter** comando en true, puede crear el objeto principal especificado si el objeto no existe. De lo contrario, si un objeto principal especificado no existe aún, se produce un error.  
  
### <a name="using-the-objectexpansion-attribute"></a>Utilizar el atributo ObjectExpansion  
 Si va a cambiar solo las propiedades del objeto principal y no desea redefinir los objetos secundarios que se encuentran en el objeto principal, puede establecer la **ObjectExpansion** atributo de la **Alter** comando *ObjectProperties*. El **ObjectDefinition** propiedad, a continuación, solo tiene que contienen los elementos para las propiedades del objeto principal y la **Alter** comando deja los objetos secundarios asociados con el objeto principal intacto.  
  
 Para volver a definir los objetos secundarios de un objeto principal, debe establecer el **ObjectExpansion** atribuir a *ExpandFull* y la definición del objeto debe incluir todos los objetos secundarios que se encuentran en el objeto principal. Si el **ObjectDefinition** propiedad de la **Alter** comando no incluye explícitamente un objeto secundario que se encuentra en el objeto principal, se elimina el objeto secundario que no se incluyó.  
  
### <a name="altering-session-objects"></a>Modificar objetos de sesión  
 Para modificar objetos de sesión creados por el **crear** comando, establezca la **ámbito** atributo de la **Alter** comando *sesión*.  
  
> [!NOTE]  
>  Cuando se usa el *sesión* establecer, el **ObjectDefinition** solo puede contener el elemento [dimensión](../../analysis-services/scripting/objects/dimension-element-assl.md), [cubo](../../analysis-services/scripting/objects/cube-element-assl.md), o [ MiningModel](../../analysis-services/scripting/objects/miningmodel-element-assl.md) elementos ASSL.  
  
## <a name="creating-or-altering-subordinate-objects"></a>Crear o modificar objetos subordinados  
 Aunque un **crear** o **Alter** comando crea o modifica solo un objeto principal de nivel superior, el objeto principal se crea o modifica puede contener definiciones en la envolvente  **ObjectDefinition** propiedad para otros objetos principales y secundarias que pertenecen a ella. Por ejemplo, si define un cubo, especifique la base de datos primaria en **ParentObject**y en la definición de cubo en **ObjectDefinition** puede definir grupos de medida para el cubo y, en la medida grupos, puede definir particiones para cada grupo de medida. Un objeto secundario solamente se puede definir bajo el objeto principal que lo contiene. Para obtener más información acerca de los objetos principales y secundarios, vea [objetos de base de datos &#40; Analysis Services - datos multidimensionales &#41; ](../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="description"></a>Description  
 En el ejemplo siguiente se crea un origen de datos relacional que hace referencia a la [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] ejemplo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos.  
  
### <a name="code"></a>código  
  
```  
<Create xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <ParentObject>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    </ParentObject>  
    <ObjectDefinition>  
        <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RelationalDataSource">  
            <ID>AdventureWorksDW2012</ID>  
            <Name>AdventureWorksDW2012</Name>  
            <ConnectionString>Data Source=localhost;Initial Catalog=AdventureWorksDW2008R2;Integrated Security=True</ConnectionString>  
            <ImpersonationInfo>  
                <ImpersonationMode>ImpersonateServiceAccount</ImpersonationMode>  
            </ImpersonationInfo>  
            <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
            <Timeout>PT0S</Timeout>  
        </DataSource>  
    </ObjectDefinition>  
</Create>  
```  
  
### <a name="description"></a>Description  
 En el ejemplo siguiente se modifica el origen de datos relacional creado en el ejemplo anterior para establecer en 30 segundos el tiempo de espera de consulta para el origen de datos.  
  
### <a name="code"></a>código  
  
```  
<Alter ObjectExpansion="ObjectProperties" xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <DataSourceID>AdventureWorksDW2012</DataSourceID>  
    </Object>  
    <ObjectDefinition>  
        <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RelationalDataSource">  
            <ID>AdventureWorksDW2012</ID>  
            <Name>AdventureWorksDW2012</Name>  
            <ConnectionString>Data Source=fr-dwk-02;Initial Catalog=AdventureWorksDW2008R2;Integrated Security=True</ConnectionString>  
            <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
            <Timeout>PT30S</Timeout>  
        </DataSource>  
    </ObjectDefinition>  
</Alter>  
```  
  
### <a name="comments"></a>Comentarios  
 El **ObjectExpansion** atributo de la **Alter** comandos se estableció en *ObjectProperties*. Esta configuración permite la [ImpersonationInfo](../../analysis-services/scripting/properties/impersonationinfo-element-assl.md) elemento, un objeto secundario, que se excluirán del origen de datos definido en **ObjectDefinition**. Por lo tanto, la información de suplantación de ese origen de datos permanece activa en la cuenta de servicio, como se especifica en el primer ejemplo.  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar método &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)   
 [Desarrollar con Analysis Services Scripting Language &#40; ASSL &#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Desarrollar con XMLA en Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  

---
title: Crear y modificar objetos (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- objects [XML for Analysis]
- subordinate objects [XML for Analysis]
- XML for Analysis, objects
- modifying objects
- removing objects
- deleting objects
- XMLA, objects
ms.assetid: a2080867-e130-440c-92eb-f768869f34a8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3dcc6eedc97b3d476d79420b4e067883e17f03d2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62702297"
---
# <a name="creating-and-altering-objects-xmla"></a>Crear y modificar objetos (XMLA)
  Los objetos principales se pueden crear, modificar y eliminar de forma independiente. Entre los objetos principales se incluyen los siguientes:  
  
-   Servidores  
  
-   Bases de datos  
  
-   Dimensions  
  
-   Cubos  
  
-   Grupos de medida  
  
-   Particiones  
  
-   perspectivas  
  
-   Modelos de minería de datos  
  
-   Roles  
  
-   Comandos asociados a un servidor o base de datos  
  
-   Orígenes de datos  
  
 Use el comando [Create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla) para crear un objeto principal en una instancia de y [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]el comando [ALTER](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla) para modificar un objeto principal existente en una instancia de. Ambos comandos se ejecutan mediante el método [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) .  
  
## <a name="creating-objects"></a>Crear objetos  
 Al crear objetos mediante el método `Create`, primero debe identificar el objeto primario que contiene el objeto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se va a crear. Para identificar el objeto primario, proporcione una referencia de objeto en la propiedad [ParentObject](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) del `Create` comando. Cada referencia de objeto contiene los identificadores de objeto necesarios para identificar de forma exclusiva el objeto primario para el comando `Create`. Para obtener más información acerca de las referencias a objetos, vea [definir e identificar objetos &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects).  
  
 Por ejemplo, debe proporcionar una referencia de objeto a un cubo para crear un nuevo grupo de medida para el cubo. La referencia de objeto para el cubo en la propiedad `ParentObject` contiene un identificador de base de datos y un identificador de cubo, ya que es posible que se utilice el mismo identificador de cubo en otra base de datos.  
  
 El elemento [ObjectDefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla) contiene elementos del lenguaje de scripting de Analysis Services (ASSL) que definen el objeto principal que se va a crear. Para obtener más información sobre ASSL, vea [desarrollar con Analysis Services lenguaje de scripting &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
 Si establece el atributo `AllowOverwrite` del comando `Create` en true, puede sobrescribir un objeto principal existente que tenga el identificador especificado. De lo contrario, si ya existe un objeto principal con el identificador especificado en el objeto primario, se produce un error.  
  
 Para obtener más información sobre `Create` el comando, vea [Create Element &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla).  
  
### <a name="creating-session-objects"></a>Crear objetos de sesión  
 Los objetos de sesión son objetos temporales que solo están disponibles para la sesión explícita o implícita utilizada por una aplicación cliente y que se eliminan cuando finaliza la sesión. Puede crear objetos de sesión estableciendo el `Scope` atributo del `Create` comando en *Session*.  
  
> [!NOTE]  
>  Cuando se usa ** la configuración de sesión `ObjectDefinition` , el elemento solo puede contener elementos ASSL de [dimensión](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl), [cubo](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl)o [MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) .  
  
## <a name="altering-objects"></a>Modificar objetos  
 Al modificar objetos mediante el `Alter` método, primero debe identificar el objeto que se va a modificar proporcionando una referencia de objeto en la propiedad de [objeto](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) del `Alter` comando. Cada referencia de objeto contiene los identificadores de objeto necesarios para identificar de forma exclusiva el objeto para el comando `Alter`. Para obtener más información acerca de las referencias a objetos, vea [definir e identificar objetos &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects).  
  
 Por ejemplo, debe proporcionar una referencia de objeto a un cubo para modificar la estructura de un cubo. La referencia de objeto para el cubo en la propiedad `Object` contiene un identificador de base de datos y un identificador de cubo, ya que es posible que se utilice el mismo identificador de cubo en otra base de datos.  
  
 El elemento `ObjectDefinition` contiene elementos ASSL que definen el objeto principal que se va a modificar. Para obtener más información sobre ASSL, vea [desarrollar con Analysis Services lenguaje de scripting &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
 Si establece el atributo `AllowCreate` del comando `Alter` en true, puede crear el objeto principal especificado si éste no existe. De lo contrario, si un objeto principal especificado no existe aún, se produce un error.  
  
### <a name="using-the-objectexpansion-attribute"></a>Utilizar el atributo ObjectExpansion  
 Si solo va a cambiar las propiedades del objeto principal y no está redefiniendo los objetos secundarios contenidos en el objeto principal, puede establecer el `ObjectExpansion` atributo del `Alter` comando en *ObjectProperties*. De este modo, la propiedad `ObjectDefinition` solo debe contener los elementos para las propiedades del objeto principal y el comando `Alter` conserva intactos los objetos secundarios asociados al objeto principal.  
  
 Para volver a definir los objetos secundarios de un objeto principal, debe `ObjectExpansion` establecer el atributo en *ExpandFull* y la definición del objeto debe incluir todos los objetos secundarios contenidos en el objeto principal. Si la propiedad `ObjectDefinition` del comando `Alter` no incluye de forma explícita un objeto secundario contenido en el objeto principal, se elimina el objeto secundario no incluido.  
  
### <a name="altering-session-objects"></a>Modificar objetos de sesión  
 Para modificar los objetos de sesión creados `Create` por el comando, `Scope` establezca el atributo `Alter` del comando en *Session*.  
  
> [!NOTE]  
>  Cuando se usa ** la configuración de sesión `ObjectDefinition` , el elemento solo puede contener elementos ASSL de [dimensión](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl), [cubo](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl)o [MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) .  
  
## <a name="creating-or-altering-subordinate-objects"></a>Crear o modificar objetos subordinados  
 Aunque los comandos `Create` o `Alter` crean o modifican solamente un objeto principal de nivel superior, el objeto principal que se crea o modifica puede contener definiciones para otros objetos principales y secundarios subordinados a éste dentro de la propiedad `ObjectDefinition` envolvente. Por ejemplo, si define un cubo, la base de datos primaria se especifica en `ParentObject` y, dentro de la definición del cubo en `ObjectDefinition`, puede definir grupos de medida para éste; a su vez, dentro de los grupos de medida, puede definir particiones para cada grupo de este tipo. Un objeto secundario solamente se puede definir bajo el objeto principal que lo contiene. Para obtener más información sobre los objetos principales y secundarios, vea [objetos de base de datos &#40;Analysis Services-&#41;de datos multidimensionales ](../multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="description"></a>Descripción  
 En el ejemplo siguiente se crea un origen de datos relacional [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hace referencia a la base de datos de [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] ejemplo.  
  
### <a name="code"></a>Código  
  
```  
<Create xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
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
  
### <a name="description"></a>Descripción  
 En el ejemplo siguiente se modifica el origen de datos relacional creado en el ejemplo anterior para establecer en 30 segundos el tiempo de espera de consulta para el origen de datos.  
  
### <a name="code"></a>Código  
  
```  
<Alter ObjectExpansion="ObjectProperties" xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
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
 El `ObjectExpansion` atributo del `Alter` comando se estableció en *ObjectProperties*. Esta configuración permite excluir el elemento [ImpersonationInfo](https://docs.microsoft.com/bi-reference/assl/properties/impersonationinfo-element-assl) , un objeto secundario, del origen de datos definido en `ObjectDefinition`. Por lo tanto, la información de suplantación de ese origen de datos permanece activa en la cuenta de servicio, como se especifica en el primer ejemplo.  
  
## <a name="see-also"></a>Consulte también  
 [Método Execute &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)   
 [Desarrollo con Analysis Services lenguaje de scripting &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Desarrollar con XMLA en Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  

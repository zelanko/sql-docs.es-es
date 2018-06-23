---
title: Crear y modificar objetos (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9702046c3e3c9e9ab0e9ff525d832baf611fe4b9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103929"
---
# <a name="creating-and-altering-objects-xmla"></a>Crear y modificar objetos (XMLA)
  Los objetos principales se pueden crear, modificar y eliminar de forma independiente. Entre los objetos principales se incluyen los siguientes:  
  
-   Servidores  
  
-   Bases de datos  
  
-   Dimensiones  
  
-   Cubos  
  
-   Grupos de medida  
  
-   Particiones  
  
-   perspectivas  
  
-   Modelos de minería de datos  
  
-   Roles  
  
-   Comandos asociados a un servidor o base de datos  
  
-   Orígenes de datos  
  
 Usa el [crear](../xmla/xml-elements-commands/create-element-xmla.md) comando para crear un objeto principal en una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]y el [Alter](../xmla/xml-elements-commands/alter-element-xmla.md) comando para modificar un objeto principal existente en una instancia. Ambos comandos se ejecutan utilizando el [Execute](../xmla/xml-elements-methods-execute.md) método.  
  
## <a name="creating-objects"></a>Creación de objetos  
 Al crear objetos mediante el método `Create`, primero debe identificar el objeto primario que contiene el objeto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se va a crear. Para identificar el objeto primario, proporcione una referencia de objeto en el [ParentObject](../xmla/xml-elements-properties/object-element-xmla.md) propiedad de la `Create` comando. Cada referencia de objeto contiene los identificadores de objeto necesarios para identificar de forma exclusiva el objeto primario para el comando `Create`. Para obtener más información acerca de las referencias de objeto, vea [definir e identificar objetos &#40;XMLA&#41;](../xmla/xml-elements-objects.md).  
  
 Por ejemplo, debe proporcionar una referencia de objeto a un cubo para crear un nuevo grupo de medida para el cubo. La referencia de objeto para el cubo en la propiedad `ParentObject` contiene un identificador de base de datos y un identificador de cubo, ya que es posible que se utilice el mismo identificador de cubo en otra base de datos.  
  
 El [ObjectDefinition](../xmla/xml-elements-properties/objectdefinition-element-xmla.md) elemento contiene elementos de Analysis Services Scripting Language (ASSL) que definen el objeto principal que se va a crear. Para obtener más información acerca de ASSL, vea [desarrollar con Analysis Services Scripting Language &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
 Si establece el atributo `AllowOverwrite` del comando `Create` en true, puede sobrescribir un objeto principal existente que tenga el identificador especificado. De lo contrario, si ya existe un objeto principal con el identificador especificado en el objeto primario, se produce un error.  
  
 Para obtener más información sobre la `Create` command, consulte [crear elemento &#40;XMLA&#41;](../xmla/xml-elements-commands/create-element-xmla.md).  
  
### <a name="creating-session-objects"></a>Crear objetos de sesión  
 Los objetos de sesión son objetos temporales que solo están disponibles para la sesión explícita o implícita utilizada por una aplicación cliente y que se eliminan cuando finaliza la sesión. Puede crear objetos de sesión estableciendo la `Scope` atributo de la `Create` comando *sesión*.  
  
> [!NOTE]  
>  Cuando se usa el *sesión* establecer, el `ObjectDefinition` solo puede contener el elemento [dimensión](../scripting/objects/dimension-element-assl.md), [cubo](../scripting/objects/cube-element-assl.md), o [MiningModel](../scripting/objects/miningmodel-element-assl.md) ASSL elementos.  
  
## <a name="altering-objects"></a>Modificar objetos  
 Cuando se modifican objetos mediante el uso de la `Alter` método, primero debe identificar el objeto que se va a modificarse proporcionando una referencia de objeto en el [objeto](../xmla/xml-elements-properties/object-element-xmla.md) propiedad de la `Alter` comando. Cada referencia de objeto contiene los identificadores de objeto necesarios para identificar de forma exclusiva el objeto para el comando `Alter`. Para obtener más información acerca de las referencias de objeto, vea [definir e identificar objetos &#40;XMLA&#41;](../xmla/xml-elements-objects.md).  
  
 Por ejemplo, debe proporcionar una referencia de objeto a un cubo para modificar la estructura de un cubo. La referencia de objeto para el cubo en la propiedad `Object` contiene un identificador de base de datos y un identificador de cubo, ya que es posible que se utilice el mismo identificador de cubo en otra base de datos.  
  
 El elemento `ObjectDefinition` contiene elementos ASSL que definen el objeto principal que se va a modificar. Para obtener más información acerca de ASSL, vea [desarrollar con Analysis Services Scripting Language &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
 Si establece el atributo `AllowCreate` del comando `Alter` en true, puede crear el objeto principal especificado si éste no existe. De lo contrario, si un objeto principal especificado no existe aún, se produce un error.  
  
### <a name="using-the-objectexpansion-attribute"></a>Utilizar el atributo ObjectExpansion  
 Si va a cambiar solo las propiedades del objeto principal y no desea redefinir los objetos secundarios que se encuentran en el objeto principal, puede establecer la `ObjectExpansion` atributo de la `Alter` comando *ObjectProperties*. De este modo, la propiedad `ObjectDefinition` solo debe contener los elementos para las propiedades del objeto principal y el comando `Alter` conserva intactos los objetos secundarios asociados al objeto principal.  
  
 Para volver a definir los objetos secundarios de un objeto principal, debe establecer el `ObjectExpansion` atribuir a *ExpandFull* y la definición del objeto debe incluir todos los objetos secundarios que se encuentran en el objeto principal. Si la propiedad `ObjectDefinition` del comando `Alter` no incluye de forma explícita un objeto secundario contenido en el objeto principal, se elimina el objeto secundario no incluido.  
  
### <a name="altering-session-objects"></a>Modificar objetos de sesión  
 Para modificar objetos de sesión creados por el `Create` comando, establezca la `Scope` atributo de la `Alter` comando *sesión*.  
  
> [!NOTE]  
>  Cuando se usa el *sesión* establecer, el `ObjectDefinition` solo puede contener el elemento [dimensión](../scripting/objects/dimension-element-assl.md), [cubo](../scripting/objects/cube-element-assl.md), o [MiningModel](../scripting/objects/miningmodel-element-assl.md) ASSL elementos.  
  
## <a name="creating-or-altering-subordinate-objects"></a>Crear o modificar objetos subordinados  
 Aunque los comandos `Create` o `Alter` crean o modifican solamente un objeto principal de nivel superior, el objeto principal que se crea o modifica puede contener definiciones para otros objetos principales y secundarios subordinados a éste dentro de la propiedad `ObjectDefinition` envolvente. Por ejemplo, si define un cubo, la base de datos primaria se especifica en `ParentObject` y, dentro de la definición del cubo en `ObjectDefinition`, puede definir grupos de medida para éste; a su vez, dentro de los grupos de medida, puede definir particiones para cada grupo de este tipo. Un objeto secundario solamente se puede definir bajo el objeto principal que lo contiene. Para obtener más información acerca de los objetos principales y secundarios, vea [objetos de base de datos &#40;Analysis Services - datos multidimensionales&#41;](../multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="description"></a>Descripción  
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
  
### <a name="description"></a>Descripción  
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
 El `ObjectExpansion` atributo de la `Alter` comandos se estableció en *ObjectProperties*. Esta configuración permite la [ImpersonationInfo](../scripting/properties/impersonationinfo-element-assl.md) elemento, un objeto secundario, que se excluirán del origen de datos definido en `ObjectDefinition`. Por lo tanto, la información de suplantación de ese origen de datos permanece activa en la cuenta de servicio, como se especifica en el primer ejemplo.  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar el método &#40;XMLA&#41;](../xmla/xml-elements-methods-execute.md)   
 [Desarrollar aplicaciones con Analysis Services Scripting Language &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Desarrollo con XMLA en Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
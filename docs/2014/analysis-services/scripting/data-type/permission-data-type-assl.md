---
title: Tipo de datos Permission (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Permission Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Permission
helpviewer_keywords:
- Permission data type
ms.assetid: 5f309544-59f8-4432-b1eb-b7c1a049f8df
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8d12fb71a8ed19ca083e8ec506fba6338f6b58a7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48101948"
---
# <a name="permission-data-type-assl"></a>Tipo de datos Permission (ASSL)
  Define un tipo de datos primitivo abstracto que representa información acerca de un permiso en particular.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Permission>  
   <Name>...</Name>  
   <ID>...</ID>  
   <CreatedTimestamp>...</CreateTimestamp>  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   <RoleID>...</RoleID>  
   <Description>...</Description>  
   <Process>...</Process>  
   <ReadDefinition>...</ReadDefinition>  
   <Read>...</Read>  
   <Write>...</Write>  
   <Annotations>...</Annotations>  
</Permission>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos básicos|None|  
|Tipos de datos derivados|[CubePermission](../objects/cubepermission-element-assl.md), [DatabasePermission](../objects/databasepermission-element-assl.md), [DimensionPermission](permission-data-type-assl.md), [MiningModelPermission](../objects/miningmodelpermission-element-assl.md), [MiningStructurePermission](../objects/miningstructurepermission-element-assl.md)|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[Las anotaciones](../collections/annotations-element-assl.md), [CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [descripción](../properties/description-element-assl.md), [ID](../properties/id-element-assl.md), [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [nombre](../properties/name-element-assl.md), [Proceso](../properties/process-element-assl.md), [lectura](../properties/read-element-assl.md), [ReadDefinition](../properties/readdefinition-element-assl.md), [RoleID](../properties/roleid-element-assl.md), [escribir](../properties/write-element-assl.md)|  
|Elementos derivados|None|  
  
## <a name="remarks"></a>Comentarios  
 `Permission` actúa como el tipo base abstracto de un número de tipos de permisos derivados que se utilizan en una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 Este tipo de datos tiene las validaciones siguientes en el valor 2 (modo de servidor tabular) de DeploymentMode.  
  
-   *Proceso* valor predeterminado del atributo se establece en `False`, excepto cuando el usuario tiene el **actualizar** permiso. Para los usuarios con el **actualizar** permiso la *proceso* el valor de atributo se establece en `True`.  
  
-   *ReadDefinition* el valor de atributo se establece en `None`; cualquier otro valor genera un error.  
  
-   *Lectura* el valor de atributo se establece en `Allowed` para los usuarios con el **usuario** permiso y `None` cuando los usuarios se asignan a la **actualizar** permiso; si un usuario tiene los **Usuario** y **actualizar** permisos y, a continuación, el atributo se establece en `Allowed`. Para los usuarios con privilegios de administrador, el valor del atributo se establece en `Allowed`.  
  
-   *Escribir* el valor de atributo se establece en `None`; cualquier otro valor genera un error.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Permission>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento role &#40;ASSL&#41;](../objects/role-element-assl.md)   
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

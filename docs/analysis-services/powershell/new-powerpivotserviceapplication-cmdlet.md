---
title: Cmdlet New-PowerPivotServiceApplication | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e36e6b170a141c7611c5eb246fd999beee970bf8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="new-powerpivotserviceapplication-cmdlet"></a>Cmdlet New-PowerPivotServiceApplication
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Crea una nueva aplicación de servicio de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  

>[!NOTE] 
>En este artículo puede contener información no actualizada y ejemplos. Use el cmdlet Get-Help para la versión más reciente.
  
 **Se aplica a:** SharePoint 2010 y SharePoint 2013.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
New-PowerPivotServiceApplication [-ServiceApplicationName] <string> [-DatabaseServerName] <string> [-DatabaseName] <string> [-AddToDefaultProxyGroup <switch>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 El cmdlet New-PowerPivotServiceApplication crea una nueva aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en la granja. Debe definir por lo menos una aplicación de servicio y debe ser un miembro del grupo de servicios de proxy predeterminado. Opcionalmente, puede crear aplicaciones de servicios adicionales si necesita modificar propiedades o la configuración. Debe asignarse la pertenencia de las aplicaciones de servicio adicionales a los grupos de conexiones de servicios personalizados. Solo una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] puede ser miembro del grupo de proxy predeterminado.  
  
 Una aplicación de servicio PowerPivot nueva se crea usando una configuración predeterminada. Para personalizar las propiedades de configuración, use el cmdlet Set-PowerPivotServiceApplication.  
  
## <a name="parameters"></a>Parámetros  
  
### <a name="-serviceapplicationname-string"></a>-Nombredeaplicacióndeservicio \<cadena >  
 Establece el nombre para mostrar de la aplicación de servicio.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|0|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-databaseservername-string"></a>-DatabaseServerName \<cadena >  
 Especifica una instancia del motor de base de datos relacional de SQL Server que hospeda la base de datos de aplicación. De forma predeterminada, puede usar el servidor de bases de datos de la granja o elegir otro servidor de bases de datos para el que tenga que crear derechos de base de datos.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|1|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-databasename-string"></a>-DatabaseName \<cadena >  
 Especifica el nombre de una base de datos relacional de SQL Server que almacena los datos de aplicación. Asegúrese de especificar un nombre que corresponda a la aplicación para que pueda identificar más fácilmente su propósito. Puede crear una base de datos o especificar una base de datos de aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para la aplicación que va a crear.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|2|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-addtodefaultproxygroup-switch"></a>-AddToDefaultProxyGroup \<cambiar >  
 Crea una conexión de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en el grupo de conexiones de servicio predeterminado. La pertenencia a este grupo determina las asociaciones entre las aplicaciones Web y las aplicaciones de servicio. Todas las aplicaciones web que se suscriban al grupo de conexiones de servicio predeterminado pueden usar la aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que agregue al grupo. Aunque puede tener varias aplicaciones de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en una granja, solo una puede ser miembro del grupo de conexiones de servicio predeterminado.  
  
 Si ya tiene una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que sea miembro del grupo de proxy predeterminado, debe establecer AddToDefautlProxyGroup: $false para la nueva aplicación que va a crear. Tendrá que agregar la aplicación de servicio nueva a un grupo de conexiones de servicio personalizado.  Puede usar los cmdlets integrados de SharePoint con este fin.  Get-SPServiceApplicationProxyGroup devuelve la lista de grupos de conexiones de servicio que están definidas en la granja.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 Este cmdlet admite parámetros comunes: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable,OutBuffer y OutVariable. Para obtener más información, vea [about_Commonparameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Entradas y salidas  
 El tipo de entrada es el tipo de objetos que se pueden canalizar al cmdlet. El tipo de valor devuelto es el tipo de objeto que el cmdlet devuelve.  
  
|||  
|-|-|  
|Entradas|Ninguno.|  
|Resultados|Ninguno.|  
  
## <a name="example-1"></a>Ejemplo 1  
  
```  
C:\PS>New-PowerPivotServiceApplication -ServiceApplicationName "PowerPivot Service Application" -DatabaseServerName "AdvWorks-SRV01\PowerPivot" -DatabaseName "PowerPivotServiceApp1" -AddtoDefaultProxyGroup:$true  
```  
  
 Este ejemplo crea una nueva aplicación de servicio. La base de datos de aplicación de servicio se crea en un servidor de bases de datos denominado AdvWorks-SRV01 que se instaló como una instancia con nombre de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , una configuración común para muchas instalaciones de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. Para crear la base de datos, debe tener permisos dbcreator en la instancia de SQL Server. Debe ser db_owner en la base de datos de configuración de SharePoint. Dado que se trata de la primera aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en la granja, debe ser un miembro del grupo predeterminado de servidores proxy.  
  
  

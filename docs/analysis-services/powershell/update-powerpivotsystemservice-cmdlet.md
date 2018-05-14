---
title: Cmdlet Update-PowerPivotSystemService | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3f09c45944b15f474bf9454303924c759ac6f6e9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="update-powerpivotsystemservice-cmdlet"></a>Cmdlet Update-PowerPivotSystemService
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Actualiza el objeto primario del Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en la granja.  

>[!NOTE] 
>En este artículo puede contener información no actualizada y ejemplos. Use el cmdlet Get-Help para la versión más reciente.
  
 **Se aplica a:** SharePoint 2010 y SharePoint 2013.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
Update-PowerPivotSystemService [-Confirm <switch>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 El cmdlet **Update-PowerPivotSystemService** ejecuta una serie de acciones de actualización en el objeto primario del Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , las instancias y las aplicaciones de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en la granja. Todos los servicios y aplicaciones de nivel intermedio de una implementación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint tienen que ejecutarse en el mismo nivel funcional. Este cmdlet ejecuta las acciones de actualización en todos estos objetos.  
  
 Ejecute este cmdlet después de ejecutar el programa de instalación de SQL Server para instalar una versión más reciente de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint o si ha aplicado una actualización acumulativa en el servidor. Para comprobar si la actualización se requiere, ejecute `Get-PowerPivotSystemService` para revisar la propiedad **NeedsUpgrade** . Si **NeedsUpgrade** es true, es necesario ejecutar los cmdlets para actualizar los objetos de nivel intermedio de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en la granja.  
  
 Como en una implementación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint se incluyen servicios de datos de nivel intermedio y back-end, es necesario ejecutar **Update-PowerPivotEngineService** siempre que se ejecute **Update-PowerPivotSystemService** para asegurarse de que ambos niveles tienen la misma versión en la granja.  
  
 La actualización no se puede revertir a la versión anterior. Si debe revertir a una versión anterior, quite [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] de la granja de servidores de SharePoint y vuelva a instalar el software. Para comprobar que la operación de actualización se realiza correctamente, ejecute `Get-PowerPivotSystemService` para revisar las propiedades globales y obtener información de la versión y para comprobar que **NeedsUpgrade** ya no está establecido en true.  
  
## <a name="parameters"></a>Parámetros  
  
### <a name="-confirm-switch"></a>-Confirme \<cambiar >  
 Le solicita confirmación antes de ejecutar el comando. Este valor se habilita de forma predeterminada. Para omitir la respuesta de confirmación de un comando, especifique Confirm:$false en el comando.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 Este cmdlet admite los siguientes parámetros:  
  
-   Verbose  
  
-   Depuración  
  
-   ErrorAction  
  
-   ErrorVariable  
  
-   WarningAction  
  
-   WarningVariable  
  
-   OutBuffer  
  
-   OutVariable  
  
 Para más información, vea [about_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Entradas y salidas  
 El tipo de entrada es el tipo de objetos que se pueden canalizar al cmdlet. El tipo de valor devuelto es el tipo de objeto que el cmdlet devuelve.  
  
|||  
|-|-|  
|Entradas|Ninguno.|  
|Resultados|Ninguno.|  
  
  

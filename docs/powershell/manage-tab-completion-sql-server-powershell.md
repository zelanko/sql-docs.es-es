---
title: Administración de la finalización mediante tabulador (SQL Server PowerShell) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 6296848a-890f-4ad3-8d9f-92ed6a79aa00
author: markingmyname
ms.author: maghan
ms.openlocfilehash: db8338f832d27fb5362cb44d3b4cf82212472957
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67912240"
---
# <a name="manage-tab-completion-sql-server-powershell"></a>Administrar la finalización mediante tabulador (SQL Server PowerShell)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]


Los complementos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell introducen tres variables ( **$SqlServerMaximumTabCompletion**, **$SqlServerMaximumChildItems**y **$SqlServerIncludeSystemObjects**) para controlar la finalización mediante el tabulador de Windows PowerShell. La finalización mediante el tabulador reduce la cantidad de texto que se debe escribir al devolver las tablas de elementos cuyos nombres empiezan por la cadena que está escribiendo.  

> [!NOTE]
> Hay dos módulos de SQL Server PowerShell: **SqlServer** y **SQLPS**. El módulo **SQLPS** está incluido en la instalación de SQL Server (por motivos de compatibilidad con versiones anteriores), pero ya no se actualiza. El módulo de PowerShell más actualizado es **SqlServer**. El módulo **SqlServer** contiene versiones actualizadas de los cmdlets en **SQLPS**, así como nuevos cmdlets para admitir las características más recientes de SQL.  
> Las versiones anteriores del módulo **SqlServer***estaban incluidas* en SQL Server Management Studio (SSMS), pero solo con las versiones 16.x de SSMS. Para usar PowerShell con SSMS 17.0 y versiones posteriores, debe tener el módulo **SqlServer** instalado desde la Galería de PowerShell.
> Para instalar el módulo **SqlServer**, consulte [Instalar SQL Server PowerShell](download-sql-server-ps-module.md).
  
Con la finalización mediante el tabulador de PowerShell, cuando se ha escrito parte de una ruta de acceso o nombre de cmdlet, se puede presionar la tecla Tab para obtener una lista de los elementos cuyos nombres coincidan con lo que ya se ha escrito. Se puede seleccionar a continuación el elemento que desee en la lista sin tener que escribir el resto del nombre.  
  
Si está trabajando en una base de datos que tiene varios objetos, las listas para finalización mediante tabulador pueden llegar a ser grandes. Algunos tipos de objeto de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , como las vistas, también tienen una gran cantidad de objetos de sistema.  
  
Los complementos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] presentan tres variables del sistema que se pueden usar para controlar la cantidad de información presentada por la finalización mediante tabulador y **Get-ChildItem**.  
  
 **$SqlServerMaximumTabCompletion =** *n*  
 Especifica el número máximo de objetos que se incluyen en una lista de finalización mediante tabulador. Si selecciona Tab en un nodo de ruta de acceso que tiene más de *n* objetos, la lista de finalización mediante tabulador se trunca en *n*. *n* es un entero. El valor predeterminado es 0, es decir, no hay límite para el número de objetos que se muestran.  
  
 **$SqlServerMaximumChildItems =** *n*  
 Especifica el número máximo de objetos mostrados por **Get-ChildItem**. Si se ejecuta **Get-ChildItem** en un nodo de ruta de acceso que tiene más de *n* objetos, la lista se trunca en *n*. *n* es un entero. El valor predeterminado es 0, es decir, no hay límite para el número de objetos que se muestran.  
  
 **$SqlServerIncludeSystemObjects =** { **$True** |  **$False** }  
 Si es **$True**, los objetos del sistema se muestran con finalización mediante tabulador y **Get-ChildItem**. Si es **$False**, no se muestran objetos del sistema. El valor de configuración predeterminado es **$False**.  
  
## <a name="set-the-sql-server-tab-completion-variables"></a>Establecer las variables de finalización mediante tabulador de SQL Server  
 Para cualquiera de las variables a las que desee cambiar el valor predeterminado, establezca la variable en el nuevo valor.  
  
### <a name="example-powershell"></a>Ejemplo (PowerShell)  
 En el ejemplo siguiente se establecen las tres variables y se enumeran sus valores:  
  
```  
$SqlServerMaximumTabCompletion = 20  
$SqlServerMaximumChildItems = 10  
$SqlServerIncludeSystemObjects = $False  
dir variable:sqlserver*  
```  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
